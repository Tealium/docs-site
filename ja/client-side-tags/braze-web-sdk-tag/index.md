---
title: Braze Web SDK タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Braze Web SDK タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/braze-web-sdk-tag/
---
## サポートされているバージョン

* 3.5
* 4.0

Braze Web SDK タグは、タグテンプレートバージョン 3.3 およびそれ以前をサポートしています。最高のタグパフォーマンスと機能性を得るために、最新のタグテンプレートへの更新をお勧めします。

## タグのヒント

* 注文IDが存在する場合、購入イベントが発火します。
* 以下の E-Commerce 拡張パラメータをサポートしています：
  * 顧客ID（`_ccustid`を上書き）
  * 市区町村（`_ccity`を上書き）
  * 国（`_ccountry`を上書き）
  * 注文ID（`_corder`を上書き）
  * 小計（`_csubtotal`を上書き）
  * 通貨（`_ccurrency`を上書き）
  * 商品ID（`_cprod`を上書き）
  * 商品数量（`_cquan`を上書き）

* 標準構成値を動的に上書きするためにマッピングを使用します。

## タグ構成

まず、Tealiumの**タグマーケットプレイス**にアクセスし、プロファイルにBraze Web SDKタグを追加します（[タグの追加方法?]()）。

タグを追加した後、以下の構成を構成します：

