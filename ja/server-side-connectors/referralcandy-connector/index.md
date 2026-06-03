---
title: ReferralCandyコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでReferralCandyコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/referralcandy-connector/
---## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|Signup Advocate| ✓| ✓|
|Invite Advocate| ✓| ✓|
|Register a Purchase| ✗| ✓|
|Update Status of Referred Purchase| ✗| ✓|
|Unsubscribe an Advocate| ✓| ✓|
|Resubscribe an Advocate| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **API Access ID**  
APIアクセスIDは、プロフィールページの&#34;API Tokens&#34;セクションで見つけることができます。&lt;https://my.referralcandy.com/settings&gt;。
* **API Secret Key**  
APIシークレットキーは、プロフィールページの&#34;API Tokens&#34;セクションで見つけることができます。&lt;https://my.referralcandy.com/settings&gt;。

## アクション構成 - パラメータとオプション

**Next**をクリックするか、**Actions**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - Signup Advocate

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  &lt;ul&gt;&lt;li&gt;アドボケイトのメールアドレス。&lt;/li&gt;&lt;li&gt;このエンドポイントについての情報は、次を参照してください：&lt;https://www.referralcandy.com/api#signup&gt;.&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;アドボケイトの名前。&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;アドボケイトの姓。&lt;/li&gt;&lt;/ul&gt; |

### アクション - Invite Advocate

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  &lt;ul&gt;&lt;li&gt;招待状を送るメールアドレス。&lt;/li&gt;&lt;li&gt;このエンドポイントについての情報は、次を参照してください：&lt;https://www.referralcandy.com/api#invite&gt;.&lt;/li&gt;&lt;/ul&gt; |

### アクション - Register a Purchase

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  &lt;ul&gt;&lt;li&gt;顧客のメールアドレス。&lt;/li&gt;&lt;li&gt;このエンドポイントについての情報は、次を参照してください：&lt;https://www.referralcandy.com/api#purchase&gt;.&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;顧客の名前。&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;顧客の姓。&lt;/li&gt;&lt;/ul&gt; |
|Customer&#39;s Language|  &lt;ul&gt;&lt;li&gt;顧客の優先言語。&lt;/li&gt;&lt;li&gt;構成されていない場合やキャンペーンで利用できない場合は、キャンペーンのデフォルト言語になります。&lt;/li&gt;&lt;li&gt;可能な値：en, fr, de, es, it, ja, nl, ru, zh-CN, zh-HK, zh-TW, da, no, sv, pt-BR。&lt;/li&gt;&lt;/ul&gt; |
|Discount Code|  &lt;ul&gt;&lt;li&gt;注文で使用された割引コード。&lt;/li&gt;&lt;/ul&gt; |
|Accepts Marketing|  &lt;ul&gt;&lt;li&gt;顧客がマーケティングに同意したかどうか。&lt;/li&gt;&lt;li&gt;可能な値：trueまたはfalse。&lt;/li&gt;&lt;li&gt;デフォルトはtrue。&lt;/li&gt;&lt;/ul&gt; |
|Order Timestamp|  &lt;ul&gt;&lt;li&gt;注文のUnixタイムスタンプ。&lt;/li&gt;&lt;li&gt;提供されていない場合、現在のUnixタイムスタンプが使用されます。&lt;/li&gt;&lt;/ul&gt; |
|Browser IP|  &lt;ul&gt;&lt;li&gt;購入時の顧客のIPアドレス。&lt;/li&gt;&lt;/ul&gt; |
|User Agent|  &lt;ul&gt;&lt;li&gt;顧客のウェブブラウザのユーザーエージェント文字列。&lt;/li&gt;&lt;/ul&gt; |
|Invoice Amount|  &lt;ul&gt;&lt;li&gt;この購入のための総請求額。&lt;/li&gt;&lt;/ul&gt; |
|Currency Code|  &lt;ul&gt;&lt;li&gt;注文請求書で使用されるISO 4217通貨コード（例：USD, GBP, INR）。&lt;/li&gt;&lt;/ul&gt; |
|External Reference ID|  &lt;ul&gt;&lt;li&gt;この購入を外部で追跡するために使用できるID。&lt;/li&gt;&lt;/ul&gt; |

### アクション - Update Status of Referred Purchase

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Customer Email|  &lt;ul&gt;&lt;li&gt;紹介された購入を行った顧客のメールアドレス。&lt;/li&gt;&lt;li&gt;このエンドポイントについての情報は、次を参照してください：&lt;https://www.referralcandy.com/api#referral&gt;.&lt;/li&gt;&lt;/ul&gt; |
|Notify Referring Customer|  &lt;ul&gt;&lt;li&gt;上記の顧客を紹介した顧客に、紹介が無視されたことを通知するかどうか。&lt;/li&gt;&lt;li&gt;可能な値：trueまたはfalse。デフォルトはtrue。&lt;/li&gt;&lt;/ul&gt; |
|Returned Purchase|  &lt;ul&gt;&lt;li&gt;顧客が購入品を返品したかどうか。&lt;/li&gt;&lt;li&gt;可能な値：trueまたはfalse。trueに構成すると、紹介は無視され、報酬は支払われません。&lt;/li&gt;&lt;/ul&gt; |

### アクション - Unsubscribe an Advocate

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  &lt;ul&gt;&lt;li&gt;連絡先のメールアドレス。&lt;/li&gt;&lt;li&gt;このエンドポイントについての詳細は、次を参照してください：&lt;https://www.referralcandy.com/api#unsubscribed&gt;.&lt;/li&gt;&lt;/ul&gt; |

### アクション - Resubscribe an Advocate

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  &lt;ul&gt;&lt;li&gt;連絡先のメールアドレス。&lt;/li&gt;&lt;li&gt;このエンドポイントについての詳細は、次を参照してください：&lt;https://www.referralcandy.com/api#unsubscribed&gt;.&lt;/li&gt;&lt;/ul&gt; |
