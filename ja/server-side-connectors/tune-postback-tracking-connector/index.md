---
title: TUNEポストバックトラッキングコネクター構成ガイド
description: この記事では、TUNEポストバックトラッキングコネクターの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/tune-postback-tracking-connector/
---
## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| コンバージョンポストバックを送信 | ✗ | ✓ |
| イベントポストバックを送信 | ✗ | ✓ |

## 構成

コネクターマーケットプレイスに移動し、新しいコネクターを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクターを追加したら、次の項目を構成します。

* **Network ID**：TUNEクライアント識別子。

コネクターを構成したら、**完了**をクリックします。

## アクション構成 - パラメーターとオプション

以下のセクションでは、各アクションでサポートされているパラメーターについて説明します。

### アクション - コンバージョンポストバックを送信

#### コンバージョンパラメーター

| **パラメーター** | **説明** |
| --- | --- |
| Transaction ID | （必須）TUNEトランザクションID |
| adv sub | 広告主のサブID（1～5）。最大5つの値を含む配列、または単一の文字列属性か数値属性をこのパラメーターに割り当てます。詳細については、[TUNE：広告主サブID](https://support.tune.com/hc/en-us/articles/1500008231142-Advertiser-Sub-Ids)を参照してください。|
| adv unique | 広告主固有のサブID（1～5）。最大5つの値を含む配列、または単一の文字列属性か数値属性をこのパラメーターに割り当てます。 |
| aff ID | オファーを宣伝するパートナーのID |
| Promo Code | プロモーションコード |
| Amount | コンバージョンによって発生した売上額 |
| Conversion Unique ID | 有効期限のない一意のID |
| Goal ID | オファーの目標ID |
| Goal Ref | オファーの目標参照ID。このパラメーターがアトリビューションに影響するのは、目標IDが指定されていない場合のみです。 |
| Offer ID | TUNE内のオファーID |
| Payout | パブリッシャーに対して指定されたオファー報酬額 |
| Revenue | 広告主からの指定されたオファー収益 |
| Security Token | コンバージョン認証に使用する広告主固有のトークン文字列 |
| Status | コンバージョンステータス。使用できる値は、`approved`、`rejected`、または`pending`です。 |

#### モバイルパラメーター

| **パラメーター** | **説明** |
| --- | --- |
| Google aid | Google Playストアのアプリについて、クリックをインストールに紐付けるために使用されるGoogle Android広告識別子 |
| Google aid sha1 | Google Android広告IDのSHA1ハッシュ |
| iOS ifa | Apple iOS広告識別子（iOS 6以降） |
| iOS ifa sha1 | iOSデバイスのIFA IDのSHA1ハッシュ |
| iOS ifv | Apple iOSベンダー識別子（iOS 6以降） |
| UNID | 不明なモバイルデバイス識別子を包括的に扱うための識別子 |
| User ID | アプリ開発者によって生成されたアプリケーション固有のユーザーID |
| Windows aid | Windowsデバイスの広告識別子 |
| Window aid sha1 | Windows広告IDのSHA1ハッシュ |

### アクション - イベントポストバックを送信

#### コンバージョンパラメーター

| **パラメーター** | **説明** |
| --- | --- |
| Goal Name | （必須）イベント名 |
| adv ID | （必須）広告主ID |
| adv sub | 広告主のサブID（1～5）。最大5つの値を含む配列、または単一の文字列属性か数値属性をこのパラメーターに割り当てます。詳細については、[TUNE：広告主サブID](https://support.tune.com/hc/en-us/articles/1500008231142-Advertiser-Sub-Ids)を参照してください。|
| adv unique | 広告主固有のサブID（1～5）。最大5つの値を含む配列、または単一の文字列属性か数値属性をこのパラメーターに割り当てます。 |
| Transaction ID | TUNEトランザクションID |
| aff ID | オファーを宣伝するパートナーのID |
| Promo Code | プロモーションコード |
| Amount | コンバージョンによって発生した売上額 |
| Conversion Unique ID | 有効期限のない一意のID |
| Goal ID | オファーの目標ID |
| Goal Ref | オファーの目標参照ID。このパラメーターがアトリビューションに影響するのは、目標IDが指定されていない場合のみです。 |
| Offer ID | TUNE内のオファーID |
| Payout | パブリッシャーに対して指定されたオファー報酬額 |
| Revenue | 広告主からの指定されたオファー収益 |
| Security Token | コンバージョン認証に使用する広告主固有のトークン文字列 |
| Status | コンバージョンステータス。使用できる値は、`approved`、`rejected`、または`pending`です。 |

#### モバイルパラメーター

| **パラメーター** | **説明** |
| --- | --- |
| Google aid | Google Playストアのアプリについて、クリックをインストールに紐付けるために使用されるGoogle Android広告識別子 |
| Google aid sha1 | Google Android広告IDのSHA1ハッシュ |
| iOS ifa | Apple iOS広告識別子（iOS 6以降） |
| iOS ifa sha1 | iOSデバイスのIFA IDのSHA1ハッシュ |
| iOS ifv | Apple iOSベンダー識別子（iOS 6以降） |
| UNID | 不明なモバイルデバイス識別子を包括的に扱うための識別子 |
| User ID | アプリ開発者によって生成されたアプリケーション固有のユーザーID |
| Windows aid | Windowsデバイスの広告識別子 |
| Window aid sha1 | Windows広告IDのSHA1ハッシュ |