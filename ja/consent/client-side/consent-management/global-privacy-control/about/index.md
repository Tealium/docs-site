---
title: グローバルプライバシーコントロール（GPC）について
description: この記事では、ユーザーが一般的に個人データの販売または共有に同意しないことを示すことができる提案されたブラウザ標準であるグローバルプライバシーコントロール（GPC）について説明します。
url: https://docs.tealium.com/ja/consent/client-side/consent-management/global-privacy-control/about/
---
[グローバルプライバシーコントロール](https://globalprivacycontrol.org/)（GPC）は、ユーザーがドメイン全体で一般的に個人データの販売または共有に同意しないことを示すことができる提案されたブラウザ標準です。

多くの点で、GPCは[Do Not Track](https://en.wikipedia.org/wiki/Do_Not_Track)に似ています。どちらもブラウザレベルのブール構成で、ユーザーが訪れる各ウェブサイトで手動でオプトアウトする必要を省くように設計されています。Do Not TrackとGPCシグナルの[主な違い](https://iapp.org/news/a/is-gpc-the-new-do-not-track/)は、カリフォルニア州の司法長官が、GPCはCCPAまたはCPRAの対象となる企業によって尊重されなければならないことを明確に示している点です。

## なぜ存在するのか？

GPCは、消費者が一般的に個人データの販売および共有に反対することを示す持続的なクロスサイトシグナルを提供することを目的としています。提案された標準は、ユーザーが訪れる各サイトでデータの販売に対して繰り返し反対する必要がないようにすることを望んでいます。[仕様](https://privacycg.github.io/gpc-spec/#introduction)からの引用：

> 複数の法的枠組みが存在し、これからも増える予定ですが、これらの枠組みの中で人々はプライバシーを保護するよう要求する権利を持っています。これには、データが販売または共有されないよう要求することも含まれます。しかし、訪れる各サイトごとに手動で自分の権利を表明することは非現実的です。

カリフォルニア州の司法長官は、GPCのようなシグナルを支持することを[明確にしています](https://oag.ca.gov/sites/all/files/agweb/pdfs/privacy/ccpa-fsor.pdf) - 企業がオプトアウトとしてシグナルを尊重することが期待されています：

> 消費者がウェブサイトを訪れるたびに個人情報が収集および販売される頻度と容易さを考えると、消費者は同様に容易な方法でグローバルにオプトアウトを要求することができるべきです。この規制は、消費者に個々のウェブサイトを訪れるたびに、新しいブラウザーや新しいデバイスを使用するたびに、各企業と個別の要求を行う代わりに、個人情報の販売をオプトアウトするグローバルな選択肢を提供します。

詳細については、[GPC仕様提案](https://privacycg.github.io/gpc-spec/#introduction)をご覧ください。


## GPCシグナルはどのように解釈されるべきか？

カリフォルニア州の司法長官と[セフォラの和解](https://oag.ca.gov/news/press-releases/attorney-general-bonta-announces-settlement-sephora-part-ongoing-enforcement)は、カリフォルニアの規制の対象となる企業がCCPA/CPRAの目的でGPCシグナルをオプトアウトとして実施することが期待されていることを明確にしています。

GPCシグナルのGDPR / ePrivacyに対する適切な解釈は明確ではありませんが、現在最終交渉中のePrivacy規制に関しては、今後の明確化が期待されています。それが法的に拘束力を持つかどうか、またどの形であるかは確定していませんが、その目的のためにすでに[標準](https://noyb.eu/en/new-browser-signal-could-make-cookie-banners-obsolete)が提案されています。

最終的には、適用される規制のどの解釈があなたのビジネスに最適かを決定するのはあなたのビジネス次第です。

## TealiumでGPCシグナルをどのように尊重するか？

お客様のニーズと要件は幅広いため、当社のプラットフォーム全体でお客様が構築できる柔軟な基盤を提供することを目指しています。

TealiumのGPCサポートについての詳細は、[クライアントサイドグローバルプライバシーコントロール](https://docs.tealium.com/client-side-global-privacy-control/)および[サーバーサイドグローバルプライバシーコントロール](https://docs.tealium.com/server-side-global-privacy-control/)をご覧ください。

## シグナルはどのように公開されていますか？

GPCを有効にするために、[対応するブラウザ](https://globalprivacycontrol.org/orgs)はDOM内でグローバルブール値（オプトアウトの場合は`true`）を公開します：

```javascript
navigator.globalPrivacyControl // オプトアウトの場合はtrueになります
```

そして、すべての発信リクエストにヘッダーを構成します（オプトアウトの場合は`1`）：

```
Sec-GPC: 1
``` 

## GPCサポートをどのように示すことができますか？

ウェブサイトは、提案された標準によって提供される[メカニズム](https://privacycg.github.io/gpc-spec/#gpc-support-resource)を使用して、GPCをサポートしていることを明示的に示すことができます。

> ウェブサイトは、GPCをサポートしていることを示すために、`.well-known` URLでリソースを生成することができます。GPCサポートリソースの目的は、サイトがグローバルプライバシーコントロールをサポートしていることを伝えることです。デフォルトでは、オリジンのサポートは不明です。

このファイルはサイト所有者によってホストされる場合がありますが、Tealiumは関連するサービスやホスティングを提供していません。