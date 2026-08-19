---
title: Google Ad Manager オーディエンス統合コネクタ構成ガイド
description: Google Ad Manager オーディエンスリストに訪問を追加または削除するために、Publisher Provided IDs (PPIDs) を使用して Google Ad Manager オーディエンス統合コネクタを構成します。
url: https://docs.tealium.com/ja/server-side-connectors/google-ad-manager-audience-integration-connector/
---
Google Ad Manager オーディエンス統合コネクタは、Publisher Provided ID (PPID) を使用して公開社が訪問を Google Ad Manager ユーザーリストに追加できるようにします。その後、公開社は PPID を基に広告を配信し、最も価値のある顧客に似たオーディエンスとマッチングすることで新しいユーザーをターゲットにできます。詳細については、[Google Ad Manager ヘルプ: 公開社提供の識別子について](https://support.google.com/admanager/answer/2880055?hl=ja)をご覧ください。

## 前提条件

* Google Ad Manager の **Linked Accounts** セクションで Tealium とリンクします。
* [Google Ad Manager 360 Audience Pixel タグ](https://docs.tealium.com/google-ad-manager-360-audience-pixel-tag/) または [Google Publisher タグ](https://docs.tealium.com/google-publisher-tag/) を使用して、ログインユーザーに対してクライアントサイドで PPID を生成して送信します。
* コネクタで使用するために Tealium 属性として PPID を構成します。

## API 情報

このコネクタは以下のベンダー API を使用します：

* API 名: Google Data Manager API
* API バージョン: v1
* API エンドポイント: `https://datamanager.googleapis.com`

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| オーディエンスリストに追加 | ✓ | ✓ |
| オーディエンスリストから削除 | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタの追加方法についての一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **Customer ID**.
(必須) Ad Manager UI で Tealium にリンクされたアカウントのカスタマー ID。Ad Manager で **ツールと構成 > リンクされたアカウント** に移動して Tealium へのリンクを作成します。

## アクション

次のセクションでは、各アクションのサポートされるパラメータをリストアップします。

### オーディエンスリストに追加

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数: 100,000
* 最古のリクエストからの最大時間: 1440 分
* リクエストの最大サイズ: 50 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| オーディエンスリスト | オーディエンスリストを選択します。<br>注意: コネクタを使用して作成されたリストのみが利用可能です。 |
| Publisher Provided ID | (必須) 単一の英数字または UUID HEX 値、または値の配列。各値は 32 から 150 文字の間でなければなりません。 |

### オーディエンスリストから削除

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数: 100,000
* 最古のリクエストからの最大時間: 1440 分
* リクエストの最大サイズ: 50 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| オーディエンスリスト | オーディエンスリストを選択します。<br>注意: コネクタを使用して作成されたリストのみが利用可能です。 |
| Publisher Provided ID | (必須) 単一の英数字または UUID HEX 値、または値の配列。各値は 32 から 150 文字の間でなければなりません。 |

## 同意

**オーディエンスリストに追加** などのアクションでは、コネクタは自動的に `adUserData` と `adPersonalization` を `GRANTED` として送信します。オーディエンスロジックを実装して、同意した訪問のみがユーザーリストに追加されるようにします。同意がない訪問の場合は、**オーディエンスリストから削除** アクションを使用してユーザーリストから削除します。

## ヒントとトラブルシューティング

* コネクタが PPID を受け取るようにするためには、コネクタアクションに使用されるイベントフィードまたはオーディエンス構成にロジックを含めてください。このロジックは `MISSING_USER_IDENTIFIER` エラーを避けるのに役立ちます。