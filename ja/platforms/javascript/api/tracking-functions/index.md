---
title: トラッキング関数
description: Tealium for JavaScript で提供されているトラッキング関数に関するリファレンス ガイド。
url: https://docs.tealium.com/ja/platforms/javascript/api/tracking-functions/
---
以下のトラッキング関数を利用できます。

| Function | 説明|
| --- | ---|
| `utag.link()` | 非ページビュー、ページでのインタラクション、その他の動的ページ イベントをトラッキングします|
| `utag.track()` | 第 1 のパラメータ値に基づき、ページ ビューまたはイベントのいずれかをトラッキングします|
| `utag.view()` | ページビュー、仮想ページ ビュー、および Ajax ページ フローをトラッキングします|

## `utag.link()`

非ページビュー、ページでのインタラクション、その他の動的ページ イベントをトラッキングします。この関数を呼び出すと、構成されたベンダー タグ内の対応するベンダー トラッキング機能がトリガーされます。 

```javascript
utag.link(data_object, callback, [uid_array]);
```

| パラメータ | 説明|
| --- | ---|
| `data_object`| イベントに関連付けられたデータレイヤー変数を含むデータ オブジェクト。|
| `callback`| トラッキング コールの完了後に実行される関数。|
| `uid_array`| トリガーするタグ UID の配列。|

配信ルールの結果に関わらず、`uid_array` パラメータで指定されたタグは必ず実行されます。。

## `utag.track()`

第 1 のパラメータ値に基づき、ページ ビューまたはイベントのいずれかをトラッキングします。[`utag.link()`](/ja/platforms/javascript/api/tracking-functions#utag-link) および [`utag.view()`](/ja/platforms/javascript/api/#utag-view) の双方が、この関数をラップします。

```javascript
utag.track(event_type, data_object, callback, [uid_array]);
```

| パラメータ | 説明|
| --- | ---|
| `event_type` | イベントのタイプ。ページ ビューについては `view` に構成し、イベントについては `link` に構成します|
| `data_object`| イベントに関連付けられたデータレイヤー変数を含むデータ オブジェクト。|
| `callback`| トラッキング コールの完了後に実行される関数。|
| `uid_array`| トリガーするタグ UID の配列。|


配信ルールの結果に関わらず、`uid_array` パラメータで指定されたタグは必ず実行されます。。

## `utag.view()`

ページビュー、仮想ページ ビュー、および Ajax ページ フローをトラッキングします。この関数を呼び出すと、構成されたベンダータグ内の対応するページ トラッキング機能がトリガーされます。 `utag.js` は、ページが読み込まれるたびに、この関数を自動的にトリガーします。

```javascript
utag.view(data_object, callback, [uid_array]);
```

| パラメータ | 型| 説明|
| --- | ---| --- |
| `data_object` | オブジェクト| (オプション) この特定のトラッキングコールに関連付けられた属性を含むデータオブ ジェクト。ユニバーサル データ オブジェクトと同じ形式および変数名を使用します。|
| `callback` | 関数| (オプション) トラッキング コールの完了後に実行される関数。|
| `uid_array` | 配列| (オプション) タグ ID の配列。この配列の UID で指定されるベンダー タグに対してトラッキング コールを限定します。|

配信ルールの結果に関わらず、`uid_array` パラメータで指定されたタグは必ず実行されます。。
