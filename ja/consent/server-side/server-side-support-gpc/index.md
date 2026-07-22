---
title: サーバーサイドのグローバルプライバシーコントロール
description: この記事では、Tealiumのサーバーサイドでのグローバルプライバシーコントロール（GPC）のサポートについて説明します。GPCは、ユーザーが個人データの販売または共有からオプトアウトできる提案されたブラウザ標準です。
url: https://docs.tealium.com/ja/consent/server-side/server-side-support-gpc/
---
[グローバルプライバシーコントロール](https://globalprivacycontrol.org/)（GPC）は、ブラウザレベルで個人データの販売または共有からオプトアウトするためのグローバルな方法を提供します。GPCについての詳細は、[グローバルプライバシーコントロールについて](https://docs.tealium.com/about-global-privacy-control/)をご覧ください。

お客様のニーズと要件は幅広いため、お客様が構築できる柔軟な基盤を提供することを目指しています。


<blockquote>
この記事では、TealiumのサーバーサイドでのGPCのサポートについて説明します。クライアントサイドのサポートについては、[クライアントサイドのグローバルプライバシーコントロール](https://docs.tealium.com/client-side-global-privacy-control/)をご覧ください。
</blockquote>


## サーバーサイドのサポート
 
Tealiumのサーバーサイドの顧客は、グローバルプライバシーコントロールヘッダー（`Sec-GPC`）を含む各イベントに`global_privacy_control_opt_out`というイベントレベルの属性を追加できます。

`global_privacy_control_opt_out`属性の可能な値は、`true`（`Sec-GPC: 1`）または`false`（`Sec-GPC:0`）です。GPCヘッダーが受信イベントに存在しない場合、`global_privacy_control_opt_out`属性はペイロードで定義されません。GPCイベントレベルの属性は、追加された場合に適切に構成されます。

サーバーサイドのシグナルを使用するには、新しいイベント属性**ユニバーサル変数**を文字列またはブール値として追加します。その後、新しい属性は適切に訪問プロファイルに豊かにされ、[決定を実施する](https://docs.tealium.com/server-side-consent-management/)ための活性化ポイントで使用されます。