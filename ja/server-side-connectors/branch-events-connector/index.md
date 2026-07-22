---
title: ブランチイベントコネクタ構成ガイド
description: この記事では、ブランチイベントDSPコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/branch-events-connector/
---## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|コマースイベントを記録| ✓| ✓|
|コンテンツイベントを記録| ✓| ✓|
|ライフサイクルイベントを記録| ✓| ✓|
|カスタムイベントを記録| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **ブランチキー**  
この値は、**ブランチアカウントマネージャー**の**プロファイル**ページで見つかります。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに進みます。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - コマースイベントを記録


#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントタイプ|  <ul><li>(必須) コマースイベントのタイプを選択してください。</li></ul> |
|OSタイプ|  <ul><li>(必須) モバイルデバイスのオペレーティングシステムのタイプを選択してください。</li></ul> |
|デバイスID|  <ul><li>(必須) 1つまたは2つのデバイスIDを指定してください。</li><li>OSタイプによって異なるIDを選択できます。</li></ul> |
|ユーザーデータ|  <ul><li>(オプション) 必要に応じて多くのデバイス識別パラメータを指定してください：</li> <ul><li>**OSバージョン** <ul><li>数値</li><li>オペレーティングシステムのバージョン。</li><li>AndroidおよびiOSに特有です。</li></ul> </li><li>**環境** <ul><li>文字列</li><li>通常は `FULL_APP`。</li></ul> </li><li>**ユーザーエージェント** <ul><li>文字列</li><li>イベントが発生したブラウザまたはアプリのユーザーエージェント。</li></ul> </li><li>**HTTPオリジン** <ul><li>文字列</li><li>Web SDKがWebセッション開始を記録した現在のページのURL。</li></ul> </li><li>**HTTPリファラー** <ul><li>文字列</li><li>Web SDKがWebセッション開始を記録した現在のページにつながる参照URL。</li></ul> </li><li>**ローカルIP** <ul><li>文字列</li><li>デバイスのローカルIP（Androidのみ）。</li></ul> </li><li>**国** <ul><li>文字列</li><li>通常、デバイスの構成またはユーザーエージェント文字列に基づいたユーザーの国コード。</li></ul> </li><li>**言語** <ul><li>文字列</li><li>通常、デバイスの構成またはユーザーエージェント文字列に基づいたユーザーの言語コード。</li></ul> </li><li>**ブランド** <ul><li>文字列</li><li>デバイスのブランド。</li></ul> </li><li>**モデル** <ul><li>文字列</li><li>デバイスのモデル。</li></ul> </li><li>**アプリバージョン** <ul><li>文字列</li><li>ユーザーがダウンロードしたアプリのバージョン。</li></ul> </li><li>**スクリーンDPI** <ul><li>数値</li><li>スクリーンDPI。</li></ul> </li><li>**スクリーンの高さ** <ul><li>数値</li><li>スクリーンの高さ。</li></ul> </li><li>**スクリーンの幅** <ul><li>数値</li><li>スクリーンの幅。</li></ul> </li><li>**開発者ID** <ul><li>文字列</li><li>ユーザーに対して開発者が指定したID。</li></ul> </li><li>**デバイスフィンガープリントID** <ul><li>Branch社内専用のデバイス追跡フィールド。</li></ul> </li><li>**ブラウザフィンガープリントID** <ul><li>Branch社内専用のブラウザ追跡フィールド。</li></ul> </li><li>**広告追跡制限** <ul><li>パートナーが広告主による追跡を拒否した場合、値はTrueです。</li></ul> </li><li>**デバイスIP** <ul><li>イベントが発生したデバイスのIPアドレス。</li><li>この値にクライアントIP属性をマッピングします。**この属性は推奨されます。**</li></ul> </li></ul> </ul> |
|イベントデータ|  <ul><li>(オプション) イベントに特有のデータ。</li> <ul><li>**トランザクションID** <ul><li>文字列</li><li>パートナーが内部使用のために指定したトランザクションID。</li></ul> </li><li>**通貨** <ul><li>文字列</li><li>パートナーが元々報告した収益、価格、送料、税金の通貨。</li></ul> </li><li>**収益** <ul><li>数値</li><li>パートナーが報告したイベントの収益。</li></ul> </li><li>**送料** <ul><li>数値</li><li>トランザクションに関連する送料。</li></ul> </li><li>**税金** <ul><li>数値</li><li>トランザクションに関連する総税金。</li></ul> </li><li>**クーポン** <ul><li>文字列</li><li>トランザクションで使用されたクーポン。</li><li>例: `SPRING2017`。</li></ul> </li><li>**提携** <ul><li>文字列</li><li>このトランザクションが発生した店舗または提携先。</li><li>例: `Google Store`。</li></ul> </li><li>**説明** <ul><li>文字列</li><li>イベントに関連する説明で、特定の個々のコンテンツアイテムに必ずしも特有ではありません。</li></ul> </li></ul> </ul> |
|カスタムデータ|  <ul><li>(オプション) 任意のプロパティ名と値で追加データを指定してください。</li></ul> |
|コンテンツ項目|  <ul><li>(オプション) コンテンツ項目のプロパティを、等しい長さの配列型の値、またはすべての項目に適用される単一の値として指定します。<ul><li>コンテンツスキーマ</li><li>コンテンツのカテゴリまたはスキーマで、将来的に分析に使用される可能性があります。</li><li>以下のいずれか:  <ul><li>`COMMERCE_AUCTION`</li><li>`COMMERCE_BUSINESS`</li><li>`COMMERCE_OTHER`</li><li>`COMMERCE_PRODUCT`</li><li>`COMMERCE_RESTAURANT`</li><li>`COMMERCE_SERVICE`</li><li>`COMMERCE_TRAVEL_FLIGHT`</li><li>`COMMERCE_TRAVEL_HOTEL`</li><li>`COMMERCE_TRAVEL_OTHER`</li><li>`GAME_STATE`</li><li>`MEDIA_IMAGE`</li><li>`MEDIA_MIXED`</li><li>`MEDIA_MUSIC`</li><li>`MEDIA_OTHER`</li><li>`MEDIA_VIDEO`</li><li>`OTHER`</li><li>`TEXT_ARTICLE`</li><li>`TEXT_BLOG`</li><li>`TEXT_OTHER`</li><li>`TEXT_RECIPE`</li><li>`TEXT_REVIEW`</li><li>`TEXT_SEARCH_RESULTS`</li><li>`TEXT_STORY`</li><li>`TEXT_TECHNICAL_DOC`</li></ul> </li><li>**タイトル** <ul><li>個々のコンテンツ項目のタイトル。</li></ul> </li><li>**説明** <ul><li>個々のコンテンツ項目の説明。</li></ul> </li><li>**画像 URL** <ul><li>個々のコンテンツ項目の画像 URL。</li></ul> </li><li>**正規識別子** <ul><li>コンテンツ分析のためにBranchがコンテンツ/メッセージを統合するのを許可するために使用されます。</li></ul> </li><li>**公開インデックス可能** <ul><li>値が `true` の場合、誰でもコンテンツを閲覧できます。</li><li>値が `false` の場合、公共の使用のためにインデックスを作成できません。</li></ul> </li><li>**ローカルインデックス可能** <ul><li>値が `true` の場合、ローカル（デバイス）で使用するためにインデックスを作成できます。</li><li>値が `false` の場合、ローカルで使用するためにインデックスを作成できません。</li></ul> </li><li>**価格** <ul><li>製品/コンテンツの価格。</li></ul> </li><li>**数量** <ul><li>注文するアイテムの数量。</li><li>例: `PURCHASE`, `ADD_TO_CART`</li></ul> </li><li>**SKU** <ul><li>製品 SKU または製品 ID。</li></ul> </li><li>**製品名** <ul><li>製品の名前。</li></ul> </li><li>**製品ブランド** <ul><li>製品のブランド。</li></ul> </li><li>**製品カテゴリ** <ul><li>該当する場合の製品のカテゴリ。</li><li>以下のいずれか:  <ul><li>`ANIMALS_AND_PET_SUPPLIES`</li><li>`APPAREL_AND_ACCESSORIES`</li><li>`ARTS_AND_ENTERTAINMENT`</li><li>`BABY_AND_TODDLER`</li><li>`BUSINESS_AND_INDUSTRIAL`</li><li>`CAMERAS_AND_OPTICS`</li><li>`ELECTRONICS`</li><li>`FOOD_BEVERAGES_AND_TOBACCO`</li><li>`FURNITURE`</li><li>`HARDWARE`</li><li>`HEALTH_AND_BEAUTY`</li><li>`HOME_AND_GARDEN`</li><li>`LUGGAGE_AND_BAGS`</li><li>`MATURE`</li><li>`MEDIA`</li><li>`OFFICE_SUPPLIES`</li><li>`RELIGIOUS_AND_CEREMONIAL`</li><li>`SOFTWARE`</li><li>`SPORTING_GOODS`</li><li>`TOYS_AND_GAMES`</li><li>`VEHICLES_AND_PARTS`</li></ul> </li></ul> </li><li>**製品バリアント** <ul><li>製品のバリアント。</li><li>例: `red`。</li></ul> </li><li>**平均評価** <ul><li>アイテムの平均評価。</li></ul> </li><li>**評価数** <ul><li>アイテムの評価数。</li></ul> </li><li>**最大評価** <ul><li>アイテムの最大可能評価。</li><li>例: 最高評価が5つ星の場合は `5.0`。</li></ul> </li><li>**作成タイムスタンプ** <ul><li>コンテンツが作成された時間。</li></ul> </li><li>**有効期限** <ul><li>このコンテンツが有効でなくなる最後の時刻。</li><li>`Null` / は制限なしを意味します。</li><li>ほとんど構成されるべきではありません。</li></ul> </li><li>**状態** <ul><li>オークションの場合、アイテムが新品、良好、許容可能などの状態。</li><li>以下のいずれか:  <ul><li>`OTHER`</li><li>`NEW`</li><li>`EXCELLENT`</li><li>`GOOD`</li><li>`FAIR`</li><li>`POOR`</li><li>`USED`</li><li>`REFURBISHED`</li></ul> </li></ul> </li><li>**キーワード** <ul><li>キーワード。</li></ul> </li><li>**画像キャプション** <ul><li>カンマ区切りの値の文字列。</li><li>画像に関連するキャプション。</li></ul> </li><li>**緯度** <ul><li>レストラン、ビジネス、部屋（ホテル）などの緯度。</li></ul> </li><li>**経度** <ul><li>レストラン、ビジネス、部屋（ホテル）などの経度。</li></ul> </li><li>**郵便番号** <ul><li>レストラン、ビジネス、部屋（ホテル）などの郵便番号/ZIPコード。</li></ul> </li><li>**国** <ul><li>レストラン、ビジネス、部屋（ホテル）などの国コード。</li></ul> </li><li>**地域** <ul><li>レストラン、ビジネス、部屋（ホテル）などの州または地域。</li></ul> </li><li>**市** <ul><li>レストラン、ビジネス、部屋（ホテル）などの市。</li></ul> </li><li>**通り** <ul><li>レストラン、ビジネス、部屋（ホテル）などの通り住所。</li></ul> </li><li>**カスタムフィールド** <ul><li>アプリ開発者がコンテンツ項目に添付したいキーと値のペア。</li></ul> </li></ul> </li></ul> |

