---
title: Veritonicコネクタ構成ガイド
description: この記事では、Veritonicコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/veritonic-connector/
---

## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Veritonic
* APIバージョン：v1
* APIエンドポイント：`https://atr.veritonicmetrics.com`

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を行います：
* **クライアントID**  
Veritonicダッシュボードからの一意の識別子。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| イベントを送信 | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベントを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| イベントタイプ | ユーザーが実行したアクションのタイプを示す文字列。 |

### イベント属性

| **パラメータ** | **説明** |
| --- | --- |
| ユーザーのIPアドレス | ユーザーのデバイスのネットワークアドレス。 |
| タイムスタンプ | アクションの日時を表す数値。 |
| ユーザーエージェント | ユーザーのブラウザとオペレーティングシステムを識別する文字列。 |
| ページURL | アクションが行われたページのURL。 |
| GDPR同意 | データ処理に対するユーザーの同意を示す文字列。 |
| イベントタイプ属性 | オプションのイベントタイプ属性。 |

### イベントタイプ属性

| **イベントタイプ** | **追加パラメータ（オプション）** |
| --- | --- |
| `view` | &lt;ul&gt;&lt;li&gt;なし&lt;/li&gt;&lt;/ul&gt; |
| `addtocart` | &lt;ul&gt;&lt;li&gt;`value`, `currency`, `quantity`, `product_id`, `product_name`, `product_type`, `product_vendor`, `variant_id`, `variant_name`&lt;/li&gt;&lt;/ul&gt; |
| `checkout` | &lt;ul&gt;&lt;li&gt;`value`, `currency`, `discount_code`, `quantity`, `line_items`&lt;/li&gt;&lt;li&gt;`line_items`は以下のオプション属性を持つオブジェクトの配列です：`value`, `quantity`, `product_id`, `product_name`, `product_type`, `product_vendor`, `variant_id`, `variant_name`&lt;/li&gt;&lt;li&gt;ユーザーは次の各パラメータに数値の配列または文字列の配列をマッピングできる必要があります：&lt;ul&gt;&lt;li&gt;`line_items.value`&lt;/li&gt;&lt;li&gt;`line_items.quantity`&lt;/li&gt;&lt;li&gt;`line_items.product_id`&lt;/li&gt;&lt;li&gt;`line_items.product_name`&lt;/li&gt;&lt;li&gt;`line_items.product_type`&lt;/li&gt;&lt;li&gt;`line_items.product_vendor`&lt;/li&gt;&lt;li&gt;`line_items.variant_id`&lt;/li&gt;&lt;li&gt;`line_items.variant_name`&lt;/li&gt;&lt;/ul&gt;&lt;/li&gt;&lt;li&gt;最終的なオブジェクトの配列はバックエンドで構築する必要があります。たとえば、以下のような場合：&lt;ul&gt;&lt;li&gt;`line_items.quantity` = [1,2]&lt;/li&gt;&lt;li&gt;`line_items.product_id` = [a,b]&lt;/li&gt;&lt;li&gt;line_items配列は次のようになります：`[{product_id:a,quantity:1},{product_id:b,quantity:2}]`&lt;/ul&gt;&lt;/li&gt;&lt;/li&gt;&lt;/ul&gt; |
| `lead` | &lt;ul&gt;&lt;li&gt;`value`, `currency`, `type`,`category`&lt;/li&gt;&lt;/ul&gt;  |
| `product` | &lt;ul&gt;&lt;li&gt;`value`, `currency`, `product_id`, `product_name`, `product_type`, `product_vendor`&lt;/li&gt;&lt;/ul&gt; |
| `purchase` | &lt;ul&gt;&lt;li&gt;`value`, `currency`, `discount_code`, `quantity`, `line_items`&lt;/li&gt;&lt;li&gt;`line_items`: チェックアウトイベントと同じ&lt;/li&gt;&lt;/ul&gt; |
| `app_install` | &lt;ul&gt;&lt;li&gt;`app_name`, `app_id`, `integration`&lt;/li&gt;&lt;/ul&gt; |
