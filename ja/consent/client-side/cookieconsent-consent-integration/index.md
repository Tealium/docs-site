---
title: CookieConsent同意統合
description: このガイドでは、オープンソースの同意管理ツールであるCookieConsentをTealium iQと統合するための詳細な手順を提供します。
url: https://docs.tealium.com/ja/consent/client-side/cookieconsent-consent-integration/
---
CookieConsentは、クライアントサイドの[同意統合]()で強制できる柔軟なオープンソースの同意管理ツールです。このガイドでは、Tealium iQで同意統合を使用してCookieConsentを構成する方法について説明します。同意統合と組み合わせることで、CookieConsentは[Tealium同意マネージャー]()にはないより良い体験と追加機能を提供します。これには以下が含まれます：

* 同意バナーのA/Bテスト。
* 同意されていないデータが追跡されないようにする堅牢な強制と[キューシステム]()。
* より良いアクセシビリティサポート。
* ユーザーエラーによって引き起こされる問題を防ぐためのデフォルトでブロックするフレームワーク。詳細については、を参照してください。
* Collect（および類似のタグ）は[再発火]()に構成でき、サーバーサイドで「必要」と「ターゲティング」の追跡を明確にマークされたイベントでトリガーし、重複追跡を避けることができます。

## CookieConsentとCMP統合の比較

CookieConsentは新しいベンダーを導入せずに柔軟性と制御を提供します。しかし、IAB TCFをサポートせず、法的指導も提供しません。以下の要約を使用して、TealiumとのCookieConsentを商用同意管理プラットフォーム（CMP）と比較してください。

| 機能 | CookieConsent | CMP統合 |
|---------|---------------|-----------------|
| Tealium iQでの強制が容易 | ✓ | ✓ |
| Tealium同意レジスターは同意決定をアクセス可能にし、更新の購読が容易 | ✓ | ✓ |
| 同意の記録と保存を提供 | ✓ | ✓ |
| 会社のデザイン要件に合わせてカスタマイズが容易 | ✓ | ? |
| 会社の法的要件に合わせて調整が容易 | ✓ | ? |
| ウェブアクセシビリティ基準（WCAG）を容易に満たす | ✓ | ? |
| ベンダー固有のオプトアウトを提供 | ✓ | ? |
| 新しいベンダーの導入やレビューが不要（Tealiumのコンテンツ配信ネットワークでホスト） | ✓ | ✗ |
| 追加のサブスクリプションが不要（同意ログの保存やサポートへのアクセスに追加費用がかかる場合があります） | ✓ | ✗ |
| IAB TCFをサポートし、サイト広告を表示するウェブサイトに有用 | ✗ | ✓ |
| GDPRやCCPAなどのプライバシー規制に基づいた事前構成された構成を提供 | ✗ | ✓ |
| 法的指導を提供 | ✗ | ✓ |

`?`でマークされた機能は特定のCMPプロバイダーによって異なります。一部のCMPはアクセシビリティサポートやベンダー固有のオプトアウトなどの機能をサポートしている場合がありますが、他のCMPではサポートされていない場合があります。これらの機能のサポートを確認するために、CMPのドキュメントを確認してください。


