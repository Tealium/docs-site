---
title: Tealium + Digioh 統合ガイド
description: この記事では、Digiohがフォーム送信イベントをTealiumアカウントに送信するためのデータソースを作成する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-digioh-integration-guide/
---
## 前提条件

* [Digiohアカウント](https://digioh.com/login)
* Tealium EventStream API HubまたはTealium AudienceStream CDPアカウント

## 仕組み

Digiohは、Digiohのフォーム送信データをイベントとしてTealiumアカウントに送信する統合を提供します。統合は1つ以上のボックスに割り当てられ、追加のメタデータフィールドを送信することができます。Digiohでは、これらのイベントの名前（`tealium_event`として送信される）を構成し、Tealiumの属性名をDigiohのフォームフィールド名にマッピングします。

Tealiumでは、HTTP APIデータソースと予想されるイベントのイベント仕様を作成します。

## Tealiumの構成

Digiohからイベントを受信するためにアカウントを構成するには、データソースとイベント仕様の2つの部分があります。DigiohでTealium統合を追加する前に、TealiumでHTTP APIデータソースのインスタンスを作成します。これにより、Digiohの構成で使用するデータソースキーが生成されます。

### データソース

Digioh統合で使用するデータソースを追加するには、**HTTP API** データソースのインスタンスを追加します。完了したら、そのデータソースで生成されたデータソースキーをコピーして、Digiohの構成で静的フィールドマッピングに使用します。

詳細は[データソースへの接続について](https://docs.tealium.com/about-data-sources/)を参照してください。

### イベント仕様

Digiohイベント名とその必須およびオプションの属性を定義するイベント仕様を作成します。イベント仕様名をDigiohの構成で**イベント**パラメータに使用します。

詳細は[イベント仕様について](https://docs.tealium.com/about-event-specifications/)を参照してください。

## Digiohの構成

DigiohアカウントにTealium統合を追加するには、次の手順に従います：

1. Digiohにログインし、**統合**に移動して**新しい統合**をクリックします。
1. **統合**リストのCDPカテゴリーで**Tealium (Event)**を選択します。
1. 次のフィールドに値を入力します：
    * **アカウント** - あなたのTealiumアカウント名
    * **プロファイル** - あなたのTealiumプロファイル名
    * **イベント** - Tealiumで作成したイベント仕様の名前（`tealium_event`の値）

1. **統合を作成**をクリック

### フィールドマッピング

次に、イベントに送信するフィールドを選択するために**フィールドマッピング**を作成します。

データソースキーをフィールドとして追加するには：

1. **フィールド名**に`tealium_datasource`を入力します。
1. **フィールド値**で**静的**を選択し、Tealiumで作成したデータソースキーを入力します。
1. **フィールドマッピングを保存**をクリックします。

Digiohでは、イベントに含める追加のフォームフィールドが許可されています。**フィールドマッピング**構成を使用して、Digiohフィールドと一致するTealium属性名を選択します。たとえば、`[PHONE]`を`customer_phone`にマッピングすることができます。


<blockquote>
Digiohフィールド`[EMAIL]`は自動的にTealium属性`email`にマッピングされますが、このマッピングを編集することができます。
</blockquote>


標準フィールドのリストは次のとおりです：

* `[EMAIL]`
* `[NAME]`
* `[FIRST_NAME]`
* `[LAST_NAME]`
* `[FULL_NAME]`
* `[PHONE]`
* `[OPT_IN]`
* `[CUSTOM_1]`
* `[CUSTOM_2]`
* `[CUSTOM_3]`
* `[CUSTOM_4]`
* `[CUSTOM_5]...[CUSTOM_50]`

マッピング可能なDigiohフィールドの完全なリストについては、[Digiohが統合を通じてプッシュできるすべてのデータと分析フィールドは何ですか？](https://help.digioh.com/knowledgebase/what-are-all-the-fields-digioh-can-push/)を参照してください。

## ベンダー文書

* [Digioh: Tealiumとの統合方法](https://help.digioh.com/knowledgebase/how-to-integrate-with-tealium/)
* [Digioh統合の基本](https://help.digioh.com/knowledgebase/digioh-integration-basics/)
* [Digioh: データフィールドのマッピング](https://help.digioh.com/knowledgebase/what-are-all-the-fields-digioh-can-push/)