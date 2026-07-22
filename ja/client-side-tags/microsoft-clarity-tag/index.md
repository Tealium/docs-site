---
title: Microsoft Clarityタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでMicrosoft Clarityタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/microsoft-clarity-tag/
---
Microsoft Clarityは、ウェブサイトの訪問の行動をよりよく理解することで、ウェブサイトマネージャーがウェブサイトの体験を改善するために作られた無料の分析製品です。

## タグのヒント
*   プロジェクトIDの値を動的に上書きするためにマッピングを使用します
*   詳細については、[Bing: Microsoft Clarity is now Generally Available](https://blogs.bing.com/webmaster/october-2020/Microsoft-Clarity-is-now-Generally-Available)を参照してください

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[About tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **Project ID**: ClarityプロジェクトのID。プロジェクトIDはClarityプロジェクトのURLから見つけることができます。例えば、`https://clarity.microsoft.com/projects/view/PROJECT_ID/`。
* **Ad Storage Consent**: Ad Storageのデフォルトの同意を構成します。**Data Mappings**セクションの`ad_storage`パラメータをマッピングしてこの値を動的に更新します。
* **Automatically read from Tealium Consent Cookie**: trueに構成すると、同意は[Tealium Consent Manager](https://docs.tealium.com/about-consent-management/)に基づいて構成されます。

## 同意モード

このタグの同意モードを実装するための2つのオプションがあります：

* [Tealium Consent Management](https://docs.tealium.com/about-consent-management/)を使用し、Tealium Consent cookieを自動的に読み取ります。
* このタグに対してあなたの同意管理プラットフォーム（CMP）からの同意選択とカテゴリマッピングをマップするために、[JavaScript Code extension](https://docs.tealium.com/javascript-code-extension/)を追加します。

訪問が同意の選択をすると、タグは第一者と第三者のクッキーに対する適切なアプローチを選択します：

* **Granted**: 第一者と第三者の両方のクッキーを読み取り、書き込むことができます。
* **Denied**: 第一者のクッキーは読み取られず、書き込まれず、第三者のクッキーは詐欺とスパムの目的のためにのみ読み取られ、広告のためには使用されません。

### Tealium Consent Management

Tealium Consent Managementを使用してこのタグの同意モードを実装するには、タグ構成で**Automatically read from Tealium Consent Cookie**を`true`に構成します。

### JavaScript Code extension

エンドユーザーの同意選択をMicrosoftの同意モード構成にマップするには、JavaScript Code extensionを使用します。次のように拡張機能を構成します：

* **Scope**を**After Load Rules (default)**に構成します
* **Occurrence**を**Run Always**に構成します
* あなたのCMPのJavaScriptコードを入力します。以下のコードテンプレートをあなたのCMPに合わせてカスタマイズし、`CUSTOM_LOGIC`をあなたのベンダーのロジックに置き換えることができます。
```js
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? 'granted' : 'denied';
```

例えば、以下のコードはOneTrust用です。
```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf('C0004') !== -1  ? 'granted' : 'denied';
```

これらの正確な変数名を使用する場合、追加のマッピングは必要ありません。タグの最新バージョンはデフォルトでこれらの変数を使用します。`ad_storage`パラメータをあなたの特定のケースの属性にマッピングしてこれらの変数を上書きします。

## Load Rules

タグをすべてのページにロードするか、タグがロードされる条件を構成します。詳細については、[About load rules](https://docs.tealium.com/about-load-rules/)を参照してください。

## Data Mappings

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[About data mappings](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### Standard

| Variable | Description |
|:---------|:------------|
| `project_id` | ClarityプロジェクトのID。プロジェクトIDはClarityプロジェクトのURLから見つけることができます。例えば、`https://clarity.microsoft.com/projects/view/PROJECT_ID/`。 |


### Events

イベントをマップするには、[Create an Event Mapping](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| Event | Description |
|:------|:------------|
| `enable_consent` | 同意を有効にする |
| `disable_consent` | 同意を無効にする |

