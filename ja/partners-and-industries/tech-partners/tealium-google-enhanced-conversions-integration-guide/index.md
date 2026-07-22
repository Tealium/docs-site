---
title: Tealium + Google Enhanced Conversions 統合ガイド
description: この記事では、iQタグ管理のGoogle Ads Conversion Tracking＆Remarketing（gtag.js）タグとEventStream API HubのGoogle Ads Enhanced Conversions for Webコネクタを構成することで、TealiumとGoogle Ads Enhanced Conversionを最大限に活用する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-google-enhanced-conversions-integration-guide/
---
TealiumとGoogle Ads Enhanced Conversions for Webの組み合わせは、同意した第一者データを活用して以下を実現し、広告のコンバージョンを保持し改善します：

* ブラウザの制限に対応する。
* 広告ブロッカーを回避する。
* プライバシーと同意要件を遵守する。

このソリューションの成功した実装は、コンバージョン率に以下のようなポジティブな影響をもたらしました：

* 検索：平均3.5％のコンバージョン率の増加（範囲：1-5％）
* YouTube：平均12％の広告コンバージョン率の増加（範囲：7-25％）

## 前提条件

* Tealium
    * iQタグ管理：[Google Ads Conversion and Remarketing（gtag.js）タグ](https://docs.tealium.com/google-ads-conversion-tracking-and-remarketing-gtagjs-tag/)または[Floodlight（gtag.js）タグ](https://docs.tealium.com/floodlight-gtagjs-tag/)
    * EventStream：[Google Ads Enhanced Conversions for Webコネクタ](https://docs.tealium.com/google-ads-enhanced-conversions-for-web-connector/)
* Google
    * Enhanced Conversionsが有効なコンバージョンを持つGoogle Adsアカウント。詳細については、[Google Ads APIのウェブ向けエンリッチメントコンバージョンについて](https://support.google.com/google-ads/answer/13261987?visit_id=638313598805594644-2275068296&rd=1)を参照してください。

## 仕組み

このハイブリッドソリューションは、クライアントサイドのタグとサーバーサイドのAPIを使用して、顧客データとコンバージョンイベント（例：サブスクリプション、サインアップ、購入）をGoogleに送信します。顧客データは、サインインしたGoogleユーザーとマッチングされ、コンバージョンイベントは広告クリックまたはビューに帰属されます。顧客データは、SHA256と呼ばれる一方向ハッシュアルゴリズムを使用して保護され、安全でプライベートに保たれます。

![](https://docs.tealium.com/images/tech-partners/tealium-google-ads-enhanced-conversions-flow.png)

エンリッチメントコンバージョンは、以下の顧客属性の1つ以上が利用可能な場合にのみ機能します：

* メールアドレス（推奨）
* 氏名と自宅の住所
* 電話番号（他のいずれかと組み合わせる必要があります）

## 顧客データ

以下の顧客パラメータが必要です。クライアントサイドのタグはこれらの値を正規化しますが、iQの拡張機能やEventStreamのエンリッチメントを使用してこれらの値を正規化する必要があります。

|データフィールド| 説明|
|---| ---|
|メールアドレス| 小文字にし、Gmailアドレスの場合はすべてのピリオドを削除します。<br> 例：`janedoe@gmail.com`|
|電話番号| 記号とダッシュを削除し、国コードを保持します。<br> 例：`14155551212`|
|名前| ユーザーの名前。<br> 例：`Jane`|
|姓| ユーザーの姓。<br> 例：`Doe`|
|住所| ユーザーの住所。<br> 例：`123 Main St`|
|市区町村| ユーザーの市区町村名。<br> 例：`San Diego`|
|地域| ユーザーの地域、州、または県。<br> 例：`CA`または`California`|
|郵便番号| ユーザーの郵便番号（5、6、または7桁版）。<br> 例：`92121`または`S099 9XX`|
|国| ユーザーの国コード、ISO 3155-1標準。<br> 例：`US`または`UK`|

## コンバージョンデータ

以下のGoogleコンバージョンパラメータがタグに必要です：

|データフィールド| 説明|
|---| ---|
|コンバージョンID| コンバージョンの一意のトラッキングID。|
|コンバージョンラベル| エンコードされたコンバージョントラッキングIDとコンバージョンタイプ。 |
|コンバージョン値| トランザクション固有の値またはこのコンバージョンタイプに使用される値。<br> [Google Adsヘルプ：コンバージョン値について](https://support.google.com/google-ads/answer/3419241?hl=en)を参照してください。|
| 注文ID | E-Commerce拡張機能からの注文IDまたはトランザクションID、または直接マッピングされたもの。 |

以下のGoogleコンバージョンパラメータがコネクタに必要です：

|**パラメータ**| **説明**|
|---| ---|
| コンバージョンアクション| Google Ads UIで構成されたコンバージョンアクション。 |
| トランザクションID| 広告主としてあなたが生成した、コンバージョンイベントを一意に識別するID。クライアントサイドのイベントと同じ値を持つべきです。 |
| コンバージョン値| コンバージョンの金額。 |
| コンバージョン通貨| コンバージョンの通貨コード。 |
| コンバージョン時間| 元のコンバージョンが発生した日時。 |

## クライアントサイドのウェブサイトトラッキングタグ

iQタグ管理でGoogle Ads Conversion and Remarketingタグを構成するには、以下が必要です：

* トラッキングするコンバージョンイベントを識別するロードルール。
* Google Adsのコンバージョン構成、特にコンバージョントラッキングIDとコンバージョンラベル。

以下の手順は、[Google Ads Conversion Tracking＆Remarketing（gtag.js）タグ構成ガイド](https://docs.tealium.com/google-ads-conversion-tracking-and-remarketing-gtagjs-tag/)で詳しく説明されています。

### タグ構成

Tealiumのtag marketplaceにアクセスし、Google Ads Conversion＆Remarketing（`gtag.js`）タグを追加します。

### ロードルール

コンバージョンイベントに一致するロードルールを構成します。これは、コンバージョンが発生するページまたはコンバージョンを表すイベントである可能性があります。

ロードルールの例には以下のようなものがあります：

* **購入** - `tealium_event EQUALS "purchase"`
* **サインアップ** - `tealium_event EQUALS "newsletter_signup"`

### データマッピング

タグを追加した後、**Data Mappings**セクションに移動して、追加のマッピングを構成します。

E-Commerce拡張機能を使用している場合、以下のマッピングは自動的に行われます：

* 注文小計/コンバージョン値
* 注文通貨/コンバージョン通貨
* 注文ID/トランザクションID

## サーバーサイドコネクタ

EventStreamでGoogle Ads Enhanced Conversions for Webコネクタを構成するには、以下が必要です：

* トラッキングするコンバージョンイベントを識別するイベントフィード。
* Google Adsのコンバージョン構成。

以下の手順は、[Google Ads Enhanced Conversions for Webコネクタ構成ガイド](https://docs.tealium.com/google-ads-enhanced-conversions-for-web-connector/)で詳しく説明されています。

### コネクタの追加

コネクタマーケットプレイスにアクセスし、Google Ads Enhanced Conversions for WebコネクタのEventStreamアクションを追加します。


<blockquote>
このコネクタを構成するには、Tealium Customer Data HubとGoogle Adsアカウント間の接続を確立しますので、コネクタを構成する前にGoogleアカウントにログインしておくと便利です。
</blockquote>


次に、以下を構成します：

* **データソース** - コンバージョンイベントが発生するウェブサイトを表すデータソースを選択します。
* **イベントフィード** - トラッキングするコンバージョンイベントのみを含むフィードを選択します。

Googleアカウントとの接続を確立し、**Send Conversion**アクションタイプを選択します。

### データマッピング

**Send Conversion**アクションは、コンバージョンイベントをエンリッチメントコンバージョンのためのGoogleサーバーサイドAPIに送信します。

エンリッチメントコンバージョンAPI呼び出しには、以下のデータマッピングが必要です：

* **トランザクションID** - 広告主としてあなたが生成した、コンバージョンイベントを一意に識別するID。購入イベントの場合、これは注文IDです。

以下の顧客データマッピングのうち、少なくとも1つが必要です：

* **メールアドレス** - コンバージョン時点のユーザーのメールアドレス。**または**
* **氏名と住所**（名前、姓、住所、市区町村、地域、郵便番号、国）
すべてのフィールドを提供する必要があります。

電話番号は、どちらのオプションでも提供できるオプションの値です。


<blockquote>
EventStreamコネクタはプレーンテキストマッピングを許可し、SHA-256ハッシュが適用されます。
</blockquote>


## Google Enhanced Conversions

Google Enhanced Conversionsについては、以下の点を注意してください：

* **Gclid**  
Gclidはオプションで、アトリビューション、レポーティング、または入札には使用されません。
* **ユーザーエージェント**  
ユーザーエージェントはウェブコンバージョンに必要で、同一デバイスとクロスデバイスのコンバージョンを別々に報告することができます。

現時点では、以下のコンバージョンイベントは対象外です：

* モバイルアプリのコンバージョン（インストール、アプリ内アクションなど）
* 電話によるコンバージョン
* インポート/オフラインコンバージョン

## 追加のリソース

* [Better Together: Tealium + Google](https://tealium.com/google-integrations/)
* [Google Ads Help: About enhanced conversions (beta)](https://support.google.com/google-ads/answer/9888656?hl=en&amp;ref_topic=3165803)


