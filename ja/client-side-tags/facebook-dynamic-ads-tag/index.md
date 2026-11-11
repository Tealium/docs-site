---
title: タグ管理で Facebook ダイナミック広告を構成する方法
description: ダイナミック広告は、訪問が操作した商品に基づいて商品を推奨するリターゲティングサービスです。
url: https://docs.tealium.com/ja/client-side-tags/facebook-dynamic-ads-tag/
---
この記事では、訪問が操作した商品に関するデータを Facebook に提供し、Facebook がそれらのイベントに基づいて処理を実行できるようにする方法について説明します。

## 前提条件

この記事の手順は、Facebook アカウントをすでに所有しており、Facebook Business Manager で商品カタログを構成済みであることを前提としています。この構成により、訪問が関心を示した商品に基づいて、Facebook がイベントを正確にリターゲティングできるようになります。([詳細はこちら](https://business.facebook.com))。

## タグ管理で Facebook Pixel を構成する

最初に、TiQ に [Facebook タグ](https://docs.tealium.com/facebook-pixel-legacy/)を追加する必要があります。

Facebook タグをすでに追加している場合は、そのタグを使用できます。別のインスタンスを追加する必要はありません。


<blockquote>
Facebook タグテンプレートの最新バージョンを使用していることを確認してください。使用中のバージョンを確認するには、**Tag Status Checker** を使用します。最新バージョンでない場合は、テンプレートを更新してください。
</blockquote>


## 必須イベントを構成する

ダイナミック広告サービスでは、次の 3 つの Facebook イベントを送信する必要があります。

* ViewContent
* AddToCart
* Purchase

### ViewContent イベントを構成する

ViewContent イベントは、訪問が商品を閲覧したことを示し、通常は商品の詳細ページで送信されます。ダイナミック広告では、少なくとも以下で説明する `content_ids` パラメーターと `content_type` パラメーターを、このイベントとともに指定する必要があります。

ViewContent イベントは通常、商品の閲覧に関連付けられ、ページの読み込みに紐付けることができます。そのため、ページの読み込み時に存在するデータソースを確認すると便利です。

次の手順に従って、ViewContent イベントのマッピングを構成します。

1. Facebook タグで編集アイコンをクリックします。
1. **Data Mappings** タブをクリックします。
1. **Data Sources** ドロップダウンリストから、商品ページを一意に識別するデータソースを選択します。  
この例では、`page_type` を使用します。
1. **Events** タブをクリックします。
1. **Trigger** フィールドに、商品ページの `page_type` 値を入力します。  
1. **Event** ドロップダウンリストから **ViewContent** を選択します。
1. **+ Add** をクリックします。  
マッピングを示すオレンジ色のテキストフィールドが表示されます。
1. **Close** をクリックしてマッピングを送信します。  
1. 構成を保存するため、変更内容を保存してパブリッシュします。

### AddToCart イベントを構成する

AddToCart イベントは、訪問が特定の商品をカートまたは買い物かごに追加したことを示します。ダイナミック広告では、このイベントにも以下で説明する `content_ids` パラメーターと `content_type` パラメーターが必要です。

カートへの商品の追加操作は通常、商品ページ上のボタンのクリックに紐付けられます。AddToCart イベントを送信するには、そのイベントのデータソースの値を基準にする必要があります。この例では、`event_name` データソースを使用します。

次の手順に従って、AddToCart イベントを構成します。

1. Facebook タグで編集アイコンをクリックします。
1. **Data Mappings** タブをクリックします。
1. AddToCart イベントが送信されるタイミングを示すデータソースを選択します。
1. **Events** タブをクリックします。
1. **Trigger** フィールドに、カート追加イベントの `event_name` 値を入力します。
1. **Event** ドロップダウンリストから **AddToCart** を選択します。
1. **+ Add** をクリックします。マッピングを示すオレンジ色のテキストフィールドが表示されます。
1. **Close** をクリックしてマッピングを送信します。
1. 構成を保存するため、変更内容を保存してパブリッシュします。

### Purchase イベント

注文 ID がマッピングされた E-Commerce 拡張機能をすでに構成している場合は、Purchase イベントのマッピングを構成する必要はありません。E-Commerce 拡張機能が構成されている場合、注文 ID に値が入力されると Purchase イベントが自動的に送信されます。([詳細はこちら](https://docs.tealium.com/e-commerce-extension/))。

E-Commerce 拡張機能を使用していない場合は、ViewContent イベントの構成手順を参考にして Purchase イベントを構成します。例として、`page_type` が「order confirmation」に等しいことを条件とするマッピングを使用します。

## イベントとともに送信する必須パラメーターを構成する

これらの各イベントでは、特定のパラメーター、具体的には `content_ids` と `content_type` を送信する必要があります。`value`、`content_name`、`currency` などの追加パラメーターを構成すると、より有用なデータを分析に活用できます。E-Commerce 拡張機能を構成している場合、これらのデータソースは自動的にマッピングされます。

### content_ids パラメーター

`content_ids` パラメーターには、訪問が閲覧した商品の ID または SKU が含まれます。E-Commerce 拡張機能を構成している場合、これらのパラメーターは、拡張機能の List of Product IDs フィールドで選択したデータソースによってマッピングされ、値が入力されます。([詳細はこちら](https://docs.tealium.com/e-commerce-extension/))。

E-Commerce 拡張機能を使用していない場合、または別のデータソースを使用する場合は、3 つの各イベントについて、データソースを `content_ids` パラメーターにマッピングします。

### content_type パラメーター

`content_type` パラメーターは、コンテンツまたは商品 ID が単一の商品を示すのか、商品のグループを示すのかを Facebook に伝えます。それぞれの場合に応じて、このパラメーターを「`product`」または「`product_group`」のいずれかに構成する必要があります。これを行うには、Set Data Value 拡張機能を使用します。


<blockquote>
この要件は Facebook 固有のものです。この処理を実行するデータソースがすでに存在する可能性は低いと考えられます。
</blockquote>


次の手順に従い、Set Data Value 拡張機能を使用して `content_type` を構成します。

1. Set Data Value 拡張機能を追加します。([詳細はこちら](https://docs.tealium.com/set-data-values-extension/))。  
`Facebook: Setting content_type` など、内容が分かるタイトルを使用します。
1. 拡張機能のスコープを Facebook タグに構成します。  
この拡張機能は Facebook タグにのみ必要であり、Facebook タグが読み込まれたときにのみ実行する必要があります。
1. データソースを作成するには、**Set** ドロップダウンリストの横にあるプラス（**+**）ボタンをクリックします。
1. `fb_content_type` など、データソースの用途が分かる名前を使用します。  
このデータソースの目的は、`content_type` の値を提供することです。
1. **To:** フィールドで、**Text** が選択されていることを確認します。
1. テキストフィールドに `product` または `product_group` を入力します。  
これで、`content_type` に適切な値を持つデータソースを構成する拡張機能が作成されます。
1. Facebook タグのマッピングにこの新しいデータソースを追加するには、**Data Mappings** タブをクリックします。
1. **Data Sources** ドロップダウンリストから、`fb_content_type` データソースを選択します。
1. **Parameters** タブをクリックします。  
これにより、選択したイベントのパラメーターマッピングを構成できます。
1. **Event** ドロップダウンリストから、コンテンツタイプをマッピングする最初のイベントとして `ViewContent` を選択します。
1. **Parameter** ドロップダウンリストから **Content Type** を選択します。
1. **+ Add** をクリックします。  
マッピングが正常に完了したことを示す青色のテキストフィールドが **Mappings** ダイアログに表示されます。
1. `AddToCart` イベントと `Purchase` イベントについて、上記の手順を繰り返します。
1. **Close** をクリックします。
1. **Apply** をクリックしてマッピングを送信します。
1. 構成を保存するため、変更内容を保存してパブリッシュします。
  
## トラブルシューティング

Facebook は、Chrome 用の Facebook Pixel Helper ブラウザー拡張機能を提供しています。この拡張機能を Chrome ブラウザーに追加すると、ページ上で送信されたイベント、イベントに含まれていたパラメーター、および Facebook が検出したエラーに関する情報を確認できます。([詳細はこちら](https://developers.facebook.com/docs/ads-for-websites/pixel-troubleshooting))。

## ベンダーのドキュメント

* [Facebook ダイナミック商品広告](https //developers.facebook.com/docs/facebook-pixel/pixel-with-ads/dynamic-product-ads)