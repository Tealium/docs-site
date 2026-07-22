---
title: テンプレートについて
description: このドキュメントでは、iQタグ管理テンプレートの基本的な概念について紹介します。
url: https://docs.tealium.com/ja/iq-tag-management/templates/about/
---
## 動作原理

テンプレートは、iQタグ管理の機能、タグ、または機能コンポーネントの核となるロジックを提供するJavaScriptコードです。テンプレートは、Tealium iQの構成を組み立てて、サイトやアプリで実行されるJavaScriptファイルにします。コンポーネント別のテンプレートのリストについては、[テンプレートの種類](#template-types)を参照してください。

ユーザーは[テンプレートステータスチェッカー](https://docs.tealium.com/template-status-checker/)を実行して、テンプレートが最新であることを確認できます。上級ユーザーは、以下の場合にテンプレートを直接編集することが役立ちます：

* サポートされていないベンダーや自作ソリューションの機能を構築するために、[カスタムコンテナタグ](https://docs.tealium.com/tealium-custom-container-tag/)や[カスタム同意統合](https://docs.tealium.com/custom-cmp-integrations/)を追加する。
* 公式の修正がリリースされるまでの間、タグのバグを一時的に修正する。
* 特定のニーズに合わせてテンプレート化されたコンポーネントの核となるロジックを変更する。


<blockquote>
カスタマイズや修正は、テンプレートを編集するのではなく、拡張機能を使用して行うことができます。拡張機能は時間が経っても維持が容易ですので、まずは拡張機能の使用を検討してください。
</blockquote>


テンプレートの編集や更新についての詳細は、[テンプレートの管理](https://docs.tealium.com/manage-templates/)を参照してください。

## テンプレートの種類

テンプレートは、システムタグ、ベンダータグ、および同意管理に使用されます。テンプレートのリストを表示するとき、各タイプは以下の名前で識別できます：

### システムタグ

* **uTag Loader** (`utag.js`)  
ユニバーサルタグのテンプレートです。ユニバーサルタグは、サイトにサードパーティのタグをロードするために必要なすべての生成コードを含むJavaScriptコードです。詳細については、[JavaScript (`utag.js`)のインストール](https://docs.tealium.com/ja/platforms/javascript/install/#universal-tag-utagjs)を参照してください。
* **uTag Sync** (`utag.sync.js`)  
このファイルは、Adobe TargetやOptimizelyなどのA/Bテストタグや多変量テストタグをサポートするためにページに使用されます。スクリプトをページコードの`<head>`セクションに配置し、最も一般的なベンダー要件に準拠して同期的にロードされます。詳細については、[`utag.sync.js`の動作方法](https://docs.tealium.com/utag-sync/)を参照してください。
* **モバイルウェブビュー** (`mobile.html`)  
モバイルインストール用のテンプレートで、モバイルアプリがベンダータグをロードするために隠されたウェブビューとしてロードされます。詳細については、[クライアントサイド](https://docs.tealium.com/ja/platforms/getting-started-mobile/client-side/#mobile)を参照してください。

### 同意管理

これらのテンプレートは、同意管理機能で使用されます。詳細については、[同意管理について](https://docs.tealium.com/about-consent-management/)を参照してください。

* Dom Ready (`cmDomready`)
* General (`cmGeneral`)
* Show Explicit (`cmShowexplicit`)
* Show Preferences (`cmShowpreferences`)
* Do Not Sell Banner (`cmShowDNSBanner`)
* Do Not Sell Preferences (`cmDoNotSell`)
* Do Not Sell Prompt (`cmShowDNSPrompt`)
* Consent Logging - Accept/Decline Consent (`fullConsentEventHandler`)
* Consent Logging - Grant Partial Consent (`partialConsentEventHandler`)

### 同意統合

これらのテンプレートは、同意統合で使用されます。詳細については、[同意統合について](https://docs.tealium.com/about-consent-integrations/)を参照してください。

* Framework (`utcm_framework`): Tealium iQの同意強制フレームワークです。
* 統合テンプレート: すべての統合テンプレートは、同意統合ダッシュボードに表示される統合名、テンプレート名（OneTrust、Usercentrics、Customなど）、およびそのテンプレートのインスタンスの内部Tealium IDによって識別されます。例：`同意統合 - テスト統合 (onetrust) UID:utcm_e9582a8f-40fd-49ae-9819-fb2721f5547e`
  * Didomi
  * OneTrust
  * OptOut Cookie + GPC
  * Usercentrics
  * Custom

### マーケットプレイスタグ

すべてのマーケットプレイステンプレートは、マーケットプレイスに表示されるベンダー名、タグ構成で入力されたタグ名、およびタグUIDによって識別されます。

例：`Twitter Conversions: Twitter Conversions (Retargeting): Tag UID: 2042
`

## テンプレートステータスチェッカー

**テンプレートステータスチェッカー**ツールは、各テンプレートを利用可能な最新のシステムバージョンと比較します。詳細については、[テンプレートステータスチェッカーについて](https://docs.tealium.com/template-status-checker/)を参照してください。

## テンプレートへのアクセス

テンプレートにアクセスするための以下の方法があります：

* **管理メニュー**  
管理メニューで**テンプレートの管理**をクリックします。  
この方法では、プロファイル内のすべてのテンプレートを閲覧し、ドロップダウンリストからすぐにアクセスできます。
* **タグ構成**  
タグ構成画面で**詳細構成**エリアを展開し、**テンプレートの編集**をクリックします。この方法では、そのタグのテンプレートに直接アクセスします。
* **テンプレートステータスチェッカー**  
管理メニューで**テンプレートステータスチェッカー**をクリックし、レポート内のテンプレートをクリックします。  
この方法では、テンプレートのステータスレポートが表示されます。レポートには各テンプレートへのリンクが含まれています。  
詳細については、[テンプレートステータスチェッカーについて](https://docs.tealium.com/template-status-checker/)を参照してください。

## テンプレートのマージ動作

タグテンプレートは標準的なマージ動作に従いません。一つのバージョンを別のバージョンにマージする際、アクティブなバージョンのタグテンプレートが優先されます。マージされたバージョンからのタグテンプレートの変更は破棄されます。別のバージョンのタグテンプレートをマージしたい場合は、そのバージョンに切り替えてから、元のバージョンにタグテンプレートをマージしてください。

バージョンのマージについての詳細は、[merging-versions](https://docs.tealium.com/merging-versions/)を参照してください。