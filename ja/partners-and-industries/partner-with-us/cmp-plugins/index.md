---
title: CMPプラグイン
description: Consent Management Platform（CMP）をTealium iQタグ管理と統合し、管理タグのプライバシー構成を強制する方法を学びます。
url: https://docs.tealium.com/ja/partners-and-industries/partner-with-us/cmp-plugins/
---


CMPプラグインは、Tealium拡張マーケットプレイスのベンダー固有のソリューションで、CMPインストールとTealium iQインストールを簡単に統合できます。

CMPプラグインは次の利点を提供します：

- 2つのソリューションを統合する時間を短縮するためのシンプルなインポートツール。
- CMPからの同意ステータスに基づいてタグを発行する堅牢な強制。
- CMPからの同意データのサーバーサイド配布。

## 仕組み

CMPプラグインは、CMPで構成されたデータ処理サービスとTealium iQで構成されたタグとの間にマッピングを作成します。プラグインは、通常はブックマークレットというヘルパーツールを提供し、CMPの構成をTealium iQに簡単にインポートし、各サービス名を1つ以上のタグにマップします。

マッピングが構成され、あなたのサイトにデプロイされると、管理されたタグはユーザーのCMPとのインタラクションに基づいて発行されます。

CMP統合には次の部分があります：

* **サービスマッピング**   
サービスマッピングは、CMPサービス名を管理タグと関連付けます。リンクされたタグは、関連付けられたCMPサービス名が同意された後にのみ発行されます。
* **データレイヤー統合**  
CMPからの同意ステータス変数が、各トラッキングコールの[data layer object](https://docs.tealium.com/ja/platforms/javascript/data-layer-object/)に追加されます。変数名は`<cmp name>_<variable name>`の形式です。例えば、Usercentricsからの同意されたサービス名の配列は`usercentrics_services_with_consent`になります。
    * `<cmp name>_services_with_consent` - 同意されたサービス名の配列。
    * `<cmp name>_consent_type` - `explicit`または`implicit`の同意タイプ。

## 要件

Tealium iQタグ管理と統合するためには、CMPで構成された各データ処理サービスに対して以下の同意ステータス情報が利用可能である必要があります。これらは通常、ページ内のグローバルJavaScript変数またはメソッドとしてアクセスされます：

* **サービス名** - 同意が適用されたサービスのユニークな名前。
* **同意ステータス** - サービスに対する同意のステータスで、`true`は同意が与えられたことを示し、`false`は同意が与えられていないことを示します。
* **同意方法タイプ** - 同意が得られた方法（`implicit`または`explicit`）。

## Tealiumに同意データを送信する

クライアントサイドで同意を収集し、強制するだけでなく、CMP統合はサーバーサイドコネクタを使用して他のベンダーに同意ステータスを配布することもできます。

CMPがWebhookコールバックをサポートしている場合、[HTTP API endpoint](https://docs.tealium.com/ja/platforms/http-api/endpoint/)に更新を送信することでTealiumとの統合を拡張できます。これらのイベントはサーバーサイドで処理され、Tealium EventStream、AudienceStream、およびDataAccessを使用して他のベンダーで活性化できます。

CMPがWebhooksをサポートしていない場合は、製品とエンジニアリングチームと協力して統合を正式化するためにTealiumに連絡してください。

## パートナーになる

あなたの技術を統合するために[お問い合わせください](https://tealium.com/tealium-partner-network/)。