---
title: クライアント側グローバルプライバシーコントロール（GPC）
description: この記事では、ユーザーが個人データの販売または共有をオプトアウトできるブラウザ標準であるグローバルプライバシーコントロール（GPC）に対するTealiumのクライアント側サポートについて説明します。
url: https://docs.tealium.com/ja/consent/client-side/consent-management/global-privacy-control/client-side-support-gpc/
---
[Global Privacy Control](https://globalprivacycontrol.org/)（GPC）は、ブラウザレベルで個人データの販売または共有をオプトアウトするためのグローバルな方法を提供します。GPCについての詳細は、[グローバルプライバシーコントロールについて](https://docs.tealium.com/about-global-privacy-control/)をご覧ください。

お客様のニーズと要件は幅広いため、お客様が構築できる柔軟な基盤を提供することを目指しています。


<blockquote>
この記事では、GPCに対するTealiumのクライアント側サポートについて説明します。サーバー側のサポートについては、[サーバー側グローバルプライバシーコントロール](https://docs.tealium.com/server-side-global-privacy-control/)をご覧ください。
</blockquote>


## クライアント側サポート

GPCシグナルは単純なブール値であるため、CCPAや類似のオプトアウト型規制が現在最も関連性が高く、受け入れられています（詳細は[グローバルプライバシーコントロールについて](https://docs.tealium.com/about-global-privacy-control/)を参照）。

厳格な解釈によると、GPCシグナルが`true`に構成されている場合、Tealium iQは全くロードされないという判断になるかもしれません。Tealium iQに実装されているすべてのタグがデータを販売または共有している場合、これが正しい選択かもしれません。

これは、プリローダーJavaScript拡張機能で実装できます：

```javascript
if (navigator.globalPrivacyControl === true) {
    // Tealium iQ not loaded due to Global Privacy Control opt-out signal
    window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
    window.utag_cfg_ovrd.noload = true;
}
```

### オプトインモデル（GDPRのような）

GPCシグナルはオプトアウトモデル（CCPA/CPRAのような）用に設計されており、オプトインモデル（GDPRのような）には適していません。Tealiumのオプトイン同意管理モジュール（[明示的同意プロンプトマネージャー]()および[同意構成マネージャー]()）は、標準でGPC関連のオプトアウトロジックを含んでいません。

お客様のニーズは多岐にわたり、当社の同意管理モジュールはカスタマイズ可能であり、必要に応じてGPCロジックを追加して、お客様の組織のニーズや解釈をサポートするよう設計されています。

### オプトアウトモデル（CCPA/CPRAのような）

#### クライアント側同意統合 - オプトアウトクッキー + GPC統合

**GPCサポートを含むクッキーベースの強制を必要とする既にアクティブなオプトアウトフォームを持つお客様向け。**

[クライアント側同意統合](https://docs.tealium.com/about-consent-integrations/)は、CCPA/CPRAが要求するシンプルなオプトアウトモデルをサポートします。

この統合は、GPCオプトアウトシグナルまたは顧客指定のオプトアウトクッキーが見つかった場合にユーザーがオプトアウトしたと仮定します。同意統合がGPCをサポートする方法についての詳細は、を参照してください。

#### クライアント側同意統合 - GPCサポート付きCMP

**GPCサポートを持つ既にアクティブな同意管理プラットフォーム（CMP）を持ち、強制のみが必要なお客様向け。**

[クライアント側同意統合](https://docs.tealium.com/about-consent-integrations/)は、GPCサポートを提供するCMPのリストを拡大しています。これらのCMPは通常、意思決定のキャプチャの一部としてGPCサポートを提供し、Tealium iQによる同意統合を通じて強制されます。追加のロジックや解釈は必要ありません。お使いのCMPがまだサポートされていない場合は、カスタム統合も利用可能です。

#### クライアント側同意管理 - オプトアウトプライバシーバナーとポップアップ

**Tealium iQで同意管理を完全に実装したいお客様向け。**

`cmDoNotSell v1.2.0`のリリース時点で、以下の図からの論理フローが[CCPAプライバシーバナーとポップアップ](https://docs.tealium.com/about-ccpa-privacy-banner-and-popup/)に実装されています。

![](https://docs.tealium.com/images/guides/server-side/global-privacy-control-consent-flow.png)

この挙動は、ユーザーとビジネスのニーズに合った同意管理ソリューションを構築するための出発点として機能します。具体的な挙動については法務チームと相談し、ユーザーに明確に伝えてください。`cmDoNotSell`テンプレートを編集してこの挙動を変更または削除します。

#### GPCサポート付きCookieConsent

**グローバルプライバシーコントロールシグナルをCookieConsent統合に統合したいお客様向け。**

詳細については、をご覧ください。