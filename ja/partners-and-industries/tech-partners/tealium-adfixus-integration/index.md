---
title: Tealium + AdFixus 統合ガイド
description: この記事では、iQタグ管理アカウントでAdFixus統合タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-adfixus-integration/
---
AdFixusを使用すると、企業は自社のデータを所有し、個人はプライバシーに焦点を当てたソリューションで同意を管理できます。AdFixusが特許を持つファーストパーティクッキープラットフォームは、企業が顧客の全体像を取り戻し、既存のシステムでそのデータを使用してパーソナライゼーション、分析、メディアの最適化を改善することを可能にします。TealiumにAdFixus IDを取り込むことで、組織はTealiumデータとともにAdFixusの特許を持つアイデンティティプラットフォームを活用し、顧客にシームレスなエンドツーエンドの統一体験を提供するために、オーディエンスの完全なビュー（クロスドメインおよびマルチドメイン）を統合できます。

## 前提条件

* **Tealium**
    * 以下のうち少なくとも1つ:
        * iQタグ管理
        * AudienceStream
        * EventStream（オプション）
* **AdFixus**
    * 組織のウェブプロパティ/ドメインに実装されたAdFixusプラットフォーム。
    * アクティブなAdFixus組織ライセンスキー。

## 動作原理

iQタグ管理プラットフォームを通じてではなく、所有するデジタルプロパティを通じてAdFixus IDを実装します。このインストール方法は、完全なブラウザカバレッジを保証します。

組織のiQタグ管理データレイヤーにAdFixus IDを追加し、関連するタグにマッピングするか、Tealiumのサーバーサイドプラットフォームに送信してプロファイルをエンリッチすることができます。組織がiQタグ管理を使用せずにAudienceStreamのみを使用する場合は、TealiumにAdFixus IDを渡し、適切な属性に割り当てます。

## iQタグ管理の構成

iQタグ管理にAdFixus IDを統合するには：

1. iQタグ管理インスタンスでAdFixus [データレイヤー変数]()を作成します。
    * AdFixus IDを使用するすべてのTealiumアカウントプロファイルでこの変数を作成します。
    * お使いのウェブサイトのクッキーにAdFixus IDが保存される可能性があります。詳細については、[AdFixus実装チーム](https://www.adfixus.com/contact)にお問い合わせください。![](/images/tech-partners/adfixus-add-variable.png)
1. AdFixus ID変数を送信する必要がある関連タグを特定し、[データポイントをマッピング]()します。
    1. **変数**ドロップダウンリストからデータ変数を選択し、**選択先を選択**をクリックします。![](/images/tech-partners/adfixus-select-destination.png)
    1. **カスタム選択先を追加**をクリックし、**カスタム選択先**フィールドにAdFixus IDの予想される名前を入力し、**&#43;追加**をクリックします。![](/images/tech-partners/adfixus-custom-destination.png)
        * 新規または既存のタグがAdFixus IDを使用するたびにこのプロセスを繰り返します。
1. 保存して公開します。

## サーバーサイドの構成

AudienceStreamおよびEventStreamにAdFixus IDを統合するには：

1. iQタグ管理も使用している場合は、[Tealium Collectタグ]()を構成します。
  * AdFixus IDは、[イベント属性]()の下でユニバーサル変数として表示されます。
1. iQタグ管理を使用していない場合は、AdFixus IDの[イベント属性を作成]()します。
    1. **イベント属性**に移動し、**&#43; 属性を追加**をクリックします。
    1. **ユニバーサル変数**を選択し、**続行**をクリックします。
    1. **文字列**を選択し、**続行**をクリックします。
    1. 属性名とその他の関連情報を入力します。![](/images/tech-partners/adfixus-add-attribute.png)
    1. **完了**をクリックします。
        * AdFixusからTealiumにさらにデータを送信する予定がある場合は、そのデータの属性も作成します。
        * データセットのすべての属性に対して[イベント仕様]()を作成することをお勧めします。
1. AdFixus IDの[訪問属性を作成]()します。
    1. **訪問/訪問属性**に移動し、**&#43; 属性を追加**をクリックします。
    1. **訪問**を選択し、**続行**をクリックします。
    1. **文字列**または**訪問ID**を選択し、**続行**をクリックします。
        * **訪問ID**を選択すると、後でデータタイプを変更することはできません。
    1. 属性名とその他の関連情報を入力します。
    1. **エンリッチメントを追加**をクリックします。
    1. ステップ1または2で作成したAdFixus IDイベント属性を選択し、**ルールを作成**をクリックします。
    1. 属性が`割り当てられている`かつ`none（大文字小文字を区別しない）と等しくない`場合のルールを作成します。![](/images/tech-partners/adfixus-attribute-ready.png)
1. 保存して公開します。

AdFixus IDは、AudienceStreamコネクタのマッピング可能な属性として利用可能になり、関連する統合でマッピングできます。

## ベンダー文書

* [統合: Tealium AudienceStream CDPとAdFixus](https://www.adfixus.com/integrations/integration-tealium-audience-stream-cdp-and-adfixus).
