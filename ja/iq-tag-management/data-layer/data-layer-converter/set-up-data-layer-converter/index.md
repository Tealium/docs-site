---
title: データレイヤーコンバーターのセットアップ
url: https://docs.tealium.com/ja/iq-tag-management/data-layer/data-layer-converter/set-up-data-layer-converter/
---
データレイヤーコンバーターは、JavaScriptコードを拡張機能に貼り付け、コードの一部を調整して特定のデータレイヤー変換に対応することで、アカウントに追加されます。

追加された機能は、次のいずれかの方法（または両方）で使用されます：

* **ページデータオブジェクトの変換**  
ソースデータオブジェクトをUniversal Data Object（`utag_data`）に変換します（すべてのページロード時）。
* **トラッキングコールの変換**  
ソースデータオブジェクトを`utag.view()`および`utag.link()`の呼び出しごとに変換します。

## コードのコピー


```js
//Define the teal global namespace
window.teal = window.teal || {};
teal.ignore_keys = {};
teal.replace_keys = {};
teal.prefix = "";

//In cases of a nested object, what should join the parent key and child key
teal.nested_delimiter = ".";

//Ignore keys in the data layer that start with the following text.
//Expecting an object of strings
/*
teal.ignore_keys = {
  "user" : 1,
  "util" : 1
};
*/

//Specify a prefix for data layer elements being sent to the utag_data object.
//Instead of utag_data.productID, it could be utag_data.dl_productID
// teal.prefix = "dl_";

//Keys to be removed from the new flattened key name
//For a flattened key, you have digitalData.page.pageInfo.pageName and you want digitalData.page.pi.pageName
/* teal.replace_keys = {
    "pageInfo":"pi"
  };
*/

//For a flattened key, you have digitalData.page.pageInfo.pageName and you want digitalData.page.pageName
/* teal.replace_keys = {
    "pageInfo":""
  };
*/

//For a flattened key, you have digitalData.page.pageInfo.pageName and you want digitalData.pageName
/* teal.replace_keys = {
    "page":"",
    "pageInfo":""
  };
*/

/*****************DO NOT MODIFY BELOW***********************/

teal.flattener_version = 1.4;

// From https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys
// Add the Object.keys method for older versions of IE
Object.keys||(Object.keys=function(){"use strict";var a=Object.prototype.hasOwnProperty,b=!{toString:null}.propertyIsEnumerable("toString"),c=["toString","toLocaleString","valueOf","hasOwnProperty","isPrototypeOf","propertyIsEnumerable","constructor"],d=c.length;return function(e){if("object"!=typeof e&&("function"!=typeof e||null===e))throw new TypeError("Object.keys called on non-object");var g,h,f=[];for(g in e)a.call(e,g)&&f.push(g);if(b)for(h=0;h<d;h++)a.call(e,c[h])&&f.push(c[h]);return f}}());

teal.ignoreKey = function(key,re){
  var should_ignore_key = 0;
  //Build a new array to avoid running through Object.keys multiple times
  if(typeof teal.ignore_keys_list === 'undefined'){
    teal.ignore_keys_list = Object.keys(teal.ignore_keys);
    teal.ignore_keys_list.forEach(function(name){
      //Store a copy of the regex in the object
      teal.ignore_keys[name] = new RegExp("^"+name);
      if(key.match(teal.ignore_keys[name])){
        should_ignore_key = 1;
      }
    });
  }else{
    //Loop through the ignore_keys object to see if we should ignore this key
    teal.ignore_keys_list.forEach(function(name){
      if(key.match(teal.ignore_keys[name])){
        should_ignore_key = 1;
      }
    });
  }
  return should_ignore_key;
}

teal.getKeyName = function(key,re){
  //Create a new object to store regexs or use existing one
  teal.replace_keys_regex = teal.replace_keys_regex || {};
  //Build a new array to avoid running through Object.keys multiple times
  if(typeof teal.replace_keys_list === 'undefined'){
    teal.replace_keys_list = Object.keys(teal.replace_keys);
    //Make a start of string and end of string regex
    teal.replace_keys_regex.startOfString = new RegExp("^[" + teal.nested_delimiter + "]");
    teal.replace_keys_regex.endOfString = new RegExp("[" + teal.nested_delimiter + "]$");
    teal.replace_keys_list.forEach(function(name){
      //Store a copy of the regex in the teal.replace_keys_regex object so that the regexs are only built once
      teal.replace_keys_regex[name] = new RegExp("[" + teal.nested_delimiter + "]?" + name + "[" + teal.nested_delimiter + "]?", "g");
      key = teal.keyReplace(key,name,teal.replace_keys_regex[name]);
    });
  }else{
    //Loop through the replace_keys object to see what we should be replacing
    teal.replace_keys_list.forEach(function(name){
      key = teal.keyReplace(key,name,teal.replace_keys_regex[name]);
    });
  }
  return key;
}

teal.keyReplace = function(key,name,re){
  //Check to see if we are replacing the key name with a new value or if we are removing the key altogether
  if(teal.replace_keys[name] === ''){
    //The key needs to be removed completely
    key = key.replace(re,teal.nested_delimiter);
    //Check to see if the key starts with the nested delimiter and if so, remove it
    if(key.indexOf(teal.nested_delimiter) === 0){
      var cleanRegEx = new RegExp("^[" + teal.nested_delimiter + "]");
      key = key.replace(cleanRegEx,'');
    }
  }else{
    //Make a copy of the original key to see how we need to update the key name
    var origKey = key;
    //Replace the key name
    key = key.replace(re,teal.nested_delimiter + teal.replace_keys[name] + teal.nested_delimiter);
    //Check for the start of the origKey to see of the nested delimiter is there
    if(!origKey.match(teal.replace_keys_regex.startOfString)){
      //Remove the nested delimiter from the start of the string
      var cleanRegEx = new RegExp("^[" + teal.nested_delimiter + "]");
      key = key.replace(cleanRegEx,'');
    }
    //Check for the end of the origKey to see of the nested delimiter is there
    if(!origKey.match(teal.replace_keys_regex.endOfString)){
      //Add the nested delimiter to the end of the string
      var cleanRegEx = new RegExp("[" + teal.nested_delimiter + "]$");
      key = key.replace(cleanRegEx,'');
    }
  }
  return key;
}

teal.processDataObject = function(obj,new_obj,parent_key,create_array){
  if(typeof parent_key === "undefined"){
    //This object isn't nested in another object
    parent_key = "";
  }else{
    //Add the nested_delimiter to the parent key if the delimiter isn't already at the end
    teal.nested_delimiter_regex = teal.nested_delimiter_regex || new RegExp("["+teal.nested_delimiter+"]$");
    if(!parent_key.match(teal.nested_delimiter_regex)){
      parent_key += ""+teal.nested_delimiter;
    }
  }
  Object.keys(obj).forEach(function(key){
    var nested_key_name = parent_key+key;
    //Format the new key name and take out any whitespace
    var new_key_name = teal.getKeyName((teal.prefix+parent_key+key).replace(https://docs.tealium.com/\s/g, ''));
    //Set the key_type to limit the number of typeof checks
    var key_type = teal.typeOf(obj[key]);
    if(key_type !== 'undefined' && key_type != null){
      if(key_type.match(https://docs.tealium.com/boolean|string|number|date/) && !teal.ignoreKey(key)){
        //If obj[key] is a date, convert to ISOString
        if(teal.typeOf(obj[key]) === 'date'){
          obj[key] = obj[key].toISOString();
        }
        //Check to see if we need to create an array for this data point
        if(create_array){
          //First check to see if this key exists
          if(teal.typeOf(new_obj[new_key_name]) !== "array"){
            //Make the key an array
            new_obj[new_key_name] = [];
          }
          new_obj[new_key_name].push(""+obj[key]); //Force value to be a string
        }else{
          //If the value of the key is a boolean or a string or a number and
          //the key shouldn't be ignored add to the data layer
          new_obj[new_key_name] = ""+obj[key]; //Force value to be a string
        }
      }else if(key_type === 'object' && !teal.ignoreKey(key)){
        //Process this piece of the data layer and merge it
        teal.processDataObject(obj[key],new_obj,nested_key_name,create_array);
      }else if(key_type === 'array'){
        teal.processDataArray(obj[key],new_obj,nested_key_name);
      }
    }
  });
}

teal.processDataArray = function(obj,new_obj,parent_key){
  var objLength = obj.length;
  if(typeof parent_key === "undefined"){
    //This object isn't nested in another object
    parent_key = "";
  }else if(objLength > 0 && teal.typeOf(obj[0]).match(https://docs.tealium.com/boolean|string|number|date/)){
    //This is a normal array that doesn't need a nested delimiter
  }else{
    //Add the nested_delimiter to the parent key
    parent_key += ""+teal.nested_delimiter;
  }
  //Format the new key name and take out any whitespace
  var new_key_name = teal.getKeyName((teal.prefix+parent_key).replace(https://docs.tealium.com/\s/g, ''));
  for(var n = 0; n < objLength; n++){
    var key_type = teal.typeOf(obj[n]);
    if(key_type.match(https://docs.tealium.com/boolean|string|number|date/)){
      //If obj[n] is a date, convert to ISOString
      if(key_type === 'date'){
        obj[n] = obj[n].toISOString();
      }
      //First check to see if this key exists
      if(teal.typeOf(new_obj[new_key_name]) !== "array"){
        //Make the key an array
        new_obj[new_key_name] = [];
      }
      //If the value of the key is a boolean or a string or a number and
      //the key shouldn't be ignored add to the data layer
      new_obj[new_key_name].push(""+obj[n]);
    }else if(key_type === 'object'){
      teal.processDataObject(obj[n],new_obj,new_key_name,1);
    }
  }
}

teal.typeOf = function(e){return ({}).toString.call(e).match(https://docs.tealium.com/\s([a-zA-Z]+)/)[1].toLowerCase();}

teal.flattenObject = function(obj,new_obj){
  //Make sure object exists
  if(typeof obj === 'undefined'){
    return false;
  }
  //Check to see if we want to flatten the same object and keep the reference
  var mergeObject = false;
  if(obj === new_obj){
    mergeObject = true;
    //Start off a clean copy of the object
    new_obj = {};
  }
  //Make sure new object exists
  if(typeof new_obj === 'undefined'){
    new_obj = {};
  }
  //Check to see if this object is an array
  if(teal.typeOf(obj) === 'array'){
    //Store a safe copy of this object in case we are processing the b object
    var temp_array = JSON.parse(JSON.stringify(obj));
    var temp_array_length = temp_array.length;
    //Clean up the object
    obj = {};
    //Let's see if the obj and new_obj are the same.  If so, going to assume we are using the b object
    if(obj == new_obj){
      //Let's ensure that we have the a object
      if(typeof a === 'undefined'){
        var a = 'view';
      }
      //Add the automatic utag data points
      utag.loader.RD(new_obj,a);
    }
    for(var i = 0; i < temp_array_length; i++){
        teal.processDataObject(temp_array[i],new_obj);
    }
  }else{
    teal.processDataObject(obj,new_obj);
  }
  if(mergeObject){
    //Need to delete everything out of obj and replace with new_obj
    Object.keys(obj).forEach(function(key){
      delete obj[key];
    });
    //Now that we have a clean original object, add everything from new_obj which allows the reference to be kept
    Object.keys(new_obj).forEach(function(key){
      obj[key] = new_obj[key];
    });
  }

  return new_obj;
}
```


