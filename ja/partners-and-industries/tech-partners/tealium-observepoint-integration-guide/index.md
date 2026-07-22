---
title: Tealium + ObservePoint 統合ガイド
description: この記事では、Tealium iQタグ管理アカウントにObservePointタグを構成し、TealiumのオーディエンスとバッジをObservePointに送信するように構成することで、TealiumとObservePointを最大限に活用する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-observepoint-integration-guide/
---
Tealium + ObservePointの統合は、分析プラットフォーム、パーソナライゼーションツールなど、すべてのデジタル資産にわたるチーム間の整合性とデータの整合性を確保します。この統合により、共同顧客は、トラッキングエラーを特定し解決するための自動ObservePointスキャンを更新時に有効化することができます。この統合により、時間を節約し、敏捷性を向上させ、分析やパーソナライゼーションに使用するデータが準拠しており一貫性があることを確認できます。

## 必要条件

ObservePointとTealiumの統合には以下が必要です：

* Tealium iQタグ管理
* ObservePoint WebAssurance
* ObservePoint AppAssurance

## 仕組み

Tealium Customer Data Hub (CDH)は、データの収集からエンリッチメント、そしてアクティベーションまで、顧客データのライフサイクル全体を管理するのに役立ちます。

* データ収集から始めて、Tealium iQタグ管理は、標準化されたベンダー非依存のデータレイヤーを使用して、他の統合システムと並行してObservePointのデプロイメントと関連データを管理することができます。
* Tealium Customer Data Platform (CDP)は、このデータ収集インフラストラクチャをデータソースとして使用し、包括的な顧客プロファイルを作成します。
* これらの顧客プロファイルは、ビジネスルールで構成され、統合ベンダーとのアクションをトリガーします。

ObservePointのWebAssuranceとAppAssurance製品は、データ収集技術を大規模にテストし、検証することで、正確なデータを確保します。

* Web AuditsとWeb Journeysは、独自の技術を使用して、あなたの分析実装をスキャンし、不正確さをチェックし、データ収集を脅かす可能性のあるエラーを警告します。
* これらの自動スキャンにより、分析QAテストをより効率的に監視し、スケールアップすることができ、データへの信頼性が向上します。
* Strala technologiesの取得により - Touchpoints、JourneyStream、Prism - ObservePointはさらに、データを事前に標準化し、オンラインとオフラインの顧客タッチポイントを収集し統一し、成長とROIの向上を促進する正確で行動可能な洞察を生成するのに役立ちます。

詳細については、[Tealium + ObservePoint Partnership Overview](https://tealium.com/technology-partner/observepoint/%20)を参照してください。

## 統合構成

以下のセクションには、成功した実装のための特定のTealium + ObservePoint構成手順についての追加情報が含まれています。

### Tealiumのテストにリモートファイルマッピングを使用する

ObservePoint Remote File Mappingを使用すると、大規模なテストを簡単に実行することができます。Remote File Mappingを使用すると、タグ管理の変更を本番環境に公開した場合にデータ品質がどのように影響を受けるかを確認することができます。これは、Tealium（または他のタグマネージャー）の実装に変更を加え、本番環境に公開することをためらっている場合に役立ちます。

詳細については、[ObservePoint: Using Remote File Substitutions to Test Tealium](https://help.observepoint.com/en/articles/9113442-using-file-substitutions-to-test-tealium)を参照してください。

### Tealiumデータオブジェクトの確認

Tealiumとの統合により、共同顧客は、utag.linkおよびutag.click関数内のデータオブジェクト（またはbオブジェクト）を確認することができます。例えば、e-commerceのAdd to Basketインタラクションで'size'オプションを正しく送信していることを確認したい場合などです。

* Tealium ObservePointタグの構成について学ぶには、[ObservePoint Data Layer Validator Tag Setup Guide](https://docs.tealium.com/observepoint-data-layer-validator-tag/)を参照してください。
* ObservePointで結果を見つける方法について詳しく知るには、[ObservePoint: Checking Tealium Data Objects](https://help.observepoint.com/en/articles/9113411-checking-tealium-data-objects)を参照してください。

## Tealium ObservePointトリガー

Tealium ObservePointトリガーを使用すると、Tealiumプロファイルに公開するたびに、ObservePoint AuditsとWeb Journeysのグループが自動的に実行されます。この機能は、ObservePointとTealiumの両方の顧客であるすべての組織で利用できます。

このトリガーの主な使用目的は、変更を迅速かつ大規模にテストし、更新をリリースした後に分析が正常に機能していることを確認することです。例えば、Tealium QAプロファイルに変更を公開するたびに、自動的に1,000ページのデータ品質をテストし、e-commerceファネルと顧客登録ファネルをテストしたい場合などです。

詳細については、[ObservePoint: Tealium ObservePoint Trigger](https://help.observepoint.com/en/articles/9113192-tealium-observepoint-trigger)を参照してください。
