---
title: Friendbuyコネクタ構成ガイド
description: この記事では、Friendbuyコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/friendbuy-connector/
---
## コネクタアクション

| **アクション名** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| Email Opt Out   | ✓                  | ✓               |
| Send Email      | ✓                  | ✓               |
| Post a Purchase | ✗                  | ✓               |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要][Connector Overview](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIアクセスキー**  
APIアクセスキーの取得方法については、次を参照してください：[開発者ドキュメント：セキュリティ](https://developers.friendbuy.com/#security&quot;&gt;https://developers.friendbuy.com/#security)。
* **APIシークレットキー**  
APIシークレットキーの取得方法については、次を参照してください：[開発者ドキュメント：セキュリティ](https://developers.friendbuy.com/#security&quot;&gt;https://developers.friendbuy.com/#security)。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - Email Opt Out

#### パラメータ

| **パラメータ** | **説明**                                                                                                                                                                                                                                                                                          |
|:--------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Email Address | <ul><li>オプトアウトリストに追加するメールアドレス。</li><li>単一のメールアドレスのみ許可されます。</li><li>このエンドポイントに関する詳細情報は、次を参照してください：[Friendbuyのドキュメンテーション](https://developers.friendbuy.com/#span-class-method-post-post-span-span-class-restofendpoint-opt_outs-emails-span)。</li></ul> |

### アクション - Send Email

#### パラメータ

| **パラメータ**     | **説明**                                                                                                                                                                                                                                                                                  |
|:------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Email Address     | <ul><li>メールを送信する先。</li><li>単一のメールアドレスのみ許可されます。</li><li>このエンドポイントに関する詳細情報は、次を参照してください：[Friendbuyのドキュメンテーション](https://developers.friendbuy.com/#span-class-method-post-post-span-span-class-restofendpoint-communication_emails-span)。</li></ul> |
| Email Template ID | <ul><li>使用する通信メールテンプレートのID。</li></ul>                                                                                                                                                                                                                                 |
| Coupon Bank ID    | <ul><li>使用するクーポンバンクのID。</li></ul>                                                                                                                                                                                                                                                  |

### アクション - Post a Purchase

#### パラメータ

| **パラメータ**         | **説明**                                                                                                                                                                                                                                                                                                                                                                         |
|:----------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Order ID              | <ul><li>購入のためのユニークな注文ID。</li><li>この注文IDが以前に使用されていた場合、リクエストは失敗し、新しい購入（および新しいコンバージョン）は作成されません。</li><li>このエンドポイントに関する詳細情報は、次を参照してください：[Friendbuyのドキュメンテーション](https://developers.friendbuy.com/#span-class-method-post-post-span-span-class-restofendpoint-purchases-span)。</li></ul> |
| Referral Code         | <ul><li>友人が購入するために紹介したRefcode。</li><li>Coupon Codeが存在しない場合は必須。</li><li>Referral CodeとCoupon Codeの両方が提供された場合、Referral Codeが優先されます。</li></ul>                                                                                                                                                                |
| Coupon Code           | <ul><li>友人がマーチャントに購入するために持ってきたクーポンコード。Referral Codeが存在しない場合は必須。</li></ul>                                                                                                                                                                                                                                                   |
| Order Amount          | <ul><li>注文の金額。</li></ul>                                                                                                                                                                                                                                                                                                                                                  |
| Order Email           | <ul><li>注文に関連付けられたメールアドレス。</li></ul>                                                                                                                                                                                                                                                                                                                              |
| New Customer          | <ul><li>購入が新規（初回）の顧客によって行われたかどうか。</li><li>可能な値：`true`または`false`。</li><li>Friendbuyでは、報酬の基準の一つとして`新規顧客でなければならない`と指定できるため、報酬の適格性をチェックするために使用されます。</li></ul>                                                                                                       |
| Customer ID           | <ul><li>顧客に割り当てたID（Friendbuyが内部的に割り当てるIDとは異なります）。</li></ul>                                                                                                                                                                                                                                                                            |
| Customer First Name   |                                                                                                                                                                                                                                                                                                                                                                                         |
| Customer Last Name    |                                                                                                                                                                                                                                                                                                                                                                                         |
| Customer Email        | <ul><li>顧客に関連付けられたメールアドレス。</li></ul>                                                                                                                                                                                                                                                                                                                           |
| Stripe Customer ID    | <ul><li>Stripeの顧客ID。</li></ul>                                                                                                                                                                                                                                                                                                                                         |
| Chargebee Customer ID | <ul><li>Chargebeeの顧客ID</li></ul>                                                                                                                                                                                                                                                                                                                                       |
