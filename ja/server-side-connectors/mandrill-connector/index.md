---
title: Mandrillコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでMandrill by MailChimpコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mandrill-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|テンプレートを使用したトランザクションメールの送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **Mandrill APIキー**：このパラメータは必須です

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - テンプレートを使用したトランザクションメールの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Target Template|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;ターゲットテンプレート。&lt;/li&gt;&lt;/ul&gt; |
|Subaccount|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;このメッセージのサブアカウント&lt;/li&gt;&lt;li&gt;すでに存在しない場合はエラーとなります&lt;/li&gt;&lt;/ul&gt; |
|Tag List|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;メッセージにタグを付けるための文字列。&lt;/li&gt;&lt;li&gt;統計はタグを使用して蓄積されますが、Mandrillは最初の100個しか保存しないため、これは一意であるか頻繁に変更されるべきではありません。&lt;/li&gt;&lt;li&gt;タグは50文字以下であるべきです。&lt;/li&gt;&lt;li&gt;アンダースコアで始まる任意のタグは内部使用のために予約されており、エラーを引き起こします。&lt;/li&gt;&lt;/ul&gt; |
|message.subject| メッセージの件名|
|message.from_email| 送信者のメールアドレス |
|message.from_name| 送信者の名前|
|message.to.email|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;受信者のメールアドレス&lt;/li&gt;&lt;/ul&gt; |
|message.to.name| 受信者の名前|
|message.important| 値はtrueまたはfalse|
|message.track_opens|  &lt;ul&gt;&lt;li&gt;ファイルの開封を追跡&lt;/li&gt;&lt;li&gt;値はyesまたはno&lt;/li&gt;&lt;/ul&gt; |
|message.track_clicks|  &lt;ul&gt;&lt;li&gt;クリックを追跡&lt;/li&gt;&lt;li&gt;値はyesまたはno&lt;/li&gt;&lt;/ul&gt; |
|message.auto_text| オプション|
|message.auto_html| オプション|
|message.inline_css| オプション|
|message.url_strip_qs| オプション|
|message.preserve_recipients| オプション|
|message.view_content_link| オプション|
|message.bcc_address| オプション|
|message.tracking_domain| オプション|
|message.signing_domain| オプション|
|message.return_path_domain| オプション|
|message.merge| オプション|
|message.merge_language| オプション|
|async| オプション|
|ip_pool| オプション|
|send_at| オプション|
|Google Analytics Domains to Set|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;一致するURLに自動的にGoogle Analyticsのパラメータをクエリ文字列に追加するための文字列の配列。&lt;/li&gt;&lt;/ul&gt; |
|Google Analytics Campaign to Set|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;`utm_campaign`追跡パラメータの値を構成するための文字列。&lt;/li&gt;&lt;li&gt;提供されていない場合、メールの送信元アドレスが代わりに使用されます。&lt;/li&gt;&lt;/ul&gt; |
|Recipient Header Type|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;受信者に使用するヘッダータイプ、提供されていない場合はデフォルトで&#34;to&#34;のいずれか：`to`、`cc`、`bcc`&lt;/li&gt;&lt;li&gt;`to.type:`&lt;/li&gt;&lt;/ul&gt; |
|Header Data (Map Value to Key)|  &lt;ul&gt;&lt;li&gt;メッセージに追加するオプションの追加ヘッダー（ほとんどのヘッダーが許可されています）&lt;/li&gt;&lt;/ul&gt; |
|Template Content To Set (Map Content to Name)|  &lt;ul&gt;&lt;li&gt;送信するテンプレートコンテンツの配列。&lt;/li&gt;&lt;li&gt;配列の各項目は2つのキーを持つ構造体であるべきです：&lt;ul&gt;&lt;li&gt;name コンテンツブロックの名前を構成するための名前&lt;/li&gt;&lt;li&gt;content ブロックに入れる実際のコンテンツ&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Global Merge Vars To Set (Map Content to Name)|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;受信者に使用するグローバルマージ変数。&lt;/li&gt; &lt;ul&gt;&lt;li&gt;name (string) グローバルマージ変数の名前。マージ変数名は大文字小文字を区別せず、アンダースコア (`_`) 文字で始まることはできません&lt;/li&gt;&lt;li&gt;content (mixed) グローバルマージ変数の内容&lt;/li&gt;&lt;/ul&gt; &lt;/ul&gt; |
|Metadata To Set (Map Value to Key)|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;メタデータ ユーザーメタデータの連想配列。&lt;/li&gt;&lt;li&gt;Mandrillはこのメタデータを保存し、取得可能にします。&lt;/li&gt;&lt;li&gt;さらに、Mandrillの検索APIを使用して検索可能にするために、最大10のメタデータフィールドを選択してインデックスを作成できます。&lt;/li&gt;&lt;/ul&gt; |

