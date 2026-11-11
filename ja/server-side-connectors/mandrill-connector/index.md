---
title: Mandrillコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでMandrill by MailChimpコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mandrill-connector/
---## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|テンプレートを使用したトランザクションメールの送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、以下の構成を構成します。

* **Mandrill APIキー**：このパラメータは必須です

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — テンプレートを使用したトランザクションメールの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ターゲットテンプレート| <ul><li>（必須）ターゲットテンプレート。</li></ul> |
|サブアカウント| <ul><li>（任意）このメッセージのサブアカウント</li><li>事前に存在している必要があります。存在しない場合はエラーになります</li></ul> |
|タグリスト| <ul><li>（任意）メッセージに付ける文字列タグ。</li><li>統計情報はタグを使用して集計されます。ただし、Mandrillに保存されるのは最初に確認された100個のみであるため、タグには一意の値や頻繁に変わる値を使用しないでください。</li><li>タグは50文字以内にしてください。</li><li>アンダースコアで始まるタグは内部使用のために予約されており、エラーの原因になります。</li></ul> |
|message.subject| メッセージの件名|
|message.from_email| 送信者のメールアドレス |
|message.from_name| 送信者名|
|message.to.email| <ul><li>（必須）受信者のメールアドレス</li></ul> |
|message.to.name| 受信者名|
|message.important| 値はtrueまたはfalseです|
|message.track_opens| <ul><li>ファイルが開かれたかどうかを追跡します</li><li>値はyesまたはnoです</li></ul> |
|message.track_clicks| <ul><li>クリックを追跡します</li><li>値はyesまたはnoです</li></ul> |
|message.auto_text| 任意|
|message.auto_html| 任意|
|message.inline_css| 任意|
|message.url_strip_qs| 任意|
|message.preserve_recipients| 任意|
|message.view_content_link| 任意|
|message.bcc_address| 任意|
|message.tracking_domain| 任意|
|message.signing_domain| 任意|
|message.return_path_domain| 任意|
|message.merge| 任意|
|message.merge_language| 任意|
|async| 任意|
|ip_pool| 任意|
|send_at| 任意|
|構成するGoogle Analyticsドメイン| <ul><li>（任意）一致するURLのクエリ文字列にGoogle Analyticsパラメータを自動的に追加する対象を示す文字列の配列。</li></ul> |
|構成するGoogle Analyticsキャンペーン| <ul><li>（任意）`utm_campaign`トラッキングパラメータに構成する値を示す文字列。</li><li>指定しない場合は、代わりにメールの送信元アドレスが使用されます。</li></ul> |
|受信者ヘッダータイプ| <ul><li>（任意）受信者に使用するヘッダータイプ。指定しない場合のデフォルトは「to」です。次のいずれかを指定します：`to`、`cc`、`bcc`</li><li>`to.type:`</li></ul> |
|ヘッダーデータ（値をキーにマッピング）| <ul><li>メッセージに追加する任意の追加ヘッダー（ほとんどのヘッダーを使用できます）</li></ul> |
|構成するテンプレートコンテンツ（コンテンツを名前にマッピング）| <ul><li>送信するテンプレートコンテンツの配列。</li><li>配列内の各項目は、次の2つのキーを持つ構造体にする必要があります：<ul><li>name：コンテンツを構成するコンテンツブロックの名前</li><li>content：ブロックに格納する実際のコンテンツ</li></ul></li></ul> |
|構成するグローバルマージ変数（コンテンツを名前にマッピング）| <ul><li>（任意）受信者に使用するグローバルマージ変数。</li><ul><li>name（文字列）：グローバルマージ変数の名前。マージ変数名では大文字と小文字が区別されず、アンダースコア（`_`）で始めることはできません</li><li>content（混合型）：グローバルマージ変数のコンテンツ</li></ul></ul> |
|構成するメタデータ（値をキーにマッピング）| <ul><li>（任意）ユーザーメタデータの連想配列。</li><li>Mandrillはこのメタデータを保存し、取得できるようにします。</li><li>さらに、最大10個のメタデータフィールドを選択してインデックスを作成し、Mandrill検索APIを使用して検索可能にできます。</li></ul> |