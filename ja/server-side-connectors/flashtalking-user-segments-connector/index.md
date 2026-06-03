---
title: Flashtalkingユーザーセグメントコネクタ構成ガイド
description: Flashtalkingコネクタを使用して、Flashtalking Pixel Managerで作成したセグメントにユーザーを追加できます。これらのセグメントは、Campaign ManagerまたはCreative ManagerインターフェースのDecision TreeまたはHedgeインポートを使用してターゲットにすることができます。
url: https://docs.tealium.com/ja/server-side-connectors/flashtalking-user-segments-connector/
---
詳細情報については、Flashtalkingアカウントにログインし、[Flashtalking: Tealium Integration.](https://flashtalkingsupport.zendesk.com/hc/en-us/articles/360043723153-Tealium-Integration)にアクセスしてください。

## コネクタアクション

| **アクション名** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| ユーザーをセグメントに追加 | ✓ | ✓ |
| ユーザーをセグメントから削除 | ✓ | ✓ |
| ユーザーをすべてのセグメントから削除 | ✓ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[Connector Overview](/ja/server-side/connectors/manage/)記事を参照してください。

コネクタを追加した後、次の構成を構成します：

*   **広告主ID:** Flashtalking Pixel Manager内で広告主IDを見つけます。
*   **ユーザー名:** Flashtalkingハブにログインするために使用するユーザー名を入力します。
*   **パスワード:** Flashtalkingハブにログインするために使用するパスワードを入力します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザーをセグメントに追加

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| DAID | Android広告ID。 |
| IDFA | Apple広告ID。 |
| UID | クッキーシンクからのユニークID。 |
| セグメント | セグメント文字列によってターゲットセグメントを識別します。単一のセグメントまたはカンマで区切られたセグメントのリストを渡します。セグメントのリストを渡す場合、ブラケット &#34;`[]`&#34; を含めないでください。 |

### アクション - ユーザーをセグメントから削除

### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| DAID | Android広告ID。 |
| IDFA | Apple広告ID。 |
| UID | クッキーシンクからのユニークID。 |
| セグメント | セグメント文字列によってターゲットセグメントを識別します。単一のセグメントまたはカンマで区切られたセグメントのリストを渡します。セグメントのリストを渡す場合、ブラケット &#34;`[]`&#34; を含めないでください。 |

### アクション - ユーザーをすべてのセグメントから削除

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| DAID | Android広告ID。 |
| IDFA | Apple広告ID。 |
| UID  | クッキーシンクからのユニークID。 |