## 拡張機能の追加

以下の手順に従って、データレイヤーコンバーターコードを追加します。

1. 左のサイドバーで、**Tag Management > Extensions**に移動します。
1. [JavaScriptコード拡張機能]()を追加します。
1. **タイトル**フィールドに`Data Layer Converter`と入力します。
1. **スコープ**フィールドで**Pre Loader**を選択します。
1. **ドラフト名**フィールドにドラフトの名前を入力します。
1. コピーしたコードを拡張機能の**JavaScript**フィールドに貼り付けます。  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-data-layer-converter-add-js-extension.jpg)
1. **Approve for Publish**をクリックし、ターゲットを選択します。

以下の手順に従って、データレイヤーコンバーターをトリガーするコードを追加します。

1. 左のサイドバーで、**Tag Management > Extensions**に移動します。
1. [JavaScript拡張機能]()を追加します。
1. **タイトル**フィールドに`Convert to utag_data`と入力します。
1. **スコープ**フィールドで**Pre Loader**を選択します。
1. **ドラフト名**フィールドにドラフトの名前を入力します。
1. 次のコードをJavaScriptフィールドにコピーして貼り付けます:  
    ```js
    utag_data = teal.flattenObject(digitalData);
    ```

<blockquote>
`digitalData`をデータレイヤーオブジェクトの名前に更新してください。
</blockquote>

1. この拡張機能が、前の手順で作成した**Data Layer Converter**拡張機能の下に表示されていることを確認します。
1. **Approve for Publish**をクリックし、ターゲットを選択します。
1. 1つ以上のパブリッシュ環境を選択し、**Apply**をクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-data-layer-converter-approve-for-publish.jpg)  
1. 変更内容を保存して公開します。