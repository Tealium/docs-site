---
title: Tealium + Quantum Metric 統合ガイド
description: この記事では、Tealium iQ タグ管理で Quantum Metric タグを構成し、Quantum Metric タグが Tealium AudienceStream にセッションリプレイURLを送信するようにすることで、Tealium と Quantum Metric を最大限に活用する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-quantum-metric-integration-guide/
---Tealium と Quantum Metric 間の双方向統合により、重要な顧客セグメントがデジタル製品をどのように体験しているかについての洞察が深まります。

 `utag` バージョン 4.50 以降を使用する場合、`utag.js` の [`always_set_v_id` 構成]()を `true` に構成する必要があります。この構成により、訪問IDがクッキー同期のために利用可能になります。詳細については、[utag 4.50 リリースノート]()および [utag 4.50&#43; へのアップグレード時の tealium_visitor_id の考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-) を参照してください。

## 前提条件

* **Tealium**
    * iQ タグ管理 (必須)
    * AudienceStream (推奨)  
双方向統合から最大の価値を得るために。
* **Quantum Metric**
    * ネイティブまたはWebのプラットフォーム (必須)

## 動作原理

Quantum Metric はデジタルエクスペリエンスインテリジェンスプラットフォームであり、すべてのデバイスにわたるすべての顧客の相互作用に対する前例のない可視性を提供し、データ駆動の意思決定を迅速化します。技術的および行動的な洞察を自動的に優先するように構築されたこのプラットフォームは、組織の顧客体験（CX）の整合を促進することで、企業のデジタル変革を推進します。パフォーマンスとセキュリティは Quantum Metric の基盤であり、顧客がリアルタイムでユーザーの洞察を安全かつ大規模に得ることを可能にします。

詳細については、[Tealium と Quantum Metric のパートナーシップ概要](https://tealium.com/technology-partner/quantum-metric/)をご覧ください。

## タグの構成

Tealium AudienceStream が Quantum Metric Replay URL を受信するように構成する前に、まず Quantum Metric タグを追加して構成する必要があります。

詳細については、[Quantum Metric タグ]()を参照してください。

### AudienceStream を有効にする

Quantum Metric から Tealium へ送信したいターゲット行動や体験を決定するために、Quantum Metric のクライアントサービスマネージャーに相談してください。

AudienceStream が Quantum Metric からのデータを受信するように構成します：

1. iQ タグ管理で Quantum Metric タグに移動します。
1. 詳細を展開し、**編集**をクリックします。
1. Send Replay URL フィールドを **True** に構成します。  
      ![](/images/tech-partners/quantum-metric-tag-configuration.jpg)
1. 次のフィールドを定義します：
      * タイムスタンプ
      * Tealium アカウント
      * Tealium プロファイル
1. **適用**をクリックします。
1. 変更を保存し、希望する環境に公開します。

### ライブイベントで表示

Quantum Metric タグが構成され、AudienceStream への Replay URL の送信が有効になった後、ライブイベントフィードで活動を確認できます。

ライブイベントで表示するには、次の手順を実行します：

1. 顧客データハブの左サイドバーで **イベントストリーム &amp;gt; ライブイベント** をクリックします。
1. `quantum_metric_replay_url` または `quantum_metric_user_id` を含むイベントをフィルタリングして、Quantum Metric のイベントを探します。  
    ![](/images/tech-partners/quantummetric-live-events.png)
1. これらのイベント属性を使用して、他の [AudienceStream 属性]()でプロファイルを豊かにします。