---
title: Mandrillコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでMandrill by MailChimpコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mandrill-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|テンプレートを使用したトランザクションメールの送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **Mandrill APIキー**：このパラメータは必須です

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - テンプレートを使用したトランザクションメールの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Target Template|  <ul><li>必須</li><li>ターゲットテンプレート。</li></ul> |
|Subaccount|  <ul><li>オプション</li><li>このメッセージのサブアカウント</li><li>すでに存在しない場合はエラーとなります</li></ul> |
|Tag List|  <ul><li>オプション</li><li>メッセージにタグを付けるための文字列。</li><li>統計はタグを使用して蓄積されますが、Mandrillは最初の100個しか保存しないため、これは一意であるか頻繁に変更されるべきではありません。</li><li>タグは50文字以下であるべきです。</li><li>アンダースコアで始まる任意のタグは内部使用のために予約されており、エラーを引き起こします。</li></ul> |
|message.subject| メッセージの件名|
|message.from_email| 送信者のメールアドレス |
|message.from_name| 送信者の名前|
|message.to.email|  <ul><li>必須</li><li>受信者のメールアドレス</li></ul> |
|message.to.name| 受信者の名前|
|message.important| 値はtrueまたはfalse|
|message.track_opens|  <ul><li>ファイルの開封を追跡</li><li>値はyesまたはno</li></ul> |
|message.track_clicks|  <ul><li>クリックを追跡</li><li>値はyesまたはno</li></ul> |
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
|Google Analytics Domains to Set|  <ul><li>オプション</li><li>一致するURLに自動的にGoogle Analyticsのパラメータをクエリ文字列に追加するための文字列の配列。</li></ul> |
|Google Analytics Campaign to Set|  <ul><li>オプション</li><li>`utm_campaign`追跡パラメータの値を構成するための文字列。</li><li>提供されていない場合、メールの送信元アドレスが代わりに使用されます。</li></ul> |
|Recipient Header Type|  <ul><li>オプション</li><li>受信者に使用するヘッダータイプ、提供されていない場合はデフォルトで"to"のいずれか：`to`、`cc`、`bcc`</li><li>`to.type:`</li></ul> |
|Header Data (Map Value to Key)|  <ul><li>メッセージに追加するオプションの追加ヘッダー（ほとんどのヘッダーが許可されています）</li></ul> |
|Template Content To Set (Map Content to Name)|  <ul><li>送信するテンプレートコンテンツの配列。</li><li>配列の各項目は2つのキーを持つ構造体であるべきです：<ul><li>name コンテンツブロックの名前を構成するための名前</li><li>content ブロックに入れる実際のコンテンツ</li></ul> </li></ul> |
|Global Merge Vars To Set (Map Content to Name)|  <ul><li>オプション</li><li>受信者に使用するグローバルマージ変数。</li> <ul><li>name (string) グローバルマージ変数の名前。マージ変数名は大文字小文字を区別せず、アンダースコア (`_`) 文字で始まることはできません</li><li>content (mixed) グローバルマージ変数の内容</li></ul> </ul> |
|Metadata To Set (Map Value to Key)|  <ul><li>オプション</li><li>メタデータ ユーザーメタデータの連想配列。</li><li>Mandrillはこのメタデータを保存し、取得可能にします。</li><li>さらに、Mandrillの検索APIを使用して検索可能にするために、最大10のメタデータフィールドを選択してインデックスを作成できます。</li></ul> |

