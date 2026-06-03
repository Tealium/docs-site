---
title: 同意構成マネージャーの仕組み
description: 同意構成マネージャーは、ウェブサイトにトラッキング構成オプションを簡単に展開することができます。顧客は許可するタグのカテゴリを指定できます。このツールは、構成ポップアップを生成するコードをカスタマイズする完全なアクセス権と、グローバルな顧客向けにコンテンツを翻訳する能力を提供します。
url: https://docs.tealium.com/ja/consent/client-side/consent-management/consent-preferences-dialog/about/
---
## 仕組み

同意構成マネージャーは、[同意プロンプトマネージャー]()と連携して、顧客にトラッキングオプションを提示し、以前に[プライバシーマネージャー拡張]()によって提供されていた機能を置き換えます。

`cmGeneral`の新しいバージョンでは、同意構成マネージャーは明示的な同意プロンプトマネージャーが必要です。これは、彼らが共有する強制ルールのためです。明示的な同意プロンプトが無効の場合、同意構成マネージャーは期待通りに動作しません。明示的な同意プロンプトを表示せずに同意構成マネージャーを使用するには、以下の[同意構成マネージャーを明示的な同意プロンプトなしで使用する](#use-the-consent-preferences-manager-without-showing-the-explicit-consent-prompt)セクションを参照してください。

同意構成マネージャーは、`Analytics`、`Display Ads`、または`Email Marketing`などの機能と目的に基づいてタグをカテゴリに分類します。これらのカテゴリは顧客に提示され、トラッキングを許可または禁止するためのトグルボタンとして表示されます。たとえば、ユーザーが`Marketing`カテゴリのオプトアウトを選択した場合、マーケティングカテゴリに分類されたタグは抑制されます。必要に応じて、顧客は同意構成ポップアップを使用して、許可するトラッキングの種類についての選択を再アクセスすることができます。

同意構成マネージャーは、オプトアウトしたカテゴリのタグの読み込みを自動的に抑制します。

構成ポップアップの例：

![](/images/iq-tag-management/consent-preferences-prompt.png)

iQタグ管理の同意構成マネージャーは、既存のインストールを使用してウェブサイトにトラッキング構成プロンプトの作成と展開を簡素化します。公開後、ページコードに単純なJavaScript関数呼び出しを追加してポップアップをトリガーします。

## 明示的な同意プロンプトを表示せずに同意構成マネージャーを使用する

`cmGeneral`の最近のバージョンでは、同意構成マネージャーは明示的な同意プロンプトマネージャーが必要です。これは、彼らが共有する強制ルールのためです。

明示的な同意プロンプトを表示せずに同意構成マネージャーを使用するには、**Before Load Rules**にスコープされたJavaScript Code拡張に次のコードを追加し、一度実行するように構成します：

```javascript
// SCOPE: Before Load Rules (run once)  
utag.gdpr.consent_prompt.noShow = true;

function checkForLoadedConsent() { 
    var foundDecision = window.tealiumConsentRegister &amp;&amp; window.tealiumConsentRegister.currentDecision; 
    return !!foundDecision;
}

function checkForImplicitDecision() { 
    var foundDecision = checkForLoadedConsent(); 
    var foundExplicitDecision = window.tealiumConsentRegister &amp;&amp; window.tealiumConsentRegister.currentDecision &amp;&amp; 
        window.tealiumConsentRegister.currentDecision.type === &#39;explicit&#39;; 
    return foundDecision &amp;&amp; !foundExplicitDecision; 
}

function showPreferences() { 
    return utag &amp;&amp; utag.gdpr &amp;&amp; utag.gdpr.showConsentPreferences &amp;&amp; utag.gdpr.showConsentPreferences(); 
}

// If the decision is only implicit, pop up the Preferences Modal to prompt a decision  
if (!checkForLoadedConsent()) { 
    window.addEventListener(&#39;consent_loaded&#39;, (event) =&gt; { 
        if (checkForImplicitDecision() &amp;&amp; utag.gdpr.getEnforcementMode() === &#39;opt-in&#39;) 
            showPreferences(); 
    }); 
} else if (checkForImplicitDecision() &amp;&amp; utag.gdpr.getEnforcementMode() === &#39;opt-in&#39;) { 
    showPreferences(); 
}
```

## EventStream同意カテゴリ

同意構成の変更は、Tealium EventStreamコネクタによっても尊重されます。コネクタアクションの同意カテゴリは、**Action**構成画面に表示されます：

![](/images/iq-tag-management/consent-categories-connector-action.png)

顧客が同意カテゴリ構成を行うと、それらは後続のサーバーサイドリクエストに含まれます。顧客がオプトインしたカテゴリのコネクタアクションのみがトリガーされます。

#### 例

`Analytics`と`Personalization`の2つのコネクタが構成されているとします。顧客が構成フォームで部分的な同意を与え、`Analytics`のトラッキングは許可するが`Personalization`は許可しないとします。

![](/images/iq-tag-management/consent-server-side-categories-example.png)

`Analytics`カテゴリのコネクタアクションのみがトリガーされます。`Personalization`に分類されるコネクタアクションは抑制されます。

## AudienceStream同意カテゴリ

Tealium AudienceStreamは`CDP`同意カテゴリに分類されます。AudienceStreamで属性とコネクタを処理するためには、訪問は`CDP`カテゴリにオプトインしている必要があります。

## DataAccess同意カテゴリ

EventStoreとEventDBは`Big Data`同意カテゴリに分類されます。EventStoreとEventDBにイベントデータを保存するためには、訪問は`Big Data`カテゴリにオプトインしている必要があります。

AudienceDBは`CDP`同意カテゴリに分類されます。AudienceDBにオーディエンスデータを保存するためには、訪問は`CDP`カテゴリにオプトインしている必要があります。

## 機能

同意構成マネージャーは、次の機能を提供します：

* 表示テンプレート
* カスタマイズ可能なスタイルとレイアウト
* 多言語サポート
* タグカテゴリ

すべての構成は、JavaScriptライブラリ（utag.js）の既存のインストールと一緒にバンドルされています。

構成プロンプトをアクティブ化して構成すると、次の公開で変更がリリースされます。

## グローバル構成

同意構成マネージャーは、グローバル構成を使用することで複数のプロファイルで同時に構成可能です。これにより、アカウントレベルで構成ポップアップを構成し、各プロファイルがグローバル構成を継承することができます。[グローバル同意内容]()についてもっと学びましょう。

