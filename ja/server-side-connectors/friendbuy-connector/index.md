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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要][Connector Overview]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIアクセスキー**  
APIアクセスキーの取得方法については、次を参照してください：[開発者ドキュメント：セキュリティ](https://developers.friendbuy.com/#security&amp;quot;&amp;gt;https://developers.friendbuy.com/#security)。
* **APIシークレットキー**  
APIシークレットキーの取得方法については、次を参照してください：[開発者ドキュメント：セキュリティ](https://developers.friendbuy.com/#security&amp;quot;&amp;gt;https://developers.friendbuy.com/#security)。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - Email Opt Out

#### パラメータ

| **パラメータ** | **説明**                                                                                                                                                                                                                                                                                          |
|:--------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Email Address | &lt;ul&gt;&lt;li&gt;オプトアウトリストに追加するメールアドレス。&lt;/li&gt;&lt;li&gt;単一のメールアドレスのみ許可されます。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、次を参照してください：[Friendbuyのドキュメンテーション](https://developers.friendbuy.com/#span-class-method-post-post-span-span-class-restofendpoint-opt_outs-emails-span)。&lt;/li&gt;&lt;/ul&gt; |

### アクション - Send Email

#### パラメータ

| **パラメータ**     | **説明**                                                                                                                                                                                                                                                                                  |
|:------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Email Address     | &lt;ul&gt;&lt;li&gt;メールを送信する先。&lt;/li&gt;&lt;li&gt;単一のメールアドレスのみ許可されます。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、次を参照してください：[Friendbuyのドキュメンテーション](https://developers.friendbuy.com/#span-class-method-post-post-span-span-class-restofendpoint-communication_emails-span)。&lt;/li&gt;&lt;/ul&gt; |
| Email Template ID | &lt;ul&gt;&lt;li&gt;使用する通信メールテンプレートのID。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                 |
| Coupon Bank ID    | &lt;ul&gt;&lt;li&gt;使用するクーポンバンクのID。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                  |

### アクション - Post a Purchase

#### パラメータ

| **パラメータ**         | **説明**                                                                                                                                                                                                                                                                                                                                                                         |
|:----------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Order ID              | &lt;ul&gt;&lt;li&gt;購入のためのユニークな注文ID。&lt;/li&gt;&lt;li&gt;この注文IDが以前に使用されていた場合、リクエストは失敗し、新しい購入（および新しいコンバージョン）は作成されません。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、次を参照してください：[Friendbuyのドキュメンテーション](https://developers.friendbuy.com/#span-class-method-post-post-span-span-class-restofendpoint-purchases-span)。&lt;/li&gt;&lt;/ul&gt; |
| Referral Code         | &lt;ul&gt;&lt;li&gt;友人が購入するために紹介したRefcode。&lt;/li&gt;&lt;li&gt;Coupon Codeが存在しない場合は必須。&lt;/li&gt;&lt;li&gt;Referral CodeとCoupon Codeの両方が提供された場合、Referral Codeが優先されます。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                |
| Coupon Code           | &lt;ul&gt;&lt;li&gt;友人がマーチャントに購入するために持ってきたクーポンコード。Referral Codeが存在しない場合は必須。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                   |
| Order Amount          | &lt;ul&gt;&lt;li&gt;注文の金額。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                  |
| Order Email           | &lt;ul&gt;&lt;li&gt;注文に関連付けられたメールアドレス。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                              |
| New Customer          | &lt;ul&gt;&lt;li&gt;購入が新規（初回）の顧客によって行われたかどうか。&lt;/li&gt;&lt;li&gt;可能な値：`true`または`false`。&lt;/li&gt;&lt;li&gt;Friendbuyでは、報酬の基準の一つとして`新規顧客でなければならない`と指定できるため、報酬の適格性をチェックするために使用されます。&lt;/li&gt;&lt;/ul&gt;                                                                                                       |
| Customer ID           | &lt;ul&gt;&lt;li&gt;顧客に割り当てたID（Friendbuyが内部的に割り当てるIDとは異なります）。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                            |
| Customer First Name   |                                                                                                                                                                                                                                                                                                                                                                                         |
| Customer Last Name    |                                                                                                                                                                                                                                                                                                                                                                                         |
| Customer Email        | &lt;ul&gt;&lt;li&gt;顧客に関連付けられたメールアドレス。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                           |
| Stripe Customer ID    | &lt;ul&gt;&lt;li&gt;Stripeの顧客ID。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                         |
| Chargebee Customer ID | &lt;ul&gt;&lt;li&gt;Chargebeeの顧客ID&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                       |