### アクション - コンテンツイベントの記録


#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントタイプ|  <ul><li>(必須) コマースイベントのタイプを選択してください。</li></ul> |
|OSタイプ|  <ul><li>(必須) モバイルデバイスのオペレーティングシステムのタイプを選択してください。</li></ul> |
|デバイスID|  <ul><li>(必須) 1つまたは2つのデバイスIDを指定してください。</li><li>OSタイプによって異なるIDを選択できます。</li></ul> |
|ユーザーデータ|  <ul><li>(オプション) 必要に応じて多くのデバイス識別パラメータを指定してください：</li> <ul><li>**OSバージョン** <ul><li>番号</li><li>オペレーティングシステムのバージョン。</li><li>AndroidおよびiOSに特有です。</li></ul> </li><li>**環境** <ul><li>文字列</li><li>通常は "**FULL_APP**"。</li></ul> </li><li>**ユーザーエージェント** <ul><li>文字列</li><li>イベントが発生したブラウザまたはアプリのユーザーエージェント。</li></ul> </li><li>**HTTPオリジン** <ul><li>文字列</li><li>Web SDKがWebセッション開始を記録した現在のページのURL。</li></ul> </li><li>**HTTPリファラー** <ul><li>文字列</li><li>Web SDKがWebセッション開始を記録した現在のページにつながった参照URL。</li></ul> </li><li>**ローカルIP** <ul><li>文字列</li><li>デバイスのローカルIP（Androidのみ）。</li></ul> </li><li>**国** <ul><li>文字列</li><li>通常、デバイスの構成またはユーザーエージェント文字列に基づいたユーザーの国コード。</li></ul> </li><li>**言語** <ul><li>文字列</li><li>通常、デバイスの構成またはユーザーエージェント文字列に基づいたユーザーの言語コード。</li></ul> </li><li>**ブランド** <ul><li>文字列</li><li>デバイスのブランド。</li></ul> </li><li>**モデル** <ul><li>文字列</li><li>デバイスのモデル。</li></ul> </li><li>**アプリバージョン** <ul><li>文字列</li><li>ユーザーがダウンロードしたアプリのバージョン。</li></ul> </li><li>**スクリーンDPI** <ul><li>数値</li><li>スクリーンDPI。</li></ul> </li><li>**スクリーンの高さ** <ul><li>数値,</li><li>スクリーンの高さ。</li></ul> </li><li>**スクリーンの幅** <ul><li>数値</li><li>スクリーンの幅。</li></ul> </li><li>**開発者ID** <ul><li>文字列</li><li>ユーザーに対して開発者が指定したID。</li></ul> </li><li>**デバイスフィンガープリントID** <ul><li>Branch内部専用のデバイス追跡フィールド。</li></ul> </li><li>**ブラウザフィンガープリントID** <ul><li>Branch内部専用のブラウザ追跡フィールド。</li></ul> </li><li>**広告追跡制限** <ul><li>パートナーが広告主による追跡を拒否した場合、値はTrueです。</li></ul> </li><li>**デバイスIP** <ul><li>イベントが発生したデバイスのIPアドレス。</li><li>この値にクライアントIP属性をマッピングします。**この属性は推奨されます。**</li></ul> </li></ul> </ul> |
|イベントデータ|  <ul><li>(オプション) イベントに特有のデータ。</li> <ul><li>**検索クエリ** <ul><li>文字列</li><li>イベントに関連する検索クエリ。</li></ul> </li><li>説明__ <ul><li>文字列</li><li>イベントに関連する説明で、個々のコンテンツアイテムに必ずしも特有ではありません。</li></ul> </li></ul> </ul> |
|カスタムデータ|  <ul><li>(オプション) 任意のプロパティ名と値で追加データを指定してください</li></ul> |
|コンテンツアイテム|  <ul><li>(オプション) コンテンツアイテムのプロパティを、同じ長さの配列型の値として、またはすべてのアイテムに適用される単一の値として指定してください。  <ul><li>コンテンツスキーマ</li><li>コンテンツのカテゴリまたはスキーマで、将来的に分析に使用される可能性があります。</li><li>次のいずれか:  <ul><li>`COMMERCE_AUCTION`</li><li>`COMMERCE_BUSINESS`</li><li>`COMMERCE_OTHER`</li><li>`COMMERCE_PRODUCT`</li><li>`COMMERCE_RESTAURANT`</li><li>`COMMERCE_SERVICE`</li><li>`COMMERCE_TRAVEL_FLIGHT`</li><li>`COMMERCE_TRAVEL_HOTEL`</li><li>`COMMERCE_TRAVEL_OTHER`</li><li>`GAME_STATE`</li><li>`MEDIA_IMAGE`</li><li>`MEDIA_MIXED`</li><li>`MEDIA_MUSIC`</li><li>`MEDIA_OTHER`</li><li>`MEDIA_VIDEO`</li><li>`OTHER`</li><li>`TEXT_ARTICLE`</li><li>`TEXT_BLOG`</li><li>`TEXT_OTHER`</li><li>`TEXT_RECIPE`</li><li>`TEXT_REVIEW`</li><li>`TEXT_SEARCH_RESULTS`</li><li>`TEXT_STORY`</li><li>`TEXT_TECHNICAL_DOC`</li></ul> </li><li>**タイトル** <ul><li>個々のコンテンツアイテムのタイトル。</li></ul> </li><li>**説明** <ul><li>個々のコンテンツアイテムの説明。</li></ul> </li><li>**画像URL** <ul><li>個々のコンテンツアイテムの画像URL。</li></ul> </li><li>**正規識別子** <ul><li>Branchがコンテンツ/メッセージを統合するために使用する識別子。</li></ul> </li><li>**公開インデックス可能** <ul><li>値が `true` の場合、誰でもコンテンツを閲覧できます。</li><li>値が `false` の場合、公開用にインデックスを作成できません。</li></ul> </li><li>**ローカルインデックス可能** <ul><li>値が `true` の場合、ローカル（デバイス）用にインデックスを作成できます。</li><li>値が `false` の場合、ローカル用にインデックスを作成できません。</li></ul> </li><li>**価格** <ul><li>製品/コンテンツの価格。</li></ul> </li><li>**数量** <ul><li>注文されるアイテムの数量。</li><li>例: `PURCHASE`, `ADD_TO_CART`</li></ul> </li><li>**SKU** <ul><li>製品SKUまたは製品ID。</li></ul> </li><li>**製品名** <ul><li>製品の名前。</li></ul> </li><li>**製品ブランド** <ul><li>製品のブランド。</li></ul> </li><li>**製品カテゴリ** <ul><li>該当する場合、製品のカテゴリ。</li><li>次のいずれか:  <ul><li>`ANIMALS_AND_PET_SUPPLIES`</li><li>`APPAREL_AND_ACCESSORIES`</li><li>`ARTS_AND_ENTERTAINMENT`</li><li>`BABY_AND_TODDLER`</li><li>`BUSINESS_AND_INDUSTRIAL`</li><li>`CAMERAS_AND_OPTICS`</li><li>`ELECTRONICS`</li><li>`FOOD_BEVERAGES_AND_TOBACCO`</li><li>`FURNITURE`</li><li>`HARDWARE`</li><li>`HEALTH_AND_BEAUTY`</li><li>`HOME_AND_GARDEN`</li><li>`LUGGAGE_AND_BAGS`</li><li>`MATURE`</li><li>`MEDIA`</li><li>`OFFICE_SUPPLIES`</li><li>`RELIGIOUS_AND_CEREMONIAL`</li><li>`SOFTWARE`</li><li>`SPORTING_GOODS`</li><li>`TOYS_AND_GAMES`</li><li>`VEHICLES_AND_PARTS`</li></ul> </li></ul> </li><li>**製品バリアント** <ul><li>製品のバリアント。</li><li>例: `red`</li></ul> </li><li>**評価平均** <ul><li>アイテムの平均評価。</li></ul> </li><li>**評価数** <ul><li>アイテムの評価数。</li></ul> </li><li>**評価最大** <ul><li>アイテムの最大可能評価。</li><li>例: `5.0` が最高評価の5つ星の場合。</li></ul> </li><li>**作成タイムスタンプ** <ul><li>コンテンツが作成された時間。</li></ul> </li><li>**有効期限** <ul><li>このコンテンツが有効でなくなる最後の時間。</li><li>`Null` / は制限なしを意味します。</li><li>ほとんど構成されるべきではありません。</li></ul> </li><li>**状態** <ul><li>オークションの場合、アイテムが新品、良好、許容可能などの状態。</li><li>次のいずれか:  <ul><li>`OTHER`</li><li>`NEW`</li><li>`EXCELLENT`</li><li>`GOOD`</li><li>`FAIR`</li><li>`POOR`</li><li>`USED`</li><li>`REFURBISHED`</li></ul> </li></ul> </li><li>**キーワード** <ul><li>キーワード。</li></ul> </li><li>**画像キャプション** <ul><li>カンマ区切りの値の文字列。</li><li>画像に関連するキャプション。</li></ul> </li><li>**緯度** <ul><li>レストラン、ビジネス、部屋（ホテル）などの緯度。</li></ul> </li><li>**経度** <ul><li>レストラン、ビジネス、部屋（ホテル）などの経度。</li></ul> </li><li>**郵便番号** <ul><li>レストラン、ビジネス、部屋（ホテル）などの郵便/郵便番号。</li></ul> </li><li>**国** <ul><li>レストラン、ビジネス、部屋（ホテル）などの国コード。</li></ul> </li><li>**地域** <ul><li>レストラン、ビジネス、部屋（ホテル）などの州または地域。</li></ul> </li><li>**市** <ul><li>レストラン、ビジネス、部屋（ホテル）などの市。</li></ul> </li><li>**通り** <ul><li>レストラン、ビジネス、部屋（ホテル）などの通り住所。</li></ul> </li><li>**カスタムフィールド** <ul><li>アプリ開発者がコンテンツアイテムに添付したいキー値ペア。</li></ul> </li></ul> </li></ul> |

