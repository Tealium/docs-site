---
title: Microsoft Clarityタグ構成ガイド
description: この記事では、タグ管理アカウントでMicrosoft Clarityタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/microsoft-clarity-tag/
---
Microsoft Clarityは、サイト訪問の行動をより深く理解することで、Webサイト管理者がWebサイト上の体験を改善できるよう支援する、無料で利用可能な分析製品です。

## タグに関するヒント
*   マッピングを使用して、プロジェクトIDの値を動的に上書きします。
*   詳細については、[Bing：Microsoft Clarityの一般提供を開始](https://blogs.bing.com/webmaster/october-2020/Microsoft-Clarity-is-now-Generally-Available)を参照してください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **プロジェクトID**：ClarityのプロジェクトID。プロジェクトIDは、ClarityプロジェクトのURLで確認できます。例：`https://clarity.microsoft.com/projects/view/PROJECT_ID/`
* **広告保存の同意**：広告保存に対するデフォルトの同意を構成します。**データマッピング**セクションで`ad_storage`パラメータをマッピングすると、この値を動的に更新できます。
* **分析保存の同意**：分析保存に対するデフォルトの同意を構成します。オプションは、**未構成**、**許可**、**拒否**です。**未構成**に構成した場合、分析保存は**広告保存の同意**構成に従います。**データマッピング**セクションで`analytics_storage`パラメータをマッピングすると、この値を動的に更新できます。
* **Tealium同意Cookieから自動的に読み取る**：trueに構成すると、[Tealium同意マネージャー](https://docs.tealium.com/about-consent-management/)に基づいて同意が構成されます。

## 同意モード

このタグでは、広告保存と分析保存のシグナルを個別に送信するClarityの[Consent API v2](https://learn.microsoft.com/en-us/clarity/setup-and-installation/clarity-consent-api-v2)を使用します。Consent API v2は、EEA、英国、スイスの訪問に適用されます。

このタグに同意モードを実装するには、次の2つの方法があります。

* [クライアントサイド同意管理](https://docs.tealium.com/about-consent-management/)を使用し、Tealium同意Cookieを自動的に読み取ります。
* [JavaScriptコード拡張機能](https://docs.tealium.com/javascript-code-extension/)を追加して、同意管理プラットフォーム（CMP）の同意選択とカテゴリーマッピングをこのタグにマッピングします。

訪問が同意内容を選択すると、タグはファーストパーティCookieとサードパーティCookieに対して適切な処理を選択します。

* **許可**：ファーストパーティCookieとサードパーティCookieの両方を読み書きできます。
* **拒否**：ファーストパーティCookieは読み書きされません。サードパーティCookieは、広告目的ではなく、不正行為およびスパム対策の目的に限り、読み取り専用となります。

### クライアントサイド同意管理

クライアントサイド同意管理を使用してこのタグに同意モードを実装するには、タグ構成で**Tealium同意Cookieから自動的に読み取る**を`true`に構成します。

### JavaScriptコード拡張機能

エンドユーザーの同意選択をMicrosoftの同意モード構成にマッピングするには、JavaScriptコード拡張機能を使用します。拡張機能を次のように構成します。

* **スコープ**を**ロードルールの後（デフォルト）**に構成します。
* **実行頻度**を**常に実行**に構成します。
* CMP用のJavaScriptコードを入力します。次のコードテンプレートの`CUSTOM_LOGIC`をベンダー固有のロジックに置き換えることで、CMPに合わせてカスタマイズできます。

```js
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? 'granted' : 'denied';
```

たとえば、次のコードはOneTrust用です。

```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf('C0004') !== -1  ? 'granted' : 'denied';
```

これらの変数名をそのまま使用する場合、追加のマッピングは必要ありません。最新バージョンのタグでは、これらの変数がデフォルトで使用されます。特定のユースケースに応じて`ad_storage`パラメータを属性にマッピングし、これらの変数を上書きします。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `project_id` | ClarityのプロジェクトID。プロジェクトIDは、ClarityプロジェクトのURLで確認できます。例：`https://clarity.microsoft.com/projects/view/PROJECT_ID/` |
| `ad_storage` | 広告保存の同意。**広告保存の同意**構成構成を上書きします。有効な値：`granted`または`denied` |
| `analytics_storage` | 分析保存の同意。**分析保存の同意**構成構成を上書きします。有効な値：`granted`または`denied` |


### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `enable_consent` | 同意を有効にします。 |
| `disable_consent` | 同意を無効にします。 |

「イベント」タブで構成したカスタムイベント名は、カスタムイベントとしてClarityに転送されます。イベント固有のマッピングには、**カスタムイベント**カテゴリーの`custom_event_name`宛先を使用します。

### Cookieの同意

ユーザーの同意状態に基づいてCookieの同意を制御するには、「Cookieの同意」宛先にマッピングします。

| 変数 | 説明 |
|:---------|:------------|
| `grant` | Cookieの同意を許可します。広告保存と分析保存の両方に対して`granted`を指定したConsent API v2シグナルを送信します。 |
| `revoke` | Cookieの同意を取り消します。Clarity Cookieを消去します。 |

### 識別

タグが発火するたびにClarityの[Identify API](https://learn.microsoft.com/en-us/clarity/setup-and-installation/identify-api)を呼び出すには、次の宛先をマッピングします。Identify APIは、`custom_user_id`がマッピングされ、空でない場合にのみ呼び出されます。

| 変数 | 説明 |
|:---------|:------------|
| `custom_user_id` | カスタムユーザー識別子。Identify API呼び出しをトリガーするために必要です。 |
| `session_id` | セッション識別子。 |
| `page_id` | ページ識別子。 |
| `friendly_name` | セッションを表す、人が読みやすいラベル。 |

### カスタムタグ

| 変数 | 説明 |
|:---------|:------------|
| `tag.{key}` | カスタムタグ。マッピングされた値を使用して`clarity('set', key, value)`を呼び出します。文字列または文字列の配列を指定できます。`{key}`をタグキー名に置き換えます。 |

### カスタムイベント

| 変数 | 説明 |
|:---------|:------------|
| `custom_event_name` | Clarityに転送されるカスタムイベント名。`clarity('event', name)`を呼び出します。 |

### アップグレード

| 変数 | 説明 |
|:---------|:------------|
| `upgrade_reason` | Clarityのセッション記録品質をアップグレードする理由。`clarity('upgrade', reason)`を呼び出します。詳細については、[Clarity API](https://learn.microsoft.com/en-us/clarity/setup-and-installation/clarity-api)を参照してください。 |