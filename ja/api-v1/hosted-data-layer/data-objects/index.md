---
title: ホストされたデータレイヤーオブジェクト
description: Tealiumのサーバー上にデータレイヤーオブジェクトまたはJSONファイルを作成します。
url: https://docs.tealium.com/ja/api-v1/hosted-data-layer/data-objects/
---
これは、[現行のTealiumホストデータレイヤーAPI](https://docs.tealium.com/about-hosted-data-layer-api/)の古いバージョンです。


## ホストされたデータレイヤーオブジェクトの作成

データレイヤーオブジェクトを作成するには、以下の手順を使用します：

1. 次の例に示すように、フラットなJSONファイルで新しい変数を定義します：  
      
<blockquote>
JSONペイロードは1 MBを超えてはなりません。
</blockquote>


        ```json
      {
          "product_category"           : ["Accessories"],
          "product_brand"              : ["Acme"],
          "product_sku"                : ["GEN-PRD-BLU"],
          "product_has_free_shipping"  : ["0"],
          "product_has_instore_pickup" : ["1"]
      }
        ```
  
1. ファイル名を命名ガイドラインに従って構成します。例："prod123456.json"。 
1. HTTPS POSTリクエストを行って、オブジェクトをTealiumにアップロードします。
1. （オプション）次の形式のアップロードされたJSON URLをプレビューします：  
`https://tags.tiqcdn.com/dle/{account}/{profile}/{dl_id}.js`


<blockquote>
アカウント名、プロファイル名、および`dl_id`名の合計は250文字を超えてはなりません。
</blockquote>