### アクション - ライフサイクルイベントの記録
#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントタイプ|  <ul><li>(必須) コマースイベントのタイプを選択してください。</li></ul> |
|OSタイプ|  <ul><li>(必須) モバイルデバイスのオペレーティングシステムのタイプを選択してください。</li></ul> |
|デバイスID|  <ul><li>(必須) 1つまたは2つのデバイスIDを指定してください。</li><li>OSタイプによって異なるIDを選択できます。</li></ul> |
|ユーザーデータ|  <ul> <ul><li>(オプション) 必要に応じて多くのデバイス識別パラメータを指定してください：</li> <ul><li>**OSバージョン** <ul><li>数値</li><li>オペレーティングシステムのバージョン。</li><li>AndroidおよびiOSに特有です。</li></ul> </li><li>**環境** <ul><li>文字列</li><li>通常は `FULL_APP` です。</li></ul> </li><li>**ユーザーエージェント** <ul><li>文字列</li><li>イベントが発生したブラウザまたはアプリのユーザーエージェント。</li></ul> </li><li>**HTTPオリジン** <ul><li>文字列</li><li>Web SDKがWebセッション開始を記録した現在のページのURL。</li></ul> </li><li>**HTTPリファラー** <ul><li>文字列</li><li>Web SDKがWebセッション開始を記録した現在のページにつながる参照URL。</li></ul> </li><li>**ローカルIP** <ul><li>文字列</li><li>デバイスのローカルIP（Androidのみ）。</li></ul> </li><li>**国** <ul><li>文字列</li><li>通常、デバイスの構成またはユーザーエージェント文字列に基づいたユーザーの国コード。</li></ul> </li><li>**言語** <ul><li>文字列</li><li>通常、デバイスの構成またはユーザーエージェント文字列に基づいたユーザーの言語コード。</li></ul> </li><li>**ブランド** <ul><li>文字列</li><li>デバイスのブランド。</li></ul> </li><li>**モデル** <ul><li>文字列</li><li>デバイスのモデル。</li></ul> </li><li>**アプリバージョン** <ul><li>文字列</li><li>ユーザーがダウンロードしたアプリのバージョン。</li></ul> </li><li>**スクリーンDPI** <ul><li>数値</li><li>スクリーンDPI。</li></ul> </li><li>**スクリーンの高さ** <ul><li>数値</li><li>スクリーンの高さ。</li></ul> </li><li>**スクリーンの幅** <ul><li>数値</li><li>スクリーンの幅。</li></ul> </li><li>**開発者ID** <ul><li>文字列</li><li>ユーザーに対して開発者が指定したID。</li></ul> </li><li>**デバイスフィンガープリントID** <ul><li>Branch内部専用のデバイス追跡フィールド。</li></ul> </li><li>**ブラウザフィンガープリントID** <ul><li>Branch内部専用のブラウザ追跡フィールド。</li></ul> </li><li>**広告追跡制限** <ul><li>パートナーが広告主による追跡を拒否した場合、値は `True` です。</li></ul> </li></ul> </ul> </ul> <ul> <ul> <ul><li>**デバイスIP** <ul><li>イベントが発生したデバイスのIPアドレス。</li><li>この値にクライアントIP属性をマッピングします。**この属性は推奨されます。**</li></ul> </li></ul> </ul> </ul> |
|イベントデータ|  <ul><li>(オプション) イベントに特有のデータ。</li><li>説明: 文字列、イベントに関連する説明で、必ずしも個々のコンテンツアイテムに特有ではありません。</li></ul> |
|カスタムデータ|  <ul><li>(オプション) 任意のプロパティ名と値で追加データを指定してください。</li></ul> |

