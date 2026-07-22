---
title: 公開について
url: https://docs.tealium.com/ja/iq-tag-management/save-publish/about-publishing/
---
公開は、保存プロセス中のオプションであり、追加のアクションです。変更を公開すると、アカウントプロファイルに関連するファイルが再生成され、現在の構成が含まれます。

## 公開のタイミング

Tealiumのコンテンツ配信ネットワーク（CDN）は、公開とテスト中の遅延を最小限に抑えるために、ファイルを即時に更新するように最適化されています。

Time-to-live（TTL）構成とブラウザによるキャッシュは、ブラウザが古いバージョンのファイルをロードする原因となります。これを解決するためには、ブラウザのキャッシュをクリアするか無効にします。Tealiumとブラウザキャッシュについての詳細は、[file-cache](https://docs.tealium.com/file-cache/)を参照してください。

#### 即時更新

公開後、以下のファイルはCDNを通じて即時に伝播します：

* `utag.js`
* `utag.#.js`

#### 最大5分後に更新

以下の項目の公開は、CDNを通じて伝播するのに最大5分かかります：

* `utag.sync.js`
* `.cn`および`.eu`ドメイン上の`utag.js`と`utag.#.js`ファイル
* ファーストパーティドメイン上の`utag.js`と`utag.#.js`ファイル



## 公開環境

公開環境は、製品および非製品サイトにインストールするためのユニバーサルタグ（`utag.js`）の別々のインスタンスを提供します。適切なリリースサイクルをサポートするための3つの公開環境があります：**Dev**、**QA**、および**Prod**。各環境は、異なるウェブサイト環境のための別々のファイルを使用します。別々の環境を使用することで、製品サイトに直接リリースする前に変更をテストすることができます。

ユニバーサルタグ（`utag.js`）の3つのインスタンスに対応する3つのデフォルトの公開環境があります：

*  **Dev**: `/utag/YOUR-ACCOUNT/YOUR-PROFILE/dev/utag.js`  
新しいタグと機能を開発するための環境。
*  **QA**: `/utag/YOUR-ACCOUNT/YOUR-PROFILE/qa/utag.js`  
テストと検証のための環境。
*  **Prod**: `/utag/YOUR-ACCOUNT/YOUR-PROFILE/prod/utag.js`  
ライブプロダクションサイトの環境。

例えば、Prod環境からのファイルは、製品サイトにインストールする必要があります：

```bash
https://tags.tiqcdn.com/utag/YOUR-ACCOUNT/main/prod/utag.js
```

QA環境からのファイルは、非製品サイト（QA/Stage）にインストールする必要があります：

```bash
https://tags.tiqcdn.com/utag/YOUR-ACCOUNT/main/qa/utag.js
```

追加の環境が必要な場合は、[カスタム公開環境](https://docs.tealium.com/custom-publish-environments/)を使用してください。
