---
title: ホストされたデータレイヤーオブジェクト
description: Tealiumのサーバー上にデータレイヤーオブジェクトまたはJSONファイルを作成します。
url: https://docs.tealium.com/ja/api-v1/hosted-data-layer/data-objects/
---
これは、[現行のTealiumホストデータレイヤーAPI]()の古いバージョンです。


## ホストされたデータレイヤーオブジェクトの作成

データレイヤーオブジェクトを作成するには、以下の手順を使用します：

1. 次の例に示すように、フラットなJSONファイルで新しい変数を定義します：  
      JSONペイロードは1 MBを超えてはなりません。

        ```json
      {
          &#34;product_category&#34;           : [&#34;Accessories&#34;],
          &#34;product_brand&#34;              : [&#34;Acme&#34;],
          &#34;product_sku&#34;                : [&#34;GEN-PRD-BLU&#34;],
          &#34;product_has_free_shipping&#34;  : [&#34;0&#34;],
          &#34;product_has_instore_pickup&#34; : [&#34;1&#34;]
      }
        ```
  
1. ファイル名を命名ガイドラインに従って構成します。例：&#34;prod123456.json&#34;。 
1. HTTPS POSTリクエストを行って、オブジェクトをTealiumにアップロードします。
1. （オプション）次の形式のアップロードされたJSON URLをプレビューします：  
`https://tags.tiqcdn.com/dle/{account}/{profile}/{dl_id}.js`

アカウント名、プロファイル名、および`dl_id`名の合計は250文字を超えてはなりません。