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


<blockquote>
Braze Web SDK タグは、タグテンプレートバージョン 3.3 およびそれ以前をサポートしています。最適なタグのパフォーマンスと機能性を得るために、最新のタグテンプレートに更新することをお勧めします。
</blockquote>


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

タグマーケットプレイスにアクセスして新しいタグを追加します。タグを追加する方法についての詳細は、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

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

[ロードルール](https://docs.tealium.com/about-load-rules/)は、サイト上でこのタグのインスタンスをいつ、どこでロードするかを決定します。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。([詳細を学ぶ](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/))

Braze Web SDK タグの宛先変数は、タグのデータマッピングタブに組み込まれています。以下の表は、利用可能な宛先カテゴリをリストし、各宛先名を説明しています。
### 標準

| **目的地名**              | **説明**                                                                                                                                                                                                        |
|:----------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `api_key`                                | <ul><li>APIキー</li><li>「Manage App Group」構成の下にあるBrazeダッシュボードで利用可能なユニークなAPIキー。</li></ul>                                                                         |
| `code_version`                           | <ul><li>コードバージョン</li><li>Braze Web SDKをロードするメジャー.マイナーバージョン。</li><li>例えば、最新の6.8.xリリースをデプロイするには<code>6.8</code>と入力します。</li></ul>                                     |
| `initOpt.allow_crawler`           | <ul><li>クローラーを許可</li><li>ウェブクローラーからのすべてのアクティビティをBrazeに記録させる。</li><li>オプションは `true` または `false`。</li></ul>                                                                                |
| `initOpt.app_ver`                 | <ul><li>アプリバージョン</li><li>データを関連付けるアプリのバージョン。</li></ul>                                                                                                                                  |
| `initOpt.base_url`                | <ul><li>ベースURL</li><li>Brazeが提供するカスタムエンドポイントへの完全なURL。</li></ul>                                                                                                                                    |
| `initOpt.no_cookies`              | <ul><li>クッキーなし</li><li>Brazeがユーザー情報をクッキーに保存するのを防ぐ。</li><li>オプションは `true` または `false`。</li></ul>                                                                                    |
| `initOpt.no_fntawsm`              | <ul><li>フォントアウェサムなし</li><li>Brazeが `FontAwesome` をロードするのを防ぐ。</li><li>オプションは `true` または `false`。</li></ul>                                                                                             |
| `initOpt.enable_htmlmsgs`         | <ul><li>メッセージ内のHTMLを有効にする</li><li>Brazeユーザーがアプリ内メッセージを通じてHTMLを送信できるようにする。</li><li>オプションは `true` または `false`。</li></ul>                                                                           |
| `initOpt.enable_logging`          | <ul><li>ログを有効にする</li><li>ウェブコンソールにBrazeのエラーメッセージを表示させる。</li><li>オプションは `true` または `false`。</li></ul>                                                                              |
| `initOpt.localization`            | <ul><li>ローカリゼーション</li><li>ブラウザのデフォルト言語を上書きするISO 639-1言語コード。</li></ul>                                                                                                       |
| `initOpt.min_trggrinterval`       | <ul><li>アクション間の最小間隔</li><li>別のトリガーアクションが発生するまでの時間（秒）。</li><li>デフォルト値は `30`。</li></ul>                                                               |
| `initOpt.msg_innewtab`            | <ul><li>新しいタブでアプリ内メッセージを開く</li><li>アプリ内メッセージのリンクを新しいタブまたはウィンドウで開くように強制する。</li><li>オプションは `true` または `false`。</li></ul>                                                            |
| `initOpt.card_innewtab`           | <ul><li>新しいタブでニュースフィードカードを開く</li><li>ニュースフィードカードのリンクを新しいタブまたはウィンドウで開くように強制する。</li><li>オプションは `true` または `false`。</li></ul>                                                            |
| `initOpt.explicit_dissmisal`      | <ul><li>明示的な解除を要求する</li><li>ユーザーがメッセージを解除するためにボタンをクリックすることを強制する。</li><li>オプションは `true` または `false`。</li></ul>                                                                          |
| `initOpt.safari_pushid`           | <ul><li>SafariウェブサイトプッシュID</li><li>Safariプッシュ証明書からのID。</li></ul>                                                                                                                             |
| `initOpt.srvcewrkr_location`      | <ul><li>サービスワーカーの場所</li><li>ルートディレクトリにない場合の`service-worker.js`ファイルへのパス。</li></ul>                                                                                            |
| `initOpt.session_timeout`         | <ul><li>セッションタイムアウト</li><li>セッションがタイムアウトするまでの時間（分）。</li><li>デフォルト値は `30`。</li></ul>                                                                                            |
| `initOpt.devicePropertyAllowlist`        | <ul><li>デバイスプロパティ許可リスト</li><li>収集するデバイスプロパティの配列。</li><li>リストにないプロパティは収集から除外されます。</li></ul>                                                  |
| `initOpt.enableSdkAuthentication`        | <ul><li>SDK認証を有効にする</li><li>Brazeサーバーへのネットワークリクエストに現在のユーザーの最後に知られているJSONウェブトークンを追加する。</li><li>この構成はバージョン3.5以降で利用可能です。</li><li>オプションは `true` または `false`。</li></ul> |
| `initOpt.sdk_auth_signature`             | <ul><li>SDK認証署名</li><li>SDK認証が有効な場合にSDKリクエストを認証するために使用されるJSONウェブトークン。</li><li>この構成はバージョン3.5以降で利用可能です。</li></ul>    |
| `initOpt.allow_user_supplied_javascript` | <ul><li>ユーザー提供のJavaScriptを許可する</li><li>アプリ内メッセージでユーザー提供のJavaScriptの実行を許可する。</li><li>オプションは `true` または `false`。</li></ul>                                                       |
| `initOpt.content_security_nonce`         | <ul><li>コンテンツセキュリティNonce</li><li>コンテンツセキュリティポリシーの準拠のためにBraze SDKスクリプトタグに含めるべきnonce文字列。</li></ul>                                                                      |
| `initOpt.disable_push_token_maintenance` | <ul><li>プッシュトークンメンテナンスを無効にする</li><li>セッション開始時の自動プッシュトークンリフレッシュを無効にする。</li><li>オプションは `true` または `false`。</li></ul>                                                          |
| `initOpt.in_app_message_zindex`          | <ul><li>アプリ内メッセージZindex</li><li>アプリ内メッセージオーバーレイのデフォルトz-indexを上書きする。</li></ul>                                                                                                    |

### E-コマース

Braze Web SDKタグはE-コマース対応であり、デフォルトのE-コマース拡張マッピングを自動的に使用します。このカテゴリで手動でマッピングする必要は通常ありませんが、拡張マッピングを上書きしたい場合や、拡張に提供されていないE-コマース変数がある場合は必要です。

| **目的地名** | **説明**                                                                 |
|:---------------------|:--------------------------------------------------------------------------------|
| `order_id`           | <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul>                         |
| `order_subtotal`     | <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul>                     |
| `order_currency`     | <ul><li>通貨</li><li>`_ccurrency`を上書きします。</li></ul>                      |
| `customer_id`        | <ul><li>顧客ID</li><li>`_ccustid`を上書きします。</li></ul>                     |
| `customer_city`      | <ul><li>顧客の市</li><li>`_ccity`を上書きします。</li></ul>                     |
| `customer_country`   | <ul><li>顧客の国</li><li>`_ccountry`を上書きします。</li></ul>               |
| `product_id`         | <ul><li>配列</li><li>製品IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
| `product_quantity`   | <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul>  |
### イベント

特定のイベントをページでトリガーするためにこれらの目的地にマッピングします。

イベントをトリガーするには、以下の手順を使用します：

1. ドロップダウンリストからイベントを選択します。
  * 事前定義されたリストから選択するか、カスタムイベントを作成できます。
  * カスタムイベントの場合、それを識別する名前を入力します。

1. **トリガー** フィールドにマッピングされる変数の値を入力します。
1. より多くのイベントをマッピングするには、**+** ボタンをクリックして手順1と2を繰り返します。
1. **適用**をクリックします。

以下の表は、データレイヤーで指定された値が見つかったときにイベントトリガーをリストしています。

| **目的地名**     | **説明**                                                                                                                                                     |
|:-------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Purchase`               | <ul><li>購入ログ</li><li>現在のユーザーによるアプリ内購入が行われます。</li><li>注文IDが存在する場合、購入イベントは自動的に構成されます。</li></ul> |
| `Alias`                  | <ul><li>ユーザーエイリアスの追加</li><li>現在のユーザーの新しいエイリアスが追加されます。</li></ul>                                                                                 |
| `addToSubscriptionGroup` | <ul><li>メールまたはSMSのサブスクリプショングループにユーザーを追加します。</li><li>この構成はバージョン3.5以降で利用可能です。</li></ul>                                  |
| `AddAtt`                 | <ul><li>カスタム属性を配列に追加</li><li>カスタム属性配列に新しい属性が追加されます。</li></ul>                                                     |
| `IncAtt`                 | <ul><li>カスタム属性のインクリメント</li><li>現在のカスタム属性配列にある属性を増やします。</li></ul>                                               |
| `RmvAtt`                 | <ul><li>カスタム属性を配列から削除</li><li>カスタム属性配列から属性を削除します。</li></ul>                                                  |
| `SetAtt`                 | <ul><li>ユーザー属性の構成</li><li>現在のユーザーの新しいカスタム属性を構成します。</li></ul>                                                                      |
| `SetAvatar`              | <ul><li>アバターの構成</li><li>現在のユーザーのアバターURLを構成します。</li><li>バージョン4.0以降では利用できません。</li></ul>                                    |
| `SetLoc`                 | <ul><li>最後の位置の構成</li><li>現在のユーザーの最後に知られている位置を構成します。</li></ul>                                                                       |
| `SetDOB`                 | <ul><li>生年月日の構成</li><li>現在のユーザーの生年月日（日、月、年）を構成します。</li></ul>                                                             |
| `SetEmail`               | <ul><li>メールの構成</li><li>現在のユーザーのメールを構成します。</li></ul>                                                                                            |
| `SetEmailSub`            | <ul><li>メールサブスクリプションタイプの構成</li><li>現在のユーザーのメールサブスクリプションの通知タイプを構成します。</li></ul>                                       |
| `SetPushSub`             | <ul><li>プッシュサブスクリプションタイプの構成</li><li>現在のユーザーのプッシュ通知の通知タイプを構成します。</li></ul>                                        |
| `SetFirst`               | <ul><li>名の構成</li><li>現在のユーザーの名を構成します。</li></ul>                                                                                  |
| `SetLast`                | <ul><li>姓の構成</li><li>現在のユーザーの姓を構成します。</li></ul>                                                                                    |
| `SetCity`                | <ul><li>ホームシティの構成</li><li>現在のユーザーの都市を構成します。</li></ul>                                                                                         |
| `SetCountry`             | <ul><li>国の構成</li><li>現在のユーザーの国を構成します。</li></ul>                                                                                        |
| `SetLang`                | <ul><li>言語の構成</li><li>現在のユーザーの言語を構成します。</li></ul>                                                                                      |
| `SetPhone`               | <ul><li>電話番号の構成</li><li>現在のユーザーの電話番号を構成します。</li></ul>                                                                              |
| `SetGender`              | <ul><li>性別の構成</li><li>現在のユーザーの性別を構成します。</li></ul>                                                                                          |
| `removeFromSubscriptionGroup` | <ul><li>サブスクリプショングループから削除</li><li>メールまたはSMSのサブスクリプショングループから現在のユーザーを削除します。</li><li>この構成はバージョン3.5以降で利用可能です。</li></ul> |
| `setCustomLocationAttribute` | <ul><li>カスタム位置属性の構成</li><li>現在のユーザーのカスタム位置属性（キー、緯度、経度）を構成します。</li></ul>                          |
| `SetLineId`              | <ul><li>LINE IDの構成</li><li>現在のユーザーのLINEメッセージングアプリIDを構成します。</li></ul>                                                                          |
| `Ecommerce`              | <ul><li>イーコマースイベントのログ</li><li>現在のユーザーの構造化されたイーコマースイベントをログします。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul> |
| `WipeData`               | <ul><li>データのワイプ（ローカルSDKデータの削除）</li><li>ローカルに保存されたすべてのSDKデータを削除し、SDKを無効にします。</li><li>さらなるデータ収集を再開する前に、SDKを明示的に再有効化する必要があります。</li></ul> |
| `RefreshFeatureFlags`    | <ul><li>フィーチャーフラグの更新</li><li>Brazeから現在のユーザーのフィーチャーフラグを更新するよう要求します。</li></ul>                                                |
| `LogFeatureFlagImpression` | <ul><li>フィーチャーフラグインプレッションのログ</li><li>指定されたフィーチャーフラグのインプレッションイベントをログします。</li></ul>                                                    |
| `RefreshContentCards`    | <ul><li>コンテンツカードの更新</li><li>Brazeからコンテンツカードフィードを更新するよう要求します。</li></ul>                                                            |
| `ShowContentCards`       | <ul><li>コンテンツカードの表示</li><li>コンテンツカードフィードを表示します。</li></ul>                                                                                       |
| `LogContentCardImpressions` | <ul><li>コンテンツカードインプレッションのログ</li><li>コンテンツカードの配列のインプレッションイベントをログします。</li></ul>                                                     |
| `LogContentCardClick`    | <ul><li>コンテンツカードクリックのログ</li><li>特定のコンテンツカードのクリックイベントをログします。</li></ul>                                                                    |
| `RequestPushPermission`  | <ul><li>プッシュ通知の許可を要求</li><li>ユーザーにプッシュ通知の許可を求めます。</li></ul>                                                           |
| `UnregisterPush`         | <ul><li>プッシュの登録解除</li><li>現在のデバイスをプッシュ通知から登録解除します。</li></ul>                                                                   |
| `FlushData`              | <ul><li>データのフラッシュ</li><li>キューに入れられた分析データを直ちにBrazeサーバーに送信します。</li></ul>                                                                      |
| `RefreshBanners`         | <ul><li>バナーの更新</li><li>指定された配置IDのBrazeバナーを更新するよう要求します。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul> |
| `LogBannerImpressions`   | <ul><li>バナーインプレッションのログ</li><li>バナー配置IDの配列のインプレッションイベントをログします。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul> |
| `LogBannerClick`         | <ul><li>バナークリックを記録</li><li>特定のバナーのクリックイベントを記録します。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul>                  |
| `InsertBanner`           | <ul><li>バナーを挿入</li><li>指定された配置IDのバナーを取得し、指定された親要素に挿入します。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul> |
| `Custom`                 | <ul><li>カスタム</li><li>現在のユーザーによって作成されたカスタムイベントを送信します。</li></ul>                                                                                     |
### パラメータ

これらの目的地にデータをマッピングして、以前にマッピングされたイベントにデータを渡します。パラメータは事前定義されたイベントでのみ使用されます。カスタムイベントでパラメータを渡す方法については、以下のカスタムイベントデータセクションを参照してください。

事前定義されたイベントにパラメータを渡すには、次の手順を使用します：

1. イベントフィールドで、ドロップダウンリストからイベントを選択します。
1. パラメータフィールドで、ドロップダウンリストからパラメータを選択します。
1. カスタムパラメータの場合、カスタムイベントを識別する名前を入力します。
1. **+ 追加**をクリックします。

| **目的地名**  | **説明**                                                                                                                                                                                                                                    |
|:----------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `product_id`          | <ul><li>商品ID</li><li>アプリ内で購入された商品のユニークID。</li><li>`_cprod`を上書きします。</li></ul>                                                                                                                                   |
| `product_quantity`    | <ul><li>商品数量</li><li>アプリ内で購入された商品の数量。</li><li>これはeコマース値`_cquan`を上書きします。</li></ul>                                                                                                     |
| `order_id`            | <ul><li>注文ID</li><li>アプリ内購入のユニークID。</li><li>`_corder`を上書きします。</li></ul>                                                                                                                                             |
| `order_subtotal`      | <ul><li>注文小計</li><li>アプリ内購入の小計。</li><li>`_csubtotal`を上書きします。</li></ul>                                                                                                                                     |
| `order_currency`      | <ul><li>注文通貨</li><li>アプリ内購入のISO 4217通貨コード。</li><li>`_ccurrency`を上書きします。</li></ul>                                                                                                                        |
| `purchase_properties` | <ul><li>購入プロパティ</li><li>アプリ内購入の追加プロパティのオブジェクト。</li></ul>                                                                                                                                          |
| `alias`               | <ul><li>ユーザーエイリアス</li><li>現在のユーザーの識別子。</li></ul>                                                                                                                                                                           |
| `label`               | <ul><li>エイリアスラベル</li><li>エイリアスのソースなど、エイリアスのラベル。</li></ul>                                                                                                                                                      |
| `key`                 | <ul><li>カスタム属性キー</li><li>カスタム属性の識別子。</li><li>送信するパラメータの名前を入力します。</li></ul>                                                                                                           |
| `value`               | <ul><li>カスタム属性値</li><li>カスタム属性の値。</li><li>送信するパラメータの名前を入力します。</li></ul>                                                                                                              |
| `inc_value`           | <ul><li>カスタム属性増分値</li><li>カスタムユーザー属性を増分する値。</li><li>送信するパラメータの名前を入力します。</li><li>減少させるには負の数を使用します。</li><li>デフォルト値は`1`です。</li></ul> |
| `custom_attributes`   | <ul><li>カスタム属性オブジェクト</li><li>現在のユーザーに一度に構成するカスタム属性キー値ペアのオブジェクト。</li></ul>                                                                                                       |
| `line_id`             | <ul><li>ユーザーのLINE ID</li><li>現在のユーザーのLINEメッセージングアプリID。</li></ul>                                                                                                                                                          |
| `feature_flag_id`     | <ul><li>フィーチャーフラグID</li><li>印象を記録するためのフィーチャーフラグのユニーク識別子。</li></ul>                                                                                                                                     |
| `banner_placement_ids` | <ul><li>バナー配置ID（配列またはコンマ区切り）</li><li>バナー配置IDの配列またはコンマ区切りの文字列で、リフレッシュまたは印象を記録します。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul>            |
| `banner_placement_id` | <ul><li>バナー配置ID</li><li>単一のバナー配置のユニーク識別子で、取得して挿入します。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul>                                                           |
| `banner_click_id`     | <ul><li>バナークリックID</li><li>クリックされたバナーのクリック追跡ID。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul>                                                                                     |
| `banner_parent_selector` | <ul><li>バナーペアレントセレクタ（CSS）</li><li>バナーが挿入される親要素を識別するCSSセレクタ文字列。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul>                                   |
| `content_cards`       | <ul><li>コンテンツカード配列</li><li>印象を記録するためのコンテンツカードオブジェクトの配列。</li></ul>                                                                                                                                            |
| `content_card`        | <ul><li>コンテンツカードオブジェクト</li><li>クリックを記録するための単一のコンテンツカードオブジェクト。</li></ul>                                                                                                                                                    |
| `ecommerce_event_name` | <ul><li>イーコマースイベント名</li><li>記録するイーコマースイベントの名前。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul>                                                                                             |
| `ecommerce_properties` | <ul><li>イーコマースプロパティ</li><li>イーコマースイベントのプロパティのオブジェクト。</li><li><code>source</code>フィールドをサポートし、デフォルトは<code>"tealium"</code>です。</li><li>この構成はバージョン6.0以降で利用可能です。</li></ul> |
| `avatar_url`          | <ul><li>アバター画像URL</li><li>現在のユーザーが選択したアバターのURL。</li><li>バージョン4.0以降では利用不可です。</li></ul>                                                                                                           |
| `longitude`           | <ul><li>ユーザーの経度</li><li>ユーザーの位置の検証済み経度、度単位。</li><li>値は`-180`から`180`です</li></ul>                                                                                                     |
| `latitude`            | <ul><li>ユーザーの緯度</li><li>ユーザーの位置の検証済み緯度、度単位。</li><li>値は`-90`から`90`です</li></ul>                                                                                                         |
| `accuracy`            | <ul><li>位置精度</li><li>ユーザーの経度と緯度の精度、メートル単位。</li></ul>                                                                                                                                          |
| `altitude`            | <ul><li>ユーザーの高度</li><li>ユーザーの位置の高度（メートル単位）。</li></ul>                                                                                                                                                          |
| `altitude_accuracy`   | <ul><li>高度の精度</li><li>ユーザーの高度の精度（メートル単位）。</li></ul>                                                                                                                                                        |
| `year`                | <ul><li>ユーザーの生年</li><li>現在のユーザーの誕生日に関連する年。</li></ul>                                                                                                                                                  |
| `month`               | <ul><li>ユーザーの誕生月</li><li>現在のユーザーの誕生日に関連する月。</li></ul>                                                                                                                                                |
| `day`                 | <ul><li>ユーザーの誕生日</li><li>現在のユーザーの誕生日に関連する日。</li></ul>                                                                                                                                                    |
| `email`               | <ul><li>ユーザーのメールアドレス</li><li>現在のユーザーの検証済みメールアドレス。</li></ul>                                                                                                                                                            |
| `notification_type`   | <ul><li>通知の種類</li><li>現在のユーザーの選択された通知タイプ。</li><li>オプション: `opted_in`, `subscribed`, `unsubscribed`</li></ul>                                                                                |
| `first_name`          | <ul><li>ユーザーの名前</li><li>現在のユーザーの名前。</li></ul>                                                                                                                                                                    |
| `subscriptionGroupId` | <ul><li>サブスクリプショングループID</li><li>サブスクリプショングループの一意の識別子。</li></ul>                                                                                                                                                  |
| `last_name`           | <ul><li>ユーザーの姓</li><li>現在のユーザーの姓。</li></ul>                                                                                                                                                                      |
| `gender`              | <ul><li>ユーザーの性別</li><li>現在のユーザーの性別コード。</li><li>オプションは男性 (`m`), 女性 (`f`), その他 `o`。</li></ul>                                                                                                              |
| `customer_city`       | <ul><li>ユーザーの居住都市</li><li>現在のユーザーの居住都市。</li><li>`_ccity`を上書き。</li></ul>                                                                                                                                          |
| `customer_country`    | <ul><li>ユーザーの国</li><li>現在のユーザーの国。</li><li>`_ccountry`を上書き。</li></ul>                                                                                                                                           |
| `localization`        | <ul><li>ユーザーの言語</li><li>現在のユーザーの表示言語のISO 639-1言語コード。</li></ul>                                                                                                                                     |
| `phone_number`        | <ul><li>ユーザーの電話番号</li><li>現在のユーザーの電話番号。</li><li>数字、スペース、`+`, `.`, `-`, ` ( `, `)` の文字のみ許可</li></ul>                                                                         |

### カスタムイベントデータ

イベントタブで以前にマッピングしたカスタムイベントにカスタムパラメータを渡したい場合、カスタムイベントデータの目的地にマップします。

カスタムイベントデータ変数をマッピングするには、以下の手順に従ってください：

1. **イベント名**に、**イベント**タブで指定されたカスタムイベントの名前を入力します。
1. **パラメータ**に、送信したいパラメータの名前を入力します。
1. **+ 追加**をクリックします。

### クッキー同意

ユーザーの同意状態に基づいてBraze SDKが有効または無効になるように、クッキー同意の目的地にマップします。同意ゲーティングはSDKの初期化前に実行されます。

| **値** | **説明**                                                                                          |
|:----------|:---------------------------------------------------------------------------------------------------------|
| `grant`   | SDKを有効にし、データ収集を進めます。SDKは初期化され、セッションが通常通り開始されます。 |
| `revoke`  | 初期化前にSDKを無効にします。データは収集されず、セッションは開始されません。                   |

## ベンダー文書

* [Braze Web SDK](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/initial_sdk_setup/)