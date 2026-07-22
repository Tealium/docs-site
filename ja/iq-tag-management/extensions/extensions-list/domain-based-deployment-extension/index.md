---
title: ドメインベースのデプロイメント拡張
description: ドメインベースのデプロイメント拡張を使用して、ホスト名に基づいてQAまたはDevバージョンのUniversal Tag（utag.js）をロードします。これは通常、Prodインスタンスのutag.jsがQAまたはDevサイトでロードされている場合の検証目的で使用されます。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/domain-based-deployment-extension/
---
## 前提条件

* [拡張について]()を参照してください。

## 動作方法

ドメインベースのデプロイメント拡張は、ホスト名（JavaScriptウィンドウ変数`location.hostname`）に基づいてQAまたはDevバージョンのUniversal Tag（`utag.js`）をロードします。`utag.js`がページでロードされると、ドメインベースの拡張はすぐに実行され、現在のホスト名が宣言された環境のいずれかと一致するかどうかをチェックします。一致がある場合、適切な環境バージョンの`utag.js`がロードされます。

## 拡張の使用

拡張が追加されると、次の構成オプションが利用可能になります：

* **Dev Domains**: テストに使用したい開発環境のドメインを入力します。例えば、`dev.tealium.com`。
* **QA Domains**: テストに使用したいQA環境のドメインを入力します。例えば、`qa.tealium.com`。

新しいDev/QA環境を追加するには、プラスボタン（**+**）をクリックし、Dev/QA環境を削除するにはマイナスボタン（**-**）をクリックします。

## 例

あなたの本番ウェブサイトには次のスクリプトが含まれています：

``` javascript
<script type="text/javascript">
(function(a,b,c,d){
a='https://tags.tiqcdn.com/utag/my_account/main/**prod**/utag.js';
b=document;c='script';d=b.createElement(c);d.src=a;d.type='text/java'+c;d.async=true;
a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
})();
</script>
```

この例では、環境は**prod**（**qa**や**dev**ではない）です。

* この`utag.js`ファイルがロードされると、ドメインベースの拡張はすぐに実行され、現在のホスト名が`dev.tealium.com`または`qa.tealium.com`（または他の宣言された環境）であることを確認します。
* ホスト名が宣言された環境のいずれかと一致する場合、適切な環境がロードされます。

次の例は、この例に対してロードされる`utag.js`ファイルを示しています：

* **dev.tealium.com**
    ``` javascript
    <script type="text/javascript">
    (function(a,b,c,d){
    a='https://tags.tiqcdn.com/utag/my_account/main/**dev**/utag.js';
    b=document;c='script';d=b.createElement(c);d.src=a;d.type='text/java'+c;d.async=true;
    a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
    })();
    </script>
    ```

* **qa.tealium.com**
    ``` javascript
    <script type="text/javascript">
    (function(a,b,c,d){
    a='https://tags.tiqcdn.com/utag/my_account/main/**qa**/utag.js';
    b=document;c='script';d=b.createElement(c);d.src=a;d.type='text/java'+c;d.async=true;
    a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
    })();
    </script>
    ```

サイトのトラフィックを表示すると、非本番環境が検出された場合、まず`/**prod**/utag.js`がロードされ、次に`/**dev**/utag.js`または`/**qa**/utag.js`がロードされます。その後にロードされる`utag.#.js`ファイルは、それぞれの**Dev**または**QA**環境から提供されます。
