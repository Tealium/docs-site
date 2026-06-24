---
title: Braze Web SDK タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Braze Web SDK タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/braze-web-sdk-tag/
---
## サポートされているバージョン

* 6.8
* 5.5
* 4.8
* 3.5

Braze Web SDK タグは、タグテンプレートバージョン 3.3 およびそれ以前をサポートしています。最適なタグのパフォーマンスと機能性を得るために、最新のタグテンプレートに更新することをお勧めします。

## タグのヒント

* 注文IDが存在する場合に購入イベントが発火します。
* 以下の E-Commerce 拡張パラメータをサポートしています：
  * 顧客ID（`_ccustid`を上書き）
  * 市区町村（`_ccity`を上書き）
  * 国（`_ccountry`を上書き）
  * 注文ID（`_corder`を上書き）
  * 小計（`_csubtotal`を上書き）
  * 通貨（`_ccurrency`を上書き）
  * 製品ID（`_cprod`を上書き）
  * 製品数量（`_cquan`を上書き）

* 標準構成値を動的に上書きするためにマッピングを使用します。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグを追加する方法についての詳細は、[タグの管理]()を参照してください。

タグを追加した後、以下の構成を構成します：

* **コードバージョン**
  * 使用したい Braze Web SDK のメジャー.マイナーバージョンを入力します。
  * 例えば、バージョン 4.8.1 をデプロイする場合は、4.8 を入力します。
  * コードバージョン 4.0 以降は Internet Explorer をサポートしていません。
  * Braze Web SDK の最新バージョンについては、[変更履歴](https://github.com/Appboy/appboy-web-sdk/blob/master/CHANGELOG.md)を参照してください。

* **API キー**
  * Braze ダッシュボードの **アプリグループ管理** 構成で利用可能なユニークな API キー。

* **ベース URL**
  * 割り当てられた Braze クラスターを指す API エンドポイント。
  * 4.0 の例：`https://js.appboycdn.com/web-sdk/4.0/braze.no-amd.min.js`
  * 3.5 およびそれ以前のバージョンの例：`https://js.appboycdn.com/web-sdk/3.5/appboy.no-amd.min.js`
  * オプションのリストについては、[Braze SDK エンドポイント](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints/)を参照してください。

* **ログの有効化**
  * 有効にすると、ウェブコンソールにデバッグ情報が記録されます。

## ロードルール

[ロードルール]()は、サイト上でこのタグのインスタンスをいつ、どこでロードするかを決定します。

## データマッピング

マッピングは、[データレイヤー変数](/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。([詳細を学ぶ](/ja/iq-tag-management/data-mappings/manage/))

Braze Web SDK タグの宛先変数は、タグのデータマッピングタブに組み込まれています。以下の表は、利用可能な宛先カテゴリをリストし、各宛先名を説明しています。
### 標準

| **目的地名**              | **説明**                                                                                                                                                                                                        |
|:----------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `api_key`                                | &lt;ul&gt;&lt;li&gt;APIキー&lt;/li&gt;&lt;li&gt;「Manage App Group」構成の下にあるBrazeダッシュボードで利用可能なユニークなAPIキー。&lt;/li&gt;&lt;/ul&gt;                                                                         |
| `code_version`                           | &lt;ul&gt;&lt;li&gt;コードバージョン&lt;/li&gt;&lt;li&gt;Braze Web SDKをロードするメジャー.マイナーバージョン。&lt;/li&gt;&lt;li&gt;例えば、最新の6.8.xリリースをデプロイするには&lt;code&gt;6.8&lt;/code&gt;と入力します。&lt;/li&gt;&lt;/ul&gt;                                     |
| `initOpt.allow_crawler`           | &lt;ul&gt;&lt;li&gt;クローラーを許可&lt;/li&gt;&lt;li&gt;ウェブクローラーからのすべてのアクティビティをBrazeに記録させる。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                                |
| `initOpt.app_ver`                 | &lt;ul&gt;&lt;li&gt;アプリバージョン&lt;/li&gt;&lt;li&gt;データを関連付けるアプリのバージョン。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                  |
| `initOpt.base_url`                | &lt;ul&gt;&lt;li&gt;ベースURL&lt;/li&gt;&lt;li&gt;Brazeが提供するカスタムエンドポイントへの完全なURL。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                    |
| `initOpt.no_cookies`              | &lt;ul&gt;&lt;li&gt;クッキーなし&lt;/li&gt;&lt;li&gt;Brazeがユーザー情報をクッキーに保存するのを防ぐ。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                                    |
| `initOpt.no_fntawsm`              | &lt;ul&gt;&lt;li&gt;フォントアウェサムなし&lt;/li&gt;&lt;li&gt;Brazeが `FontAwesome` をロードするのを防ぐ。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                                             |
| `initOpt.enable_htmlmsgs`         | &lt;ul&gt;&lt;li&gt;メッセージ内のHTMLを有効にする&lt;/li&gt;&lt;li&gt;Brazeユーザーがアプリ内メッセージを通じてHTMLを送信できるようにする。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                           |
| `initOpt.enable_logging`          | &lt;ul&gt;&lt;li&gt;ログを有効にする&lt;/li&gt;&lt;li&gt;ウェブコンソールにBrazeのエラーメッセージを表示させる。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                              |
| `initOpt.localization`            | &lt;ul&gt;&lt;li&gt;ローカリゼーション&lt;/li&gt;&lt;li&gt;ブラウザのデフォルト言語を上書きするISO 639-1言語コード。&lt;/li&gt;&lt;/ul&gt;                                                                                                       |
| `initOpt.min_trggrinterval`       | &lt;ul&gt;&lt;li&gt;アクション間の最小間隔&lt;/li&gt;&lt;li&gt;別のトリガーアクションが発生するまでの時間（秒）。&lt;/li&gt;&lt;li&gt;デフォルト値は `30`。&lt;/li&gt;&lt;/ul&gt;                                                               |
| `initOpt.msg_innewtab`            | &lt;ul&gt;&lt;li&gt;新しいタブでアプリ内メッセージを開く&lt;/li&gt;&lt;li&gt;アプリ内メッセージのリンクを新しいタブまたはウィンドウで開くように強制する。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                            |
| `initOpt.card_innewtab`           | &lt;ul&gt;&lt;li&gt;新しいタブでニュースフィードカードを開く&lt;/li&gt;&lt;li&gt;ニュースフィードカードのリンクを新しいタブまたはウィンドウで開くように強制する。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                            |
| `initOpt.explicit_dissmisal`      | &lt;ul&gt;&lt;li&gt;明示的な解除を要求する&lt;/li&gt;&lt;li&gt;ユーザーがメッセージを解除するためにボタンをクリックすることを強制する。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                                          |
| `initOpt.safari_pushid`           | &lt;ul&gt;&lt;li&gt;SafariウェブサイトプッシュID&lt;/li&gt;&lt;li&gt;Safariプッシュ証明書からのID。&lt;/li&gt;&lt;/ul&gt;                                                                                                                             |
| `initOpt.srvcewrkr_location`      | &lt;ul&gt;&lt;li&gt;サービスワーカーの場所&lt;/li&gt;&lt;li&gt;ルートディレクトリにない場合の`service-worker.js`ファイルへのパス。&lt;/li&gt;&lt;/ul&gt;                                                                                            |
| `initOpt.session_timeout`         | &lt;ul&gt;&lt;li&gt;セッションタイムアウト&lt;/li&gt;&lt;li&gt;セッションがタイムアウトするまでの時間（分）。&lt;/li&gt;&lt;li&gt;デフォルト値は `30`。&lt;/li&gt;&lt;/ul&gt;                                                                                            |
| `initOpt.devicePropertyAllowlist`        | &lt;ul&gt;&lt;li&gt;デバイスプロパティ許可リスト&lt;/li&gt;&lt;li&gt;収集するデバイスプロパティの配列。&lt;/li&gt;&lt;li&gt;リストにないプロパティは収集から除外されます。&lt;/li&gt;&lt;/ul&gt;                                                  |
| `initOpt.enableSdkAuthentication`        | &lt;ul&gt;&lt;li&gt;SDK認証を有効にする&lt;/li&gt;&lt;li&gt;Brazeサーバーへのネットワークリクエストに現在のユーザーの最後に知られているJSONウェブトークンを追加する。&lt;/li&gt;&lt;li&gt;この構成はバージョン3.5以降で利用可能です。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
| `initOpt.sdk_auth_signature`             | &lt;ul&gt;&lt;li&gt;SDK認証署名&lt;/li&gt;&lt;li&gt;SDK認証が有効な場合にSDKリクエストを認証するために使用されるJSONウェブトークン。&lt;/li&gt;&lt;li&gt;この構成はバージョン3.5以降で利用可能です。&lt;/li&gt;&lt;/ul&gt;    |
| `initOpt.allow_user_supplied_javascript` | &lt;ul&gt;&lt;li&gt;ユーザー提供のJavaScriptを許可する&lt;/li&gt;&lt;li&gt;アプリ内メッセージでユーザー提供のJavaScriptの実行を許可する。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                       |
| `initOpt.content_security_nonce`         | &lt;ul&gt;&lt;li&gt;コンテンツセキュリティNonce&lt;/li&gt;&lt;li&gt;コンテンツセキュリティポリシーの準拠のためにBraze SDKスクリプトタグに含めるべきnonce文字列。&lt;/li&gt;&lt;/ul&gt;                                                                      |
| `initOpt.disable_push_token_maintenance` | &lt;ul&gt;&lt;li&gt;プッシュトークンメンテナンスを無効にする&lt;/li&gt;&lt;li&gt;セッション開始時の自動プッシュトークンリフレッシュを無効にする。&lt;/li&gt;&lt;li&gt;オプションは `true` または `false`。&lt;/li&gt;&lt;/ul&gt;                                                          |
| `initOpt.in_app_message_zindex`          | &lt;ul&gt;&lt;li&gt;アプリ内メッセージZindex&lt;/li&gt;&lt;li&gt;アプリ内メッセージオーバーレイのデフォルトz-indexを上書きする。&lt;/li&gt;&lt;/ul&gt;                                                                                                    |

### E-コマース

Braze Web SDKタグはE-コマース対応であり、デフォルトのE-コマース拡張マッピングを自動的に使用します。このカテゴリで手動でマッピングする必要は通常ありませんが、拡張マッピングを上書きしたい場合や、拡張に提供されていないE-コマース変数がある場合は必要です。

| **目的地名** | **説明**                                                                 |
|:---------------------|:--------------------------------------------------------------------------------|
| `order_id`           | &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt;                         |
| `order_subtotal`     | &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt;                     |
| `order_currency`     | &lt;ul&gt;&lt;li&gt;通貨&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt;                      |
| `customer_id`        | &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;`_ccustid`を上書きします。&lt;/li&gt;&lt;/ul&gt;                     |
| `customer_city`      | &lt;ul&gt;&lt;li&gt;顧客の市&lt;/li&gt;&lt;li&gt;`_ccity`を上書きします。&lt;/li&gt;&lt;/ul&gt;                     |
| `customer_country`   | &lt;ul&gt;&lt;li&gt;顧客の国&lt;/li&gt;&lt;li&gt;`_ccountry`を上書きします。&lt;/li&gt;&lt;/ul&gt;               |
| `product_id`         | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品IDのリスト&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `product_quantity`   | &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt;  |
### イベント

特定のイベントをページでトリガーするためにこれらの目的地にマッピングします。

イベントをトリガーするには、以下の手順を使用します：

1. ドロップダウンリストからイベントを選択します。
  * 事前定義されたリストから選択するか、カスタムイベントを作成できます。
  * カスタムイベントの場合、それを識別する名前を入力します。

1. **トリガー** フィールドにマッピングされる変数の値を入力します。
1. より多くのイベントをマッピングするには、**&#43;** ボタンをクリックして手順1と2を繰り返します。
1. **適用**をクリックします。

以下の表は、データレイヤーで指定された値が見つかったときにイベントトリガーをリストしています。

| **目的地名**     | **説明**                                                                                                                                                     |
|:-------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Purchase`               | &lt;ul&gt;&lt;li&gt;購入ログ&lt;/li&gt;&lt;li&gt;現在のユーザーによるアプリ内購入が行われます。&lt;/li&gt;&lt;li&gt;注文IDが存在する場合、購入イベントは自動的に構成されます。&lt;/li&gt;&lt;/ul&gt; |
| `Alias`                  | &lt;ul&gt;&lt;li&gt;ユーザーエイリアスの追加&lt;/li&gt;&lt;li&gt;現在のユーザーの新しいエイリアスが追加されます。&lt;/li&gt;&lt;/ul&gt;                                                                                 |
| `addToSubscriptionGroup` | &lt;ul&gt;&lt;li&gt;メールまたはSMSのサブスクリプショングループにユーザーを追加します。&lt;/li&gt;&lt;li&gt;この構成はバージョン3.5以降で利用可能です。&lt;/li&gt;&lt;/ul&gt;                                  |
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
| `SetCity`                | &lt;ul&gt;&lt;li&gt;ホームシティの構成&lt;/li&gt;&lt;li&gt;現在のユーザーの都市を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                         |
| `SetCountry`             | &lt;ul&gt;&lt;li&gt;国の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの国を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                        |
| `SetLang`                | &lt;ul&gt;&lt;li&gt;言語の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの言語を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                      |
| `SetPhone`               | &lt;ul&gt;&lt;li&gt;電話番号の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの電話番号を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                              |
| `SetGender`              | &lt;ul&gt;&lt;li&gt;性別の構成&lt;/li&gt;&lt;li&gt;現在のユーザーの性別を構成します。&lt;/li&gt;&lt;/ul&gt;                                                                                          |
| `removeFromSubscriptionGroup` | &lt;ul&gt;&lt;li&gt;サブスクリプショングループから削除&lt;/li&gt;&lt;li&gt;メールまたはSMSのサブスクリプショングループから現在のユーザーを削除します。&lt;/li&gt;&lt;li&gt;この構成はバージョン3.5以降で利用可能です。&lt;/li&gt;&lt;/ul&gt; |
| `setCustomLocationAttribute` | &lt;ul&gt;&lt;li&gt;カスタム位置属性の構成&lt;/li&gt;&lt;li&gt;現在のユーザーのカスタム位置属性（キー、緯度、経度）を構成します。&lt;/li&gt;&lt;/ul&gt;                          |
| `SetLineId`              | &lt;ul&gt;&lt;li&gt;LINE IDの構成&lt;/li&gt;&lt;li&gt;現在のユーザーのLINEメッセージングアプリIDを構成します。&lt;/li&gt;&lt;/ul&gt;                                                                          |
| `Ecommerce`              | &lt;ul&gt;&lt;li&gt;イーコマースイベントのログ&lt;/li&gt;&lt;li&gt;現在のユーザーの構造化されたイーコマースイベントをログします。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt; |
| `WipeData`               | &lt;ul&gt;&lt;li&gt;データのワイプ（ローカルSDKデータの削除）&lt;/li&gt;&lt;li&gt;ローカルに保存されたすべてのSDKデータを削除し、SDKを無効にします。&lt;/li&gt;&lt;li&gt;さらなるデータ収集を再開する前に、SDKを明示的に再有効化する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `RefreshFeatureFlags`    | &lt;ul&gt;&lt;li&gt;フィーチャーフラグの更新&lt;/li&gt;&lt;li&gt;Brazeから現在のユーザーのフィーチャーフラグを更新するよう要求します。&lt;/li&gt;&lt;/ul&gt;                                                |
| `LogFeatureFlagImpression` | &lt;ul&gt;&lt;li&gt;フィーチャーフラグインプレッションのログ&lt;/li&gt;&lt;li&gt;指定されたフィーチャーフラグのインプレッションイベントをログします。&lt;/li&gt;&lt;/ul&gt;                                                    |
| `RefreshContentCards`    | &lt;ul&gt;&lt;li&gt;コンテンツカードの更新&lt;/li&gt;&lt;li&gt;Brazeからコンテンツカードフィードを更新するよう要求します。&lt;/li&gt;&lt;/ul&gt;                                                            |
| `ShowContentCards`       | &lt;ul&gt;&lt;li&gt;コンテンツカードの表示&lt;/li&gt;&lt;li&gt;コンテンツカードフィードを表示します。&lt;/li&gt;&lt;/ul&gt;                                                                                       |
| `LogContentCardImpressions` | &lt;ul&gt;&lt;li&gt;コンテンツカードインプレッションのログ&lt;/li&gt;&lt;li&gt;コンテンツカードの配列のインプレッションイベントをログします。&lt;/li&gt;&lt;/ul&gt;                                                     |
| `LogContentCardClick`    | &lt;ul&gt;&lt;li&gt;コンテンツカードクリックのログ&lt;/li&gt;&lt;li&gt;特定のコンテンツカードのクリックイベントをログします。&lt;/li&gt;&lt;/ul&gt;                                                                    |
| `RequestPushPermission`  | &lt;ul&gt;&lt;li&gt;プッシュ通知の許可を要求&lt;/li&gt;&lt;li&gt;ユーザーにプッシュ通知の許可を求めます。&lt;/li&gt;&lt;/ul&gt;                                                           |
| `UnregisterPush`         | &lt;ul&gt;&lt;li&gt;プッシュの登録解除&lt;/li&gt;&lt;li&gt;現在のデバイスをプッシュ通知から登録解除します。&lt;/li&gt;&lt;/ul&gt;                                                                   |
| `FlushData`              | &lt;ul&gt;&lt;li&gt;データのフラッシュ&lt;/li&gt;&lt;li&gt;キューに入れられた分析データを直ちにBrazeサーバーに送信します。&lt;/li&gt;&lt;/ul&gt;                                                                      |
| `RefreshBanners`         | &lt;ul&gt;&lt;li&gt;バナーの更新&lt;/li&gt;&lt;li&gt;指定された配置IDのBrazeバナーを更新するよう要求します。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt; |
| `LogBannerImpressions`   | &lt;ul&gt;&lt;li&gt;バナーインプレッションのログ&lt;/li&gt;&lt;li&gt;バナー配置IDの配列のインプレッションイベントをログします。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt; |
| `LogBannerClick`         | &lt;ul&gt;&lt;li&gt;バナークリックを記録&lt;/li&gt;&lt;li&gt;特定のバナーのクリックイベントを記録します。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt;                  |
| `InsertBanner`           | &lt;ul&gt;&lt;li&gt;バナーを挿入&lt;/li&gt;&lt;li&gt;指定された配置IDのバナーを取得し、指定された親要素に挿入します。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt; |
| `Custom`                 | &lt;ul&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;li&gt;現在のユーザーによって作成されたカスタムイベントを送信します。&lt;/li&gt;&lt;/ul&gt;                                                                                     |
### パラメータ

これらの目的地にデータをマッピングして、以前にマッピングされたイベントにデータを渡します。パラメータは事前定義されたイベントでのみ使用されます。カスタムイベントでパラメータを渡す方法については、以下のカスタムイベントデータセクションを参照してください。

事前定義されたイベントにパラメータを渡すには、次の手順を使用します：

1. イベントフィールドで、ドロップダウンリストからイベントを選択します。
1. パラメータフィールドで、ドロップダウンリストからパラメータを選択します。
1. カスタムパラメータの場合、カスタムイベントを識別する名前を入力します。
1. **&#43; 追加**をクリックします。

| **目的地名**  | **説明**                                                                                                                                                                                                                                    |
|:----------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `product_id`          | &lt;ul&gt;&lt;li&gt;商品ID&lt;/li&gt;&lt;li&gt;アプリ内で購入された商品のユニークID。&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                   |
| `product_quantity`    | &lt;ul&gt;&lt;li&gt;商品数量&lt;/li&gt;&lt;li&gt;アプリ内で購入された商品の数量。&lt;/li&gt;&lt;li&gt;これはeコマース値`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                     |
| `order_id`            | &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;アプリ内購入のユニークID。&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                             |
| `order_subtotal`      | &lt;ul&gt;&lt;li&gt;注文小計&lt;/li&gt;&lt;li&gt;アプリ内購入の小計。&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                     |
| `order_currency`      | &lt;ul&gt;&lt;li&gt;注文通貨&lt;/li&gt;&lt;li&gt;アプリ内購入のISO 4217通貨コード。&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt;                                                                                                                        |
| `purchase_properties` | &lt;ul&gt;&lt;li&gt;購入プロパティ&lt;/li&gt;&lt;li&gt;アプリ内購入の追加プロパティのオブジェクト。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                          |
| `alias`               | &lt;ul&gt;&lt;li&gt;ユーザーエイリアス&lt;/li&gt;&lt;li&gt;現在のユーザーの識別子。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                           |
| `label`               | &lt;ul&gt;&lt;li&gt;エイリアスラベル&lt;/li&gt;&lt;li&gt;エイリアスのソースなど、エイリアスのラベル。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                      |
| `key`                 | &lt;ul&gt;&lt;li&gt;カスタム属性キー&lt;/li&gt;&lt;li&gt;カスタム属性の識別子。&lt;/li&gt;&lt;li&gt;送信するパラメータの名前を入力します。&lt;/li&gt;&lt;/ul&gt;                                                                                                           |
| `value`               | &lt;ul&gt;&lt;li&gt;カスタム属性値&lt;/li&gt;&lt;li&gt;カスタム属性の値。&lt;/li&gt;&lt;li&gt;送信するパラメータの名前を入力します。&lt;/li&gt;&lt;/ul&gt;                                                                                                              |
| `inc_value`           | &lt;ul&gt;&lt;li&gt;カスタム属性増分値&lt;/li&gt;&lt;li&gt;カスタムユーザー属性を増分する値。&lt;/li&gt;&lt;li&gt;送信するパラメータの名前を入力します。&lt;/li&gt;&lt;li&gt;減少させるには負の数を使用します。&lt;/li&gt;&lt;li&gt;デフォルト値は`1`です。&lt;/li&gt;&lt;/ul&gt; |
| `custom_attributes`   | &lt;ul&gt;&lt;li&gt;カスタム属性オブジェクト&lt;/li&gt;&lt;li&gt;現在のユーザーに一度に構成するカスタム属性キー値ペアのオブジェクト。&lt;/li&gt;&lt;/ul&gt;                                                                                                       |
| `line_id`             | &lt;ul&gt;&lt;li&gt;ユーザーのLINE ID&lt;/li&gt;&lt;li&gt;現在のユーザーのLINEメッセージングアプリID。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                          |
| `feature_flag_id`     | &lt;ul&gt;&lt;li&gt;フィーチャーフラグID&lt;/li&gt;&lt;li&gt;印象を記録するためのフィーチャーフラグのユニーク識別子。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                     |
| `banner_placement_ids` | &lt;ul&gt;&lt;li&gt;バナー配置ID（配列またはコンマ区切り）&lt;/li&gt;&lt;li&gt;バナー配置IDの配列またはコンマ区切りの文字列で、リフレッシュまたは印象を記録します。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt;            |
| `banner_placement_id` | &lt;ul&gt;&lt;li&gt;バナー配置ID&lt;/li&gt;&lt;li&gt;単一のバナー配置のユニーク識別子で、取得して挿入します。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt;                                                           |
| `banner_click_id`     | &lt;ul&gt;&lt;li&gt;バナークリックID&lt;/li&gt;&lt;li&gt;クリックされたバナーのクリック追跡ID。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt;                                                                                     |
| `banner_parent_selector` | &lt;ul&gt;&lt;li&gt;バナーペアレントセレクタ（CSS）&lt;/li&gt;&lt;li&gt;バナーが挿入される親要素を識別するCSSセレクタ文字列。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt;                                   |
| `content_cards`       | &lt;ul&gt;&lt;li&gt;コンテンツカード配列&lt;/li&gt;&lt;li&gt;印象を記録するためのコンテンツカードオブジェクトの配列。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                            |
| `content_card`        | &lt;ul&gt;&lt;li&gt;コンテンツカードオブジェクト&lt;/li&gt;&lt;li&gt;クリックを記録するための単一のコンテンツカードオブジェクト。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                    |
| `ecommerce_event_name` | &lt;ul&gt;&lt;li&gt;イーコマースイベント名&lt;/li&gt;&lt;li&gt;記録するイーコマースイベントの名前。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt;                                                                                             |
| `ecommerce_properties` | &lt;ul&gt;&lt;li&gt;イーコマースプロパティ&lt;/li&gt;&lt;li&gt;イーコマースイベントのプロパティのオブジェクト。&lt;/li&gt;&lt;li&gt;&lt;code&gt;source&lt;/code&gt;フィールドをサポートし、デフォルトは&lt;code&gt;&#34;tealium&#34;&lt;/code&gt;です。&lt;/li&gt;&lt;li&gt;この構成はバージョン6.0以降で利用可能です。&lt;/li&gt;&lt;/ul&gt; |
| `avatar_url`          | &lt;ul&gt;&lt;li&gt;アバター画像URL&lt;/li&gt;&lt;li&gt;現在のユーザーが選択したアバターのURL。&lt;/li&gt;&lt;li&gt;バージョン4.0以降では利用不可です。&lt;/li&gt;&lt;/ul&gt;                                                                                                           |
| `longitude`           | &lt;ul&gt;&lt;li&gt;ユーザーの経度&lt;/li&gt;&lt;li&gt;ユーザーの位置の検証済み経度、度単位。&lt;/li&gt;&lt;li&gt;値は`-180`から`180`です&lt;/li&gt;&lt;/ul&gt;                                                                                                     |
| `latitude`            | &lt;ul&gt;&lt;li&gt;ユーザーの緯度&lt;/li&gt;&lt;li&gt;ユーザーの位置の検証済み緯度、度単位。&lt;/li&gt;&lt;li&gt;値は`-90`から`90`です&lt;/li&gt;&lt;/ul&gt;                                                                                                         |
| `accuracy`            | &lt;ul&gt;&lt;li&gt;位置精度&lt;/li&gt;&lt;li&gt;ユーザーの経度と緯度の精度、メートル単位。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                          |
| `altitude`            | &lt;ul&gt;&lt;li&gt;ユーザーの高度&lt;/li&gt;&lt;li&gt;ユーザーの位置の高度（メートル単位）。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                          |
| `altitude_accuracy`   | &lt;ul&gt;&lt;li&gt;高度の精度&lt;/li&gt;&lt;li&gt;ユーザーの高度の精度（メートル単位）。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                        |
| `year`                | &lt;ul&gt;&lt;li&gt;ユーザーの生年&lt;/li&gt;&lt;li&gt;現在のユーザーの誕生日に関連する年。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                  |
| `month`               | &lt;ul&gt;&lt;li&gt;ユーザーの誕生月&lt;/li&gt;&lt;li&gt;現在のユーザーの誕生日に関連する月。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                |
| `day`                 | &lt;ul&gt;&lt;li&gt;ユーザーの誕生日&lt;/li&gt;&lt;li&gt;現在のユーザーの誕生日に関連する日。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                    |
| `email`               | &lt;ul&gt;&lt;li&gt;ユーザーのメールアドレス&lt;/li&gt;&lt;li&gt;現在のユーザーの検証済みメールアドレス。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                            |
| `notification_type`   | &lt;ul&gt;&lt;li&gt;通知の種類&lt;/li&gt;&lt;li&gt;現在のユーザーの選択された通知タイプ。&lt;/li&gt;&lt;li&gt;オプション: `opted_in`, `subscribed`, `unsubscribed`&lt;/li&gt;&lt;/ul&gt;                                                                                |
| `first_name`          | &lt;ul&gt;&lt;li&gt;ユーザーの名前&lt;/li&gt;&lt;li&gt;現在のユーザーの名前。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                    |
| `subscriptionGroupId` | &lt;ul&gt;&lt;li&gt;サブスクリプショングループID&lt;/li&gt;&lt;li&gt;サブスクリプショングループの一意の識別子。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                  |
| `last_name`           | &lt;ul&gt;&lt;li&gt;ユーザーの姓&lt;/li&gt;&lt;li&gt;現在のユーザーの姓。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                      |
| `gender`              | &lt;ul&gt;&lt;li&gt;ユーザーの性別&lt;/li&gt;&lt;li&gt;現在のユーザーの性別コード。&lt;/li&gt;&lt;li&gt;オプションは男性 (`m`), 女性 (`f`), その他 `o`。&lt;/li&gt;&lt;/ul&gt;                                                                                                              |
| `customer_city`       | &lt;ul&gt;&lt;li&gt;ユーザーの居住都市&lt;/li&gt;&lt;li&gt;現在のユーザーの居住都市。&lt;/li&gt;&lt;li&gt;`_ccity`を上書き。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                          |
| `customer_country`    | &lt;ul&gt;&lt;li&gt;ユーザーの国&lt;/li&gt;&lt;li&gt;現在のユーザーの国。&lt;/li&gt;&lt;li&gt;`_ccountry`を上書き。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                           |
| `localization`        | &lt;ul&gt;&lt;li&gt;ユーザーの言語&lt;/li&gt;&lt;li&gt;現在のユーザーの表示言語のISO 639-1言語コード。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                     |
| `phone_number`        | &lt;ul&gt;&lt;li&gt;ユーザーの電話番号&lt;/li&gt;&lt;li&gt;現在のユーザーの電話番号。&lt;/li&gt;&lt;li&gt;数字、スペース、`&#43;`, `.`, `-`, ` ( `, `)` の文字のみ許可&lt;/li&gt;&lt;/ul&gt;                                                                         |

### カスタムイベントデータ

イベントタブで以前にマッピングしたカスタムイベントにカスタムパラメータを渡したい場合、カスタムイベントデータの目的地にマップします。

カスタムイベントデータ変数をマッピングするには、以下の手順に従ってください：

1. **イベント名**に、**イベント**タブで指定されたカスタムイベントの名前を入力します。
1. **パラメータ**に、送信したいパラメータの名前を入力します。
1. **&#43; 追加**をクリックします。

### クッキー同意

ユーザーの同意状態に基づいてBraze SDKが有効または無効になるように、クッキー同意の目的地にマップします。同意ゲーティングはSDKの初期化前に実行されます。

| **値** | **説明**                                                                                          |
|:----------|:---------------------------------------------------------------------------------------------------------|
| `grant`   | SDKを有効にし、データ収集を進めます。SDKは初期化され、セッションが通常通り開始されます。 |
| `revoke`  | 初期化前にSDKを無効にします。データは収集されず、セッションは開始されません。                   |

## ベンダー文書

* [Braze Web SDK](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/initial_sdk_setup/)