### アクション - カスタムイベントの記録

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントタイプ|  <ul><li>(必須) コマースイベントのタイプを選択してください。</li></ul> |
|OSタイプ|  <ul><li>(必須) モバイルデバイスのオペレーティングシステムのタイプを選択してください。</li></ul> |
|デバイスID|  <ul><li>(必須) 1つまたは2つのデバイスIDを指定してください。</li><li>OSタイプによって異なるIDを選択できます。</li></ul> |
|ユーザーデータ|  <ul><li>(オプション) 必要に応じて多くのデバイス識別パラメータを指定してください：</li> <ul><li>**OSバージョン** <ul><li>数値</li><li>オペレーティングシステムのバージョン。</li><li>AndroidおよびiOSに特有です。</li></ul> </li><li>**環境** <ul><li>文字列</li><li>通常は `FULL_APP` です。</li></ul> </li><li>**ユーザーエージェント** <ul><li>文字列</li><li>イベントが発生したブラウザまたはアプリのユーザーエージェント。</li></ul> </li><li>**HTTPオリジン** <ul><li>文字列</li><li>Web SDKがWebセッション開始を記録した現在のページのURL。</li></ul> </li><li>**HTTPリファラー** <ul><li>文字列</li><li>Web SDKがWebセッション開始を記録した現在のページにつながる参照URL。</li></ul> </li><li>**ローカルIP** <ul><li>文字列</li><li>デバイスのローカルIP（Androidのみ）。</li></ul> </li><li>**国** <ul><li>文字列</li><li>通常、デバイスの構成またはユーザーエージェント文字列に基づいたユーザーの国コード。</li></ul> </li><li>**言語** <ul><li>文字列</li><li>通常、デバイスの構成またはユーザーエージェント文字列に基づいたユーザーの言語コード。</li></ul> </li><li>**ブランド** <ul><li>文字列</li><li>デバイスのブランド。</li></ul> </li><li>**モデル** <ul><li>文字列</li><li>デバイスのモデル。</li></ul> </li><li>**アプリバージョン** <ul><li>文字列</li><li>ユーザーがダウンロードしたアプリのバージョン。</li></ul> </li><li>**スクリーンDPI** <ul><li>数値</li><li>スクリーンDPI。</li></ul> </li><li>**スクリーンの高さ** <ul><li>数値,</li><li>スクリーンの高さ。</li></ul> </li><li>**スクリーンの幅** <ul><li>数値</li><li>スクリーンの幅。</li></ul> </li><li>**開発者ID** <ul><li>文字列</li><li>ユーザーに対して開発者が指定したID。</li></ul> </li><li>**デバイスフィンガープリントID** <ul><li>Branch内部専用のデバイス追跡フィールド。</li></ul> </li><li>**ブラウザフィンガープリントID** <ul><li>Branch内部専用のブラウザ追跡フィールド。</li></ul> </li><li>**広告追跡制限** <ul><li>パートナーが広告主による追跡を拒否した場合、値は `True` です。</li></ul> </li><li>**デバイスIP** <ul><li>イベントが発生したデバイスのIPアドレス。</li><li>この値にクライアントIP属性をマッピングします。**この属性は推奨されます。**</li></ul> </li></ul> </ul> |
|カスタムデータ|  <ul><li>(オプション) 任意のプロパティ名と値で追加データを指定してください。</li></ul> |

#### ベンダー文書

* [Branch Docs: Events](https://docs.branch.io/apps/v2event/)
* [Branch API: Logging Commerce, Content, Lifecycle and Custom Events](https://github.com/BranchMetrics/branch-deep-linking-public-api#logging-commerce-events "TGest")