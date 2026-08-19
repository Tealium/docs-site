---
title: データサプライチェーンダッシュボード
description: データサプライチェーンダッシュボードは、カスタマーデータハブのデータサプライチェーンの包括的な概要を提供します。
url: https://docs.tealium.com/ja/server-side/getting-started/data-supply-chain-dashboard/
---
## 仕組み

このダッシュボードは、データフローを表すために3つのインタラクティブなパネルを表示します：

* **フィルター** - 製品と期間によってダッシュボードビューを調整します。
* **データフローサマリー** - データフローのサマリーメトリクスと重要なステータスアラートを確認します。
* **データフローの詳細** - 特定のコンポーネントを調査して、データコネクトと健康状態を確認します。

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-dashboard.png)

## データサプライチェーンのビュー

**データサプライチェーン** ダッシュボードビューは、選択された製品ビューと期間によって変わります。製品を選択し、ドロップダウンリストから期間を選択してください。

ほとんどのビューには以下の情報が含まれており、製品固有のセクションで説明されている違いがあります。

* **データソース** – データソースへのクイックリンク
* **受信イベント** – ライブイベントへのクイックリンク
* **検査されたイベント** – イベント仕様とイベントタイプのサマリーメトリクスへのクイックリンク

### 全製品

**全製品**の概要ビューから、概要に記載されている標準情報または以下のビューのいずれかを選択します：

* **トリガーされたアクション** – 成功したコネクタアクションと失敗したコネクタアクションの数を表示
* **コネクター** – EventStreamおよびAudienceStreamコネクタへのクイックリンク

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-all-products-view.png)

### EventStream

**EventStream**の概要ビューから、概要に記載されている標準情報または以下のビューのいずれかを選択します：

* **適用されたエンリッチメント** – 属性へのクイックリンク
* **アクティブなフィード** – フィードへのクイックリンク
* **EventStreamアクションのトリガー** – 成功したEventStreamアクションまたは失敗したEventStreamアクションの数を表示
* **EventStreamコネクター** – EventStreamコネクタへのクイックリンク

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-event-data-view.png)

### AudienceStream

**AudienceStream**の概要ビューから、概要に記載されている標準情報または以下のビューのいずれかを選択します：

* **訪問数** – 選択した期間の訪問数を表示
* **アクティブなオーディエンス** – オーディエンスへのクイックリンク
* **AudienceStreamアクションのトリガー** – 成功したAudienceStreamアクションまたは失敗したAudienceStreamアクションの数を表示
* **AudienceStreamコネクター** – AudienceStreamコネクタへのクイックリンク

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-customer-data-view.png)

### EventStore

**EventStore**の概要ビューから、概要に記載されている標準情報または以下のビューのいずれかを選択します：

* **EventStoreフィード** – フィードへのクイックリンク
* **S3へ送信されたイベント** – S3バケットに送信されたイベント数を表示

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-eventstore-view.png)

### EventDB

**EventDB**の概要ビューから、概要に記載されている標準情報または以下のビューのいずれかを選択します：

* **EventDBフィード** – フィードへのクイックリンク
* **Redshiftへ送信されたイベント** – Redshiftに送信されたイベント数を表示

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-eventdb-view.png)

### AudienceStore

**AudienceStore**の概要ビューから、**データソース**または以下のビューのいずれかを選択します：

* **アクティブなオーディエンス** – オーディエンスへのクイックリンク
* **S3へ送信された訪問** – S3バケットに送信された訪問数を表示

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-audiencestore-view.png)

### AudienceDB

**AudienceDB**の概要ビューから、**データソース**または以下のビューのいずれかを選択します：

* **アクティブなオーディエンス** – オーディエンスへのクイックリンク
* **RedShiftへ送信された訪問** – RedShiftに送信された訪問数を表示

![](https://docs.tealium.com/images/server-side/ss-data-supply-chain-audiencedb-view.png)

## 追加のビューとナビゲーション

このセクションでは、インターフェースの本体内で利用可能な追加のビューとインタラクションについて説明します。

### データフローと関係の表示

画面の下部にはデータの関係とデータフローが明確に表示されます。これらの関係とフローをすばやく確認し、関連するアイテムの詳細にドリルダウンして編集できます。

![](https://docs.tealium.com/images/server-side/e44f1444-fdc8-40f6-a6b1-2e181191468e-1-201-a.jpeg)

### 機能

**全製品**ビューは、画面の下部に作成された[機能]()とその状態のリストを表示します。


### 展開と折りたたみ

アイテムの詳細を展開または折りたたみます。


### 結果の並べ替え

上 (▲) または下 (▼) の矢印を使用して、量、アクションの成功、または失敗によって結果を並べ替えます。


### その他のオプション

その他のオプションアクションボタン (**︙**) をクリックして、データソース、コネクタ、またはイベントフィードを直接編集します。


### エラーと警告の表示

警告アイコンの上にポインタを置いてエラーメッセージまたは警告メッセージを表示し、**詳細を学ぶ**リンクをクリックして問題の解決方法について読みます。

