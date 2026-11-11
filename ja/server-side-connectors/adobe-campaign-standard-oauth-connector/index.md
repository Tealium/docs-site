---
title: Adobe Campaign Standard（OAuth）コネクタ構成ガイド
description: この記事では、Adobe Campaign Standard（OAuth）コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-standard-oauth-connector/
---
## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：Adobe Campaign Standard（OAuth）
* APIバージョン：v1.0
* APIエンドポイント：`https://mc.adobe.io/`

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を行います。
* **テナントID**  
    * テナントIDは、Adobe Marketing CloudのURLで確認できます。
    * 例：`https://_yourtenantid_.experiencecloud.adobe.com/campaign.html`
* **APIキー**  
    * APIキー（クライアントID）は、[Adobe I/O Console](https://console.adobe.io/)で確認できます。
* **秘密鍵**  
    * クライアントシークレットは、[Adobe I/O Console](https://console.adobe.io/)で確認できます。

コネクタを構成したら、**完了**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| プロファイルの作成または更新 | ✓ | ✗ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメーターとオプションを構成する方法について説明します。

### プロファイルの作成または更新

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| 更新戦略 | <ul><li>（必須）適用する更新戦略を選択します。</li><li>**作成のみ**：既存のプロファイルを検索し、見つからない場合は新しいプロファイルを作成します。</li><li>**更新のみ**：既存のプロファイルを検索して更新します。</li><li>**作成または更新**：既存のプロファイルを検索し、見つかった場合は更新します。それ以外の場合は、新しいプロファイルを作成します。</li></ul> |
| プロファイルデータ | <ul><li>プロファイルフィールド名とそれに対応する値。 </li></ul> |
| フィルター | <ul><li>**更新戦略**が`Create Or Update`または`Update Only`の場合は必須です。</lil><li>一意の結果を返すフィルターを選択することをお勧めします。</li><li>詳細については、[Campaign：複合識別キーを使用したリソースの呼び出し](https://experienceleague.adobe.com/docs/campaign-standard/using/developing/adding-or-extending-a-resource/uc-calling-resource-id-key.html?lang=en)を参照してください。</li><li>検索結果で複数のプロファイルが返された場合は、最初のプロファイルのみが更新されます。</li></ul>  |
| カスタムフィルター | <ul><li>選択したフィルターがカスタムフィルターの場合は、このオプションを選択します。</li><li>詳細については、[Campaign：カスタムフィルター](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/global-concepts/additional-operations/filtering.html?lang=en#custom-filters)を参照してください。</li></ul> |
| フィルターパラメーター | <ul><li>検索で使用するフィルターパラメーター。</li></ul> |
| テンプレート変数 | <ul><li>テンプレート変数をデータ入力として指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から構築されます。</li></ul> |
| テンプレート | <ul><li>本文データで参照するテンプレートを指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。例：`{{SomeTemplateName}}`</li></ul> |