CookieConsentは、一部の公開社や広告プラットフォームが必要とするIABの透明性と同意フレームワーク（TCF）をサポートしていません。お客様の組織がIAB TCFのサポートやGoogle認定CMPを必要とする場合は、代替ソリューションを使用してください。詳細については、[CookieConsent: あなたに適していますか？](https://cookieconsent.orestbida.com/essential/introduction.html#is-cookieconsent-the-right-tool-for-you)および[TealiumとIABの透明性と同意フレームワーク](https://tealium.com/blog/data-strategy/the-iabs-transparency-and-consent-framework-and-tealium/)を参照してください。


## このガイドは誰のためのものですか？

CookieConsentは、ユーザーの同意を管理するための柔軟なオープンソースアプローチを提供する同意管理ツールです。ポリシーの強制、分析、ベンダーのコンプライアンス管理などの追加機能を含む完全なCMPとは異なり、CookieConsentは企業が特定のニーズに応じて同意コントロールを実装できる透明で意見のないツールとして設計されています。

Tealiumとシームレスに統合され、カスタマイズ可能で開発者に優しいツールが必要な場合、CookieConsentは優れた選択肢です。ただし、IABフレームワークのサポートやGoogle認定の同意管理を含む包括的なCMPソリューションが必要な場合は、代替ソリューションが必要です。

## 必要条件

CookieConsent同意統合を作成するには、次のものが必要です：

* Tealium iQタグ管理
* クライアントサイドの同意統合

### なぜ使用するのか？

CookieConsentは、堅牢で非商業的な同意管理ツールとして[同意マネージャー]()を置き換え、複雑なコンプライアンスニーズに対応するために調整可能な堅牢な強制を提供する信頼性の高い同意キャプチャ層を提供します。

### カテゴリ、サービス、および目的の説明

CookieConsent V3は、カテゴリとサービスレベルの同意オプションの両方をサポートしています：

* **カテゴリ**は、`necessary`や`functional`のようなデータ処理の目的の広いグループです。これらはデータ使用ケースの高レベルのグルーピングを定義します。
* **サービス**は、カテゴリ内の特定のベンダーやサブ目的、例えば`necessary-vendor1`のようなものです。サービスは、カテゴリ内の個々のエンティティや明確な目的を定義することで、より詳細な同意構成を可能にします。

サービス名は、透明性のためにカテゴリ名とベンダー名またはサブ目的名をハイフンで結合しています。たとえば、`necessary`カテゴリ内のサービスには、`necessary-vendor1`や`necessary-subpurpose1`が含まれる場合があります。

カテゴリ内にサービスが定義されている場合、そのカテゴリ自体はマッピングに使用できなくなります。たとえば、`necessary`カテゴリに`necessary-vendor1`や`necessary-vendor2`などのサービスが含まれている場合、それらの特定のサービスのみがマッピングに使用できます。

**同意の振る舞い：**

* オプトインモードでは、カテゴリとそのサービスが許可されます。
* オプトアウトモードでは、`targeting`を除くすべてが許可されます。

## 統合手順

Tealium iQでCookieConsent統合を構成するために、次の手順を完了してください：

1. [CookieConsentライブラリを読み込む](#step-1-load-the-cookieconsent-library)。
1. [同意ログを実装する](#step-2-implement-consent-logging)。
1. [CookieConsent v3統合および強制ルールを作成する](#step-3-create-a-cookieconsent-v3-integration-and-enforcement-rule)。
1. [目的グループを作成する](#step-4-create-purpose-group)。
1. [Tealium iQプロファイルを保存して公開する](#step-5-save-and-publish-tealium-iq-profile)。
1. [テストとトラブルシューティング](#test-and-troubleshoot)。

### ステップ1: CookieConsentライブラリを読み込む

サイトにCookieConsentライブラリを読み込み、選択したカテゴリ、レイアウト、言語、および振る舞いで同意バナーとモーダルを表示するように構成します。

次のいずれかの方法でライブラリと構成を読み込みます：

* Tealium iQのCookieConsent v3 Loader拡張機能を使用して、ライブラリを読み込み、構成を適用します。拡張機能の構成方法については、[CookieConsent v3 Loader拡張機能]()を参照してください。
* サイトに直接CookieConsent v3ローダースクリプトと構成コードを埋め込みます。
### ステップ2：同意ログの実装

報告またはコンプライアンス目的のために、同意の構成と決定を記録します。

以下の方法のいずれかで同意ログを実装します：

* Tealium iQのCookieConsent v3 Logging拡張機能を使用します。この拡張機能はCookieConsentバナーからの同意更新をリッスンし、決定の詳細をJSONペイロードとして指定されたエンドポイントに送信します。拡張機能の構成コードを更新して目的地を構成します。拡張機能の構成方法については、[CookieConsent v3 Logging拡張機能]()を参照してください。
* CookieConsent v3ログ拡張機能コードを直接サイトに埋め込みます。

### ステップ3：CookieConsent v3統合と強制ルールの作成

CookieConsent v3の同意統合を構成し、同意を強制するルールを定義します。このステップでは、CookieConsentをTealium iQの同意ロジックにリンクし、ユーザーが適切な同意を与えたときにのみタグが発火するようにします。

1. **iQタグ管理 &gt; 同意統合**セクションに移動します。
1. **統合追加**をクリックします。
1. 統合の目的を明確に識別する名前を入力します。
1. ベンダーのドロップダウンリストから**CookieConsent v3**を選択します。
1. **次へ**をクリックします。
1. 適切な強制ルールを定義します。特定のユースケースに必要な場合は、免除を含めます。
    他の統合や免除との強制ルールが重複しないように注意してください。詳細については、[強制条件の競合の取り扱い]()を参照してください。
1. **次へ**をクリックします。
1. 公開場所を選択し、**次へ**をクリックします。

### ステップ4：目的グループの作成

まだ存在しない場合は、目的グループを作成して、CookieConsentによってキャプチャされた同意カテゴリとサービスをTealium iQのタグに定義してマッピングします。

1. 目的グループのドロップダウンリストから**&#43; 新しい目的グループ**を選択します。
1. **目的グループ作成**をクリックします。
1. 名前と説明を入力します。
1. **次へ**をクリックします。
1. 目的を作成します：
    * [CookieConsent v3 Loader拡張機能](#step-1-configure-the-cookieconsent-v3-loader-extension)の構成コードの`ccConfig.categories`から、各サービスまたはベンダーに対して目的を追加します。カテゴリ内にサービスやベンダーが存在しない場合のみ、カテゴリレベルの目的を追加します。
    * 各目的について、カテゴリ内のサービスキー（例：`necessary-necessary_vendor1`）を使用して、目的グループ内の同意決定にマッピングします。カテゴリキー（例：`necessary`）は、そのカテゴリにサービスが定義されていない場合のみ使用します。
1. **Tealium iQ目的**タブをクリックします。
1. Tealium iQが常にロードされるように、ユーザーがオプトアウトできない目的、例えば**厳密に必要**にTealium iQを割り当てます。
1. **タグマップ**タブをクリックします。
1. 各タグを適切な目的に割り当てます。
1. 同意が同じイベントで更新されたときにタグ（例えばTealium Collectタグ）が再発火することを望む場合は、タグの再発火を有効にします。
1. **保存**をクリックして目的グループを保存します。
1. **保存**をクリックして同意統合を保存します。
1. 新しい統合のテンプレートを生成するためにTealium iQプロファイルを保存して公開します。

### ステップ5：Tealium iQプロファイルの保存と公開

Tealium iQプロファイルを**Dev**環境に保存して公開し、**Prod**環境に公開する前にテストします。これで、クライアント側の同意統合でCookieConsentを正常に構成しました。

## テストとトラブルシューティング

[Tealium Tools Environment Switcher]()を使用して、環境間で実装をプレビューし、同意統合が期待通りに動作しているかを確認します。

### 同意統合セットアップの確認

1. サイトを訪れてトラッキングを承諾します。
1. 開発者ツールのJavaScriptコンソールを開きます。
1. ブラウザの開発者ツールで次のコマンドを使用してテストします：
    * `CookieConsent.show(true)`でバナーを表示します。
    * `CookieConsent.showPreferences(true)`で構成ダイアログを表示します。
1. 次のことを確認します：
    * バナーと構成ダイアログが正しく表示されます。
    * 同意決定が`cc_cookie`クッキーに保存されます。
    * 開発者ツールの**同意レジスタ**を使用して同意活動を監視します。
    * 有効な同意があるタグのみが発火されます。

同意状態をリセットするために、決定の間にCookieConsentクッキー（デフォルトでは`cc_cookie`）をクリアします。

強制の検証と問題のデバッグについての詳細は、[同意統合の検証とデバッグ]()を参照してください。

### テスト

CookieConsentと同意統合のエンドツーエンド統合テストのスイートについては、[CookieConsent &#43; Tealium iQ - エンドツーエンド統合テスト](https://solutions.tealium.net/hosted/cookieconsent/integration-test-report/summary.html)を参照してください。

## グローバルプライバシーコントロール（GPC）の統合

この統合は、GPCがアクティブな場合に同意バナーを抑制し、GPCに対する明示的な訪問の決定を優先し、訪問が手動でバナーを開くことを許可します。また、GPCが後で無効にされたシナリオでは、暗黙の同意ルールにフォールバックし、以前に同意した訪問が誤ってオプトアウトとして扱われないようにします。

このアプローチは技術的なガイダンスのみを提供します。グローバルプライバシーコントロール（GPC）の信号を検出し、優先し、または尊重するかどうかの決定は、組織の法務チームと協議して行う必要があります。法務チームは、GPCの動作が適用されるべきタイミング、それが影響を与えるべき同意状態、およびそれが既存の同意ワークフローとどのように相互作用するかを決定する必要があります。これらのソリューションを調整して、組織の法的、規制的、およびポリシー要件を満たす責任はあなたにあります。

### 仕組み

次のセクションでは、異なるシナリオでのグローバルプライバシーコントロール（GPC）信号と同意決定の取り扱いについて説明します。

**GPCをオプトアウト信号として扱う**  
このソリューションは、グローバルプライバシーコントロール（GPC）信号を完全なオプトアウトとして扱い、訪問の初回訪問およびその後のページロードまたは標準的なインタラクション中に同意バナーを抑制します。

**同意バナーと構成の対話の保存**  
訪問は、たとえばフッターリンクをクリックすることで、手動で同意バナーまたは構成ダイアログを開くことができます。開かれた場合、CookieConsentはGPC信号のために訪問をすべてのオプショナルトラッキングからオプトアウトした状態として表示します。

**明示的な同意決定の強制**  
このソリューションは、訪問が明示的な同意決定を行った場合、グローバルプライバシーコントロール（GPC）信号を無視します。同意クッキーが存在する場合、訪問の選択がGPCのオプトアウト信号を優先し、バナーと同意構成が訪問の選択に従って表示され、機能することを許可します。

**暗黙の同意決定にフォールバック**  
このソリューションは、グローバルプライバシーコントロール（GPC）信号が以前アクティブだったデバイスで無効にされた場合、デフォルトの暗黙の同意決定に依存します。
### コード

このコードをCookieConsent V3ローダー拡張機能に、`ccConfig`定義と`CookieConsent.run()`の呼び出しの間に追加してください。

この解決策は公式のCookieConsentプロジェクトに提案されました。更新情報はこちらでフォローしてください: https://github.com/orestbida/cookieconsent/issues/811


```js
// テスト用にこれをtrueまたはfalseに構成しますが、本番環境では戻してください
var gpcFlagIsTrue = navigator.globalPrivacyControl 
var noDecisionYet = typeof readCookie((ccConfig.cookie &amp;&amp; ccConfig.cookie.name) || &#39;cc_cookie&#39; ) !== &#39;string&#39; // すでに構成されている場合は文字列になります
// GPCフラグがtrueでオプトアウトモードの場合、オプショナルなトラッキングと初期バナーポップアップを無効にします（CCPAのように）
if (gpcFlagIsTrue &amp;&amp; ccConfig.mode === &#39;opt-out&#39; &amp;&amp; noDecisionYet) {
    logMessage(&#39;GPCフラグを強制して、オプトアウトモードでオプショナルなトラッキングと初期バナーポップアップを抑制します - クッキーは構成されません。&#39;)
    Object.keys(ccConfig.categories).forEach(function (cat){
        var thisCat = ccConfig.categories[cat]
        if (thisCat &amp;&amp; thisCat.enabled === true &amp;&amp; thisCat.readOnly !== true) {
            thisCat.enabled = false
        }
    })
    ccConfig.onModalShow = function (modalNameObj) {
        window.tealiumCmpIntegration = window.tealiumCmpIntegration || {};
        var modalName = modalNameObj.modalName;
        var alreadySuppressed = window.tealiumCmpIntegration.gpcAlreadySuppressedOnce === true;
        var validDecision = CookieConsent.validConsent();
        if (gpcFlagIsTrue &amp;&amp; !validDecision &amp;&amp; !alreadySuppressed) {
            // &#39;show&#39;が完了するのを待つためにここでsetTimeoutを使用する必要があります - 表示中に隠すと壊れます
            if (modalName === &#39;consentModal&#39;) setTimeout(CookieConsent.hide, 1);
            if (modalName === &#39;preferencesModal&#39;) setTimeout(CookieConsent.hidePreferences, 1);
            window.tealiumCmpIntegration.gpcAlreadySuppressedOnce = true    // 最初のポップアップのみを抑制し、手動でポップアップさせることを許可します
        }
    }
}

// GPCヘルパー関数
function logMessage (message) {
  var loggingFunction = (window.tealiumCmpIntegration &amp;&amp; window.tealiumCmpIntegration.logger) || (window.utag &amp;&amp; window.utag.DB)
  return loggingFunction(message);
}

function readCookie (name) {
    var reString = &#39;(?:(?:^|.*;\\s*)&#39; &#43; name &#43; &#39;\\s*\\=\\s*([^;]*).*$)|^.*$&#39;;
    var re = new RegExp(reString);
    var cookieValue = document.cookie.replace(re, &#34;$1&#34;);
    if (!cookieValue) return undefined;
    return cookieValue;
}
```


## 追加リソース

* [同意統合](): 同意統合構成の参照。
* [CookieConsent v3.1.0 プレイグラウンド](https://playground.cookieconsent.orestbida.com/): 構成とスタイルを探索。
* [CookieConsent: UIカスタマイズ](https://cookieconsent.orestbida.com/advanced/ui-customization.html): UIカスタマイズガイド。