* **コードバージョン**
  * 使用したいBraze Web SDKのメジャー.マイナーバージョンを入力します。
  * 例えば、バージョン2.6.1をデプロイする場合は、2.6と入力します。
  * Braze Web SDKの最新バージョンは、[changelog](https://github.com/Appboy/appboy-web-sdk/blob/master/CHANGELOG.md)を参照してください。

* **APIキー**
  * Brazeダッシュボードの**アプリグループ管理**構成で利用可能なユニークなAPIキー。

* **ベースURL**
  * 割り当てられたBrazeクラスターを指すAPIエンドポイント。
  * 4.0の例：`https://js.appboycdn.com/web-sdk/4.0/braze.no-amd.min.js`
  * 3.5およびそれ以前のバージョンの例：`https://js.appboycdn.com/web-sdk/3.5/appboy.no-amd.min.js`
  * オプションのリストについては、[Braze SDK Endpoints](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints/)を参照してください。

* **ログの有効化**
  * 有効にすると、ウェブコンソールにデバッグ情報が記録されます。

## ロードルール

[ロードルール]()は、このタグのインスタンスをサイトのどこに、いつロードするかを決定します。

## データマッピング

マッピングは、[データレイヤー変数](/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。（[詳細を学ぶ](/ja/iq-tag-management/data-mappings/manage/)）

Braze Web SDKタグの宛先変数は、タグのデータマッピングタブに組み込まれています。以下の表は、利用可能な宛先カテゴリをリストし、各宛先名を説明しています。

### 標準

| **宛先名**              | **説明**                                                                                                                                                                                                        |
|:----------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `initOpt.allow_crawler`           | &lt;ul&gt;&lt;li&gt;クローラーを許可&lt;/li&gt;&lt;li&gt;Brazeによってウェブクローラーの活動が記録されます。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                                |
| `initOpt.app_ver`                 | &lt;ul&gt;&lt;li&gt;アプリバージョン&lt;/li&gt;&lt;li&gt;データを関連付けるアプリのバージョン。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                  |
| `initOpt.base_url`                | &lt;ul&gt;&lt;li&gt;ベースURL&lt;/li&gt;&lt;li&gt;Brazeが提供するカスタムエンドポイントへの完全なURL。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                    |
| `initOpt.no_cookies`              | &lt;ul&gt;&lt;li&gt;クッキーなし&lt;/li&gt;&lt;li&gt;Brazeがユーザー情報をクッキーに保存するのを防ぎます。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                                    |
| `initOpt.no_fntawsm`              | &lt;ul&gt;&lt;li&gt;フォントアウェサムなし&lt;/li&gt;&lt;li&gt;Brazeが `FontAwesome` をロードするのを防ぎます。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                                             |
| `initOpt.enable_htmlmsgs`         | &lt;ul&gt;&lt;li&gt;メッセージ内のHTMLを有効化&lt;/li&gt;&lt;li&gt;Brazeユーザーがアプリ内メッセージを介してHTMLを送信できるようにします。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                           |
| `initOpt.enable_logging`          | &lt;ul&gt;&lt;li&gt;ログの有効化&lt;/li&gt;&lt;li&gt;ウェブコンソールにBrazeのエラーメッセージが表示されることを許可します。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                              |
| `initOpt.localization`            | &lt;ul&gt;&lt;li&gt;ローカリゼーション&lt;/li&gt;&lt;li&gt;ブラウザのデフォルト言語を上書きするISO 639-1言語コード。&lt;/li&gt;&lt;/ul&gt;                                                                                                       |
| `initOpt.min_trggrinterval`       | &lt;ul&gt;&lt;li&gt;アクション間の最小間隔&lt;/li&gt;&lt;li&gt;別のトリガーアクションが発生するまでの時間（秒単位）。&lt;/li&gt;&lt;li&gt;デフォルト値は `30`。&lt;/li&gt;&lt;/ul&gt;                                                               |
| `initOpt.msg_innewtab`            | &lt;ul&gt;&lt;li&gt;新しいタブでアプリ内メッセージを開く&lt;/li&gt;&lt;li&gt;アプリ内メッセージのリンクを新しいタブまたはウィンドウで開くように強制します。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                            |
| `initOpt.card_innewtab`           | &lt;ul&gt;&lt;li&gt;新しいタブでニュースフィードカードを開く&lt;/li&gt;&lt;li&gt;ニュースフィードカードのリンクを新しいタブまたはウィンドウで開くように強制します。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                            |
| `initOpt.explicit_dissmisal`      | &lt;ul&gt;&lt;li&gt;明示的な解除を要求&lt;/li&gt;&lt;li&gt;ユーザーがメッセージを解除するためにボタンをクリックすることを強制します。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                          |
| `initOpt.safari_pushid`           | &lt;ul&gt;&lt;li&gt;SafariウェブサイトプッシュID&lt;/li&gt;&lt;li&gt;Safariプッシュ証明書からのID。&lt;/li&gt;&lt;/ul&gt;                                                                                                                             |
| `initOpt.srvcewrkr_location`      | &lt;ul&gt;&lt;li&gt;サービスワーカーの場所&lt;/li&gt;&lt;li&gt;ルートディレクトリにない場合の `service-worker.js` ファイルへのパス。&lt;/li&gt;&lt;/ul&gt;                                                                                            |
| `initOpt.session_timeout`         | &lt;ul&gt;&lt;li&gt;セッションタイムアウト&lt;/li&gt;&lt;li&gt;セッションがタイムアウトするまでの時間（分単位）。デフォルト値は `30`。&lt;/li&gt;&lt;/ul&gt;                                                                                            |
| `initOpt.enableSdkAuthentication` | &lt;ul&gt;&lt;li&gt;現在のユーザーの最後に知られているJSONウェブトークンをBrazeサーバーへのネットワークリクエストに追加します。&lt;/li&gt;&lt;li&gt;この構成はバージョン3.5以降で利用可能です。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |


### Eコマース

Braze Web SDKタグはEコマース対応であり、デフォルトのEコマース拡張マッピングを自動的に使用します。このカテゴリで手動でマッピングする必要は通常ありませんが、拡張マッピングを上書きするか、Eコマース変数が拡張に提供されていない場合は必要になることがあります。

| **宛先名** | **説明** |
|:---------------------|:--------------------------------------------------------------------------------|
| `order_id`           | &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt;                         |
| `order_subtotal`     | &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt;                     |
| `order_currency`     | &lt;ul&gt;&lt;li&gt;通貨&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt;                      |
| `customer_id`        | &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書きします。&lt;/li&gt;&lt;/ul&gt;                     |
| `customer_city`      | &lt;ul&gt;&lt;li&gt;顧客の市&lt;/li&gt;&lt;li&gt;`_ccity`を上書きします。&lt;/li&gt;&lt;/ul&gt;                     |
| `customer_country`   | &lt;ul&gt;&lt;li&gt;顧客の国&lt;/li&gt;&lt;li&gt;`_ccountry`を上書きします。&lt;/li&gt;&lt;/ul&gt;               |
| `product_id`         | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;商品IDのリスト&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `product_quantity`   | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt;  |

### イベント

ページ上で特定のイベントをトリガーするためにこれらの宛先にマップします。

イベントをトリガーするには、以下の手順を使用します：

1. ドロップダウンリストからイベントを選択します。
  * 事前定義されたリストから選択するか、カスタムイベントを作成できます。
  * カスタムイベントの場合、それを識別する名前を入力します。

1. **トリガー**フィールドにマッピングされる変数の値を入力します。
1. より多くのイベントをマップするには、**&#43;**ボタンをクリックして手順1と2を繰り返します。
1. **適用**をクリックします。

次の表は、データレイヤーに提供された値が見つかったときにイベントトリガーをリストします。

| **宛先名**     | **説明**                                                                                                                                                     |
|:-------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Purchase`               | &lt;ul&gt;&lt;li&gt;購入ログ&lt;/li&gt;&lt;li&gt;現在のユーザーによってアプリ内購入が行われます。&lt;/li&gt;&lt;li&gt;注文IDが存在する場合、購入イベントは自動的に構成されます。&lt;/li&gt;&lt;/ul&gt; |
| `Alias`                  | &lt;ul&gt;&lt;li&gt;ユーザーエイリアスの追加&lt;/li&gt;&lt;li&gt;現在のユーザーの新しいエイリアスが追加されます。&lt;/li&gt;&lt;/ul&gt;                                                                                 |
| `addToSubscriptionGroup` | &lt;ul&gt;&lt;li&gt;ユーザーをメールまたはSMSのサブスクリプショングループに追加します。&lt;/li&gt;&lt;li&gt;この構成はバージョン3.5以降で利用可能です。&lt;/li&gt;&lt;/ul&gt;                                  |
| `AddAtt`                 | &lt;ul&gt;&lt;li&gt;カスタム属性を配列に追加&lt;/li&gt;&lt;li&gt;カスタム属性配列に新しい属性が追加されます。&lt;/li&gt;&lt;/ul&gt;                                                     |
| `IncAtt`                 | &lt;ul&gt;&lt;li&gt;カスタム属性のインクリメント&lt;/li&gt;&lt;li&gt;現在のカスタム属性配列にある属性を増やします。&lt;/li&gt;&lt;/ul&gt;                                               |
| `RmvAtt`                 | &lt;ul&gt;&lt;li&gt;カスタム属性を配列から削除&lt;/li&gt;&lt;li&gt;カスタム属性配列から属性を削除します。&lt;/li&gt;&lt;/ul&gt;                                                  |
| `SetAtt`                 | &lt;ul&gt;&lt;li&gt;ユーザー属性の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの新しいカスタム属性を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                      |
| `SetAvatar`              | &lt;ul&gt;&lt;li&gt;アバターの構成&lt;/li&gt;&lt;li&gt;現在のユーザーのアバターURLを構成します。&lt;/li&gt;&lt;li&gt;バージョン4.0以降では利用できません。&lt;/li&gt;&lt;/ul&gt;                                    |
| `SetLoc`                 | &lt;ul&gt;&lt;li&gt;最後の位置の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの最後に知られている位置を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                       |
| `SetDOB`                 | &lt;ul&gt;&lt;li&gt;生年月日の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの生年月日（日、月、年）を構成します。&lt;/li&gt;&lt;/ul&gt;                                                             |
| `SetEmail`               | &lt;ul&gt;&lt;li&gt;メールの構成&lt;/li&gt;&lt;li&gt;現在のユーザーのメールを構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                            |
| `SetEmailSub`            | &lt;ul&gt;&lt;li&gt;メールサブスクリプションタイプの構成&lt;/li&gt;&lt;li&gt;現在のユーザーのメールサブスクリプションの通知タイプを構成します。&lt;/li&gt;&lt;/ul&gt;                                       |
| `SetPushSub`             | &lt;ul&gt;&lt;li&gt;プッシュサブスクリプションタイプの構成&lt;/li&gt;&lt;li&gt;現在のユーザーのプッシュ通知の通知タイプを構成します。&lt;/li&gt;&lt;/ul&gt;                                        |
| `SetFirst`               | &lt;ul&gt;&lt;li&gt;名の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの名を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                  |
| `SetLast`                | &lt;ul&gt;&lt;li&gt;姓の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの姓を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                    |
| `SetCity`                | &lt;ul&gt;&lt;li&gt;ホームシティの構成&lt;/li&gt;&lt;li&gt;現在のユーザーの市を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                         |
| `SetCountry`             | &lt;ul&gt;&lt;li&gt;国の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの国を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                        |
| `SetLang`                | &lt;ul&gt;&lt;li&gt;言語の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの言語を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                      |
| `SetPhone`               | &lt;ul&gt;&lt;li&gt;電話番号の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの電話番号を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                              |
| `SetGender`              | &lt;ul&gt;&lt;li&gt;性別の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの性別を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                          |
| `Custom`                 | &lt;ul&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;li&gt;現在のユーザーによって作成されたカスタムイベントを送信します。&lt;/li&gt;&lt;/ul&gt;                                                                 |
### パラメータ

これらの目的地にマッピングして、以前にマッピングしたイベントにデータを渡します。パラメータは事前定義されたイベントでのみ使用されます。カスタムイベントでパラメータを渡す方法については、以下のカスタムイベントデータセクションを参照してください。

事前定義されたイベントにパラメータを渡すには、以下の手順を使用します：

1. イベントフィールドで、ドロップダウンリストからイベントを選択します。
1. パラメータフィールドで、ドロップダウンリストからパラメータを選択します。
1. カスタムパラメータの場合、カスタムイベントを識別する名前を入力します。
1. **&#43; 追加**をクリックします。

| **目的地名**  | **説明**                                                                                                                                                                                                                                    |
|:----------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `product_id`          | &lt;ul&gt;&lt;li&gt;商品ID&lt;/li&gt;&lt;li&gt;アプリ内で購入された商品のユニークID。&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                   |
| `product_quantity`    | &lt;ul&gt;&lt;li&gt;商品数量&lt;/li&gt;&lt;li&gt;アプリ内で購入された商品の数量。&lt;/li&gt;&lt;li&gt;これはeコマースの値`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                     |
| `order_id`            | &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;アプリ内購入のユニークID。&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                             |
| `order_subtotal`      | &lt;ul&gt;&lt;li&gt;注文小計&lt;/li&gt;&lt;li&gt;アプリ内購入の小計。&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                     |
| `order_currency`      | &lt;ul&gt;&lt;li&gt;注文通貨&lt;/li&gt;&lt;li&gt;アプリ内購入のISO 4217通貨コード。&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                        |
| `purchase_properties` | &lt;ul&gt;&lt;li&gt;購入プロパティ&lt;/li&gt;&lt;li&gt;アプリ内購入の追加プロパティのオブジェクト。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                          |
| `alias`               | &lt;ul&gt;&lt;li&gt;ユーザーエイリアス&lt;/li&gt;&lt;li&gt;現在のユーザーの識別子。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                           |
| `label`               | &lt;ul&gt;&lt;li&gt;エイリアスラベル&lt;/li&gt;&lt;li&gt;エイリアスのソースなど、エイリアスのラベル。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                      |
| `key`                 | &lt;ul&gt;&lt;li&gt;カスタム属性キー&lt;/li&gt;&lt;li&gt;カスタム属性の識別子。&lt;/li&gt;&lt;li&gt;送信するパラメータの名前を入力します。&lt;/li&gt;&lt;/ul&gt;                                                                                                           |
| `value`               | &lt;ul&gt;&lt;li&gt;カスタム属性値&lt;/li&gt;&lt;li&gt;カスタム属性の値。&lt;/li&gt;&lt;li&gt;送信するパラメータの名前を入力します。&lt;/li&gt;&lt;/ul&gt;                                                                                                              |
| `inc_value`           | &lt;ul&gt;&lt;li&gt;カスタム属性増分値&lt;/li&gt;&lt;li&gt;カスタムユーザー属性を増分する値。&lt;/li&gt;&lt;li&gt;送信するパラメータの名前を入力します。&lt;/li&gt;&lt;li&gt;減少させるには負の数を使用します。&lt;/li&gt;&lt;li&gt;デフォルト値は`1`です。&lt;/li&gt;&lt;/ul&gt; |
| `avatar_url`          | &lt;ul&gt;&lt;li&gt;アバター画像URL&lt;/li&gt;&lt;li&gt;現在のユーザーが選択したアバターのURL。&lt;/li&gt;&lt;li&gt;バージョン4.0以降では利用できません。&lt;/li&gt;&lt;/ul&gt;                                                                                                           |
| `longitude`           | &lt;ul&gt;&lt;li&gt;ユーザーの経度&lt;/li&gt;&lt;li&gt;ユーザーの位置の検証済み経度、度単位。&lt;/li&gt;&lt;li&gt;値は`-180`から`180`までです&lt;/li&gt;&lt;/ul&gt;                                                                                                     |
| `latitude`            | &lt;ul&gt;&lt;li&gt;ユーザーの緯度&lt;/li&gt;&lt;li&gt;ユーザーの位置の検証済み緯度、度単位。&lt;/li&gt;&lt;li&gt;値は`-90`から`90`までです&lt;/li&gt;&lt;/ul&gt;                                                                                                         |
| `accuracy`            | &lt;ul&gt;&lt;li&gt;位置精度&lt;/li&gt;&lt;li&gt;ユーザーの経度と緯度の精度、メートル単位。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                          |
| `altitude`            | &lt;ul&gt;&lt;li&gt;ユーザーの高度&lt;/li&gt;&lt;li&gt;ユーザーの位置の高度、メートル単位。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                          |
| `altitude_accuracy`   | &lt;ul&gt;&lt;li&gt;高度精度&lt;/li&gt;&lt;li&gt;ユーザーの高度の精度、メートル単位。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                        |
| `year`                | &lt;ul&gt;&lt;li&gt;ユーザーの誕生年&lt;/li&gt;&lt;li&gt;現在のユーザーの誕生日に関連する年。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                  |
| `month`               | &lt;ul&gt;&lt;li&gt;ユーザーの誕生月&lt;/li&gt;&lt;li&gt;現在のユーザーの誕生日に関連する月。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                |
| `day`                 | &lt;ul&gt;&lt;li&gt;ユーザーの誕生日&lt;/li&gt;&lt;li&gt;現在のユーザーの誕生日に関連する日。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                    |
| `email`               | &lt;ul&gt;&lt;li&gt;ユーザーのメール&lt;/li&gt;&lt;li&gt;現在のユーザーの検証済みメールアドレス。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                            |
| `notification_type`   | &lt;ul&gt;&lt;li&gt;通知購読タイプ&lt;/li&gt;&lt;li&gt;現在のユーザーの選択された通知タイプ。&lt;/li&gt;&lt;li&gt;オプション: `opted_in`, `subscribed`, `unsubscribed`&lt;/li&gt;&lt;/ul&gt;                                                                                |
| `first_name`          | &lt;ul&gt;&lt;li&gt;ユーザーの名前&lt;/li&gt;&lt;li&gt;現在のユーザーの名前。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                    |
| `subscriptionGroupId` | &lt;ul&gt;&lt;li&gt;サブスクリプショングループID。&lt;/li&gt;&lt;li&gt;サブスクリプショングループのユニークな識別子。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                  |
| `last_name`           | &lt;ul&gt;&lt;li&gt;ユーザーの姓&lt;/li&gt;&lt;li&gt;現在のユーザーの姓。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                      |
| `gender`              | &lt;ul&gt;&lt;li&gt;ユーザーの性別&lt;/li&gt;&lt;li&gt;現在のユーザーの性別コード。&lt;/li&gt;&lt;li&gt;オプションは男性(`m`)、女性(`f`)、その他(`o`)です。&lt;/li&gt;&lt;/ul&gt;                                                                                                              |
| `customer_city`       | &lt;ul&gt;&lt;li&gt;ユーザーの居住都市&lt;/li&gt;&lt;li&gt;現在のユーザーの居住都市。&lt;/li&gt;&lt;li&gt;`_ccity`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                          |
| `customer_country`    | &lt;ul&gt;&lt;li&gt;ユーザーの国&lt;/li&gt;&lt;li&gt;現在のユーザーの国。&lt;/li&gt;&lt;li&gt;`_ccountry`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                           |
| `localization`        | &lt;ul&gt;&lt;li&gt;ユーザーの言語&lt;/li&gt;&lt;li&gt;現在のユーザーの表示言語のISO 639-1言語コード。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                     |
| `phone_number`        | &lt;ul&gt;&lt;li&gt;ユーザーの電話番号&lt;/li&gt;&lt;li&gt;現在のユーザーの電話番号。&lt;/li&gt;&lt;li&gt;数字、スペース、`&#43;`、`.`、`-`、`(`、`)`の文字のみ許可されます&lt;/li&gt;&lt;/ul&gt;                                                                         |

### カスタムイベントデータ

イベントタブで以前にマッピングしたカスタムイベントにカスタムパラメータを渡したい場合、カスタムイベントデータの送信先にマップします。

カスタムイベントデータ変数をマップするには、以下の手順に従ってください：

1. **イベント名**に、**イベント**タブで指定されたカスタムイベントの名前を正確に入力します。
1. **パラメータ**に、送信したいパラメータの名前を入力します。
1. **&#43; 追加**をクリックします。

## ベンダー文書

* [Braze Web SDK](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/initial_sdk_setup/)

