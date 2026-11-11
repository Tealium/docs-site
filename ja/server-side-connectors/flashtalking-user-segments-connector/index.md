---
title: Flashtalkingユーザーセグメントコネクタ構成ガイド
description: Flashtalkingコネクタを使用して、Flashtalking Pixel Managerで作成したセグメントにユーザーを追加できます。これらのセグメントは、Campaign ManagerまたはCreative Managerのインターフェイスで、Decision TreeまたはHedgeのインポートを使用してターゲットにできます。
url: https://docs.tealium.com/ja/server-side-connectors/flashtalking-user-segments-connector/
---
詳細については、Flashtalkingアカウントにログインし、[Flashtalking：Tealiumインテグレーション](https://flashtalkingsupport.zendesk.com/hc/en-us/articles/360043723153-Tealium-Integration)を参照してください。

## コネクタアクション

| **アクション名** | **訪問プロファイル** | **イベントデータ** |
| --- | --- | --- |
| ユーザーをセグメントに追加 | ✓ | ✓ |
| ユーザーをセグメントから削除 | ✓ | ✓ |
| ユーザーをすべてのセグメントから削除 | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタの概要](https://docs.tealium.com/ja/server-side/connectors/manage/)を参照してください。

コネクタを追加した後、次の構成を行います。

*   **広告主ID：** Flashtalking Pixel Managerで広告主IDを確認します。
*   **ユーザー名：** Flashtalkingハブへのログインに使用するユーザー名を入力します。
*   **パスワード：** Flashtalkingハブへのログインに使用するパスワードを入力します。

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — ユーザーをセグメントに追加

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| DAID | Android広告ID。 |
| IDFA | Apple広告ID。 |
| UID | Cookie同期から取得した一意のID。 |
| Segment(s) | セグメント文字列を使用して対象セグメントを指定します。単一のセグメント、またはカンマ区切りのセグメントリストを渡します。セグメントのリストを渡す場合は、角括弧「`[]`」を含めないでください。 |

### アクション — ユーザーをセグメントから削除

### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| DAID | Android広告ID。 |
| IDFA | Apple広告ID。 |
| UID | Cookie同期から取得した一意のID。 |
| Segment(s) | セグメント文字列を使用して対象セグメントを指定します。単一のセグメント、またはカンマ区切りのセグメントリストを渡します。セグメントのリストを渡す場合は、角括弧「`[]`」を含めないでください。 |

### アクション — ユーザーをすべてのセグメントから削除

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| DAID | Android広告ID。 |
| IDFA | Apple広告ID。 |
| UID  | Cookie同期から取得した一意のID。 |