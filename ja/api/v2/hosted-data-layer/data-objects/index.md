---
title: ホストされたデータレイヤーオブジェクト
description: Tealiumのサーバー上にデータレイヤーオブジェクトまたはJSONファイルを作成します。
url: https://docs.tealium.com/ja/api/v2/hosted-data-layer/data-objects/
---
## ホストされたデータレイヤーオブジェクトを作成する

ホストされたデータレイヤーオブジェクトを作成するには、以下の手順を使用します：

1. 次の例に示すように、フラットなJSONファイルで新しい変数を定義します：  
JSONペイロードは1 MBを超えてはなりません。
  
      ```json
      {
          "product_category"           : ["Accessories"],
          "product_brand"              : ["Acme"],
          "product_sku"                : ["GEN-PRD-BLU"],
          "product_has_free_shipping"  : ["0"],
          "product_has_instore_pickup" : ["1"]
      }
      ```

1. ファイルを命名ガイドラインに従って名前を付けて保存します。  
例：`prod123456.json`  
`account`、`profile`、および`datalayer_id`の名前の合計は250文字を超えてはなりません。
1. HTTPS POSTリクエストを作成して、ホストされたデータレイヤーオブジェクトをTealiumにアップロードします。
1. （オプション）以下のURLを入力して、アップロードされたデータレイヤーオブジェクトをプレビューします：  
      ```bash
      https://tags.tiqcdn.com/dle/{account}/{profile}/{datalayer_id}.js
      ```
JSONファイルの場合は、_.json_ ファイル拡張子を使用します。
