---
title: Microsoft Clarity タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Microsoft Clarity タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/microsoft-clarity-tag/
---
Microsoft Clarity は、ウェブサイトの訪問の行動をよりよく理解することで、ウェブサイトの体験を改善するのを支援するために作られた無料の分析製品です。

## タグのヒント
*   プロジェクトIDの値を動的に上書きするためにマッピングを使用する
*   詳細については、[Bing: Microsoft Clarity が一般公開されました](https://blogs.bing.com/webmaster/october-2020/Microsoft-Clarity-is-now-Generally-Available)を参照してください

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法についての詳細は、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **プロジェクトID**：Clarity プロジェクトID。プロジェクトIDは、Clarity プロジェクトのURLから見つけることができます。例：`https://clarity.microsoft.com/projects/view/PROJECT_ID/`。
* **広告保存の同意**：広告保存のデフォルト同意を構成します。`ad_storage`パラメータを**データマッピング**セクションでマッピングすることにより、この値を動的に更新します。
* **分析保存の同意**：分析保存のデフォルト同意を構成します。オプションは**未構成**、**許可**、**拒否**です。**未構成**に構成されている場合、分析保存は**広告保存の同意**構成に従います。`analytics_storage`パラメータを**データマッピング**セクションでマッピングすることにより、この値を動的に更新します。
* **Tealium 同意クッキーから自動的に読み取る**：trueに構成されている場合、同意は[Tealium 同意マネージャー](https://docs.tealium.com/about-consent-management/)に基づいて構成されます。

## 同意モード

このタグは、独立した広告および分析保存の信号を送信するClarityの[同意API v2](https://learn.microsoft.com/en-us/clarity/setup-and-installation/clarity-consent-api-v2)を使用します。同意API v2は、EEA、英国、スイスの訪問に対して適用されます。

このタグの同意モードを実装するには2つのオプションがあります：

* [クライアントサイドの同意管理](https://docs.tealium.com/about-consent-management/)を使用し、Tealium 同意クッキーを自動的に読み取る。
* [JavaScript コード拡張](https://docs.tealium.com/javascript-code-extension/)を追加して、同意管理プラットフォーム（CMP）からこのタグに同意選択とカテゴリマッピングをマップします。

訪問が同意選択を行うと、タグは第一者および第三者クッキーに対して適切なアプローチを選択します：

* **許可**：第一者および第三者クッキーの両方を読み書きできます。
* **拒否**：第一者クッキーは読み書きされず、第三者クッキーは詐欺およびスパム目的でのみ読み取り可能で、広告目的ではありません。

### クライアントサイドの同意管理

このタグの同意モードをクライアントサイドの同意管理を使用して実装するには、タグ構成で**Tealium 同意クッキーから自動的に読み取る**を`true`に構成します。

### JavaScript コード拡張

エンドユーザーの同意選択をMicrosoft同意モード構成にマッピングするには、JavaScript コード拡張を使用します。拡張を次のように構成します：

* **スコープ**を**ロードルール後（デフォルト）**に構成
* **発生**を**常に実行**に構成
* CMPのためのロジックで`CUSTOM_LOGIC`を置き換えることにより、CMP用の以下のJavaScriptコードテンプレートをカスタマイズします。
```js
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? 'granted' : 'denied';
```

例えば、以下のコードはOneTrust用です。
```js
// ロードルール後 - 常に実行
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf('C0004') !== -1  ? 'granted' : 'denied';
```

これらの正確な変数名を使用する場合、追加のマッピングは必要ありません。タグの最新バージョンはデフォルトでこれらの変数を使用します。特定のケースの属性に`ad_storage`パラメータをマッピングすることにより、これらの変数を上書きします。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `project_id` | Clarity プロジェクトID。プロジェクトIDは、Clarity プロジェクトのURLから見つけることができます。例：`https://clarity.microsoft.com/projects/view/PROJECT_ID/`。 |
| `ad_storage` | 広告保存の同意。**広告保存の同意**構成を上書きします。有効な値：`granted`または`denied`。 |
| `analytics_storage` | 分析保存の同意。**分析保存の同意**構成を上書きします。有効な値：`granted`または`denied`。 |


### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください

| イベント | 説明 |
|:------|:------------|
| `enable_consent` | 同意を有効にする |
| `disable_consent` | 同意を無効にする |

イベントタブで構成されたカスタムイベント名は、カスタムイベントとしてClarityに転送されます。イベント固有のマッピングには、**カスタムイベント**カテゴリの`custom_event_name`宛先を使用します。

### クッキー同意

クッキー同意宛先にマッピングして、ユーザーの同意状態に基づいてクッキー同意を制御します。

| 変数 | 説明 |
|:---------|:------------|
| `grant` | クッキー同意を許可。`granted`のConsent API v2信号を送信します。 |
| `revoke` | クッキー同意を取り消す。Clarityクッキーを消去します。 |

### 識別

以下の宛先にマッピングして、各タグ発火時にClarity [識別API](https://learn.microsoft.com/en-us/clarity/setup-and-installation/identify-api)を呼び出します。`custom_user_id`がマッピングされており、空でない場合にのみ識別APIが呼び出されます。

| 変数 | 説明 |
|:---------|:------------|
| `custom_user_id` | カスタムユーザー識別子。識別API呼び出しをトリガーするために必要です。 |
| `session_id` | セッション識別子。 |
| `page_id` | ページ識別子。 |
| `friendly_name` | セッションの人間が読めるラベル。 |

### カスタムタグ

| 変数 | 説明 |
|:---------|:------------|
| `tag.{key}` | カスタムタグ。マッピングされた値で`clarity('set', key, value)`を呼び出します。文字列または文字列の配列を受け入れます。`{key}`をタグキー名に置き換えます。 |

### カスタムイベント

| 変数 | 説明 |
|:---------|:------------|
| `custom_event_name` | Clarityに転送されるカスタムイベント名。`clarity('event', name)`を呼び出します。 |

### アップグレード

| 変数 | 説明 |
|:---------|:------------|
| `upgrade_reason` | Clarityセッション録画品質をアップグレードする理由。`clarity('upgrade', reason)`を呼び出します。詳細については、[Clarity API](https://learn.microsoft.com/en-us/clarity/setup-and-installation/clarity-api)を参照してください。 |
