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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **API Access ID**  
APIアクセスIDは、プロフィールページの"API Tokens"セクションで見つけることができます。<https://my.referralcandy.com/settings>。
* **API Secret Key**  
APIシークレットキーは、プロフィールページの"API Tokens"セクションで見つけることができます。<https://my.referralcandy.com/settings>。

## アクション構成 - パラメータとオプション

**Next**をクリックするか、**Actions**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - Signup Advocate

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  <ul><li>アドボケイトのメールアドレス。</li><li>このエンドポイントについての情報は、次を参照してください：<https://www.referralcandy.com/api#signup>.</li></ul> |
|First Name|  <ul><li>アドボケイトの名前。</li></ul> |
|Last Name|  <ul><li>アドボケイトの姓。</li></ul> |

### アクション - Invite Advocate

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  <ul><li>招待状を送るメールアドレス。</li><li>このエンドポイントについての情報は、次を参照してください：<https://www.referralcandy.com/api#invite>.</li></ul> |

### アクション - Register a Purchase

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  <ul><li>顧客のメールアドレス。</li><li>このエンドポイントについての情報は、次を参照してください：<https://www.referralcandy.com/api#purchase>.</li></ul> |
|First Name|  <ul><li>顧客の名前。</li></ul> |
|Last Name|  <ul><li>顧客の姓。</li></ul> |
|Customer's Language|  <ul><li>顧客の優先言語。</li><li>構成されていない場合やキャンペーンで利用できない場合は、キャンペーンのデフォルト言語になります。</li><li>可能な値：en, fr, de, es, it, ja, nl, ru, zh-CN, zh-HK, zh-TW, da, no, sv, pt-BR。</li></ul> |
|Discount Code|  <ul><li>注文で使用された割引コード。</li></ul> |
|Accepts Marketing|  <ul><li>顧客がマーケティングに同意したかどうか。</li><li>可能な値：trueまたはfalse。</li><li>デフォルトはtrue。</li></ul> |
|Order Timestamp|  <ul><li>注文のUnixタイムスタンプ。</li><li>提供されていない場合、現在のUnixタイムスタンプが使用されます。</li></ul> |
|Browser IP|  <ul><li>購入時の顧客のIPアドレス。</li></ul> |
|User Agent|  <ul><li>顧客のウェブブラウザのユーザーエージェント文字列。</li></ul> |
|Invoice Amount|  <ul><li>この購入のための総請求額。</li></ul> |
|Currency Code|  <ul><li>注文請求書で使用されるISO 4217通貨コード（例：USD, GBP, INR）。</li></ul> |
|External Reference ID|  <ul><li>この購入を外部で追跡するために使用できるID。</li></ul> |

### アクション - Update Status of Referred Purchase

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Customer Email|  <ul><li>紹介された購入を行った顧客のメールアドレス。</li><li>このエンドポイントについての情報は、次を参照してください：<https://www.referralcandy.com/api#referral>.</li></ul> |
|Notify Referring Customer|  <ul><li>上記の顧客を紹介した顧客に、紹介が無視されたことを通知するかどうか。</li><li>可能な値：trueまたはfalse。デフォルトはtrue。</li></ul> |
|Returned Purchase|  <ul><li>顧客が購入品を返品したかどうか。</li><li>可能な値：trueまたはfalse。trueに構成すると、紹介は無視され、報酬は支払われません。</li></ul> |

### アクション - Unsubscribe an Advocate

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  <ul><li>連絡先のメールアドレス。</li><li>このエンドポイントについての詳細は、次を参照してください：<https://www.referralcandy.com/api#unsubscribed>.</li></ul> |

### アクション - Resubscribe an Advocate

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Email Address|  <ul><li>連絡先のメールアドレス。</li><li>このエンドポイントについての詳細は、次を参照してください：<https://www.referralcandy.com/api#unsubscribed>.</li></ul> |
