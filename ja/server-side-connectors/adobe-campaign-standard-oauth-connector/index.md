---
title: Adobe Campaign Standard (OAuth) コネクタ構成ガイド
description: この記事では、Adobe Campaign Standard (OAuth) コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-standard-oauth-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Adobe Campaign Standard (OAuth)
* APIバージョン：v1.0
* APIエンドポイント：`https://mc.adobe.io/`

## 構成

コネクタマーケットプレイスにアクセスして新しいコネクタを追加します。コネクタの追加方法については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：
* **テナントID**  
    * テナントIDは、Adobe Marketing CloudのURLで見つけることができます。
    * 例：`https://_yourtenantid_.experiencecloud.adobe.com/campaign.html`。
* **APIキー**  
    * APIキー（クライアントID）は、[Adobe I/Oコンソール](https://console.adobe.io/)で見つけることができます。
* **シークレットキー**  
    * クライアントシークレットは、[Adobe I/Oコンソール](https://console.adobe.io/)で見つけることができます。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| プロファイルの作成または更新 | ✓ | ✗ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### プロファイルの作成または更新

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 更新戦略 | <ul><li>必須。適用可能な更新戦略を選択します。</li><li>**新規作成のみ**：既存のプロファイルを検索し、見つからない場合は新しいプロファイルを作成します。</li><li>**更新のみ**：既存のプロファイルを検索して更新します。</li><li>**新規作成または更新**：既存のプロファイルを検索し、見つかった場合は更新し、そうでない場合は新しいプロファイルを作成します。</li></ul> |
| プロファイルデータ | <ul><li>プロファイルフィールド名と対応する値。</li></ul> |
| フィルター | <ul><li>**更新戦略**が`Create Or Update`または`Update Only`の場合は必須です。</li><li>一意の結果を返すフィルターを選択することをお勧めします。</li><li>詳細については、[Campaign: Calling a resource using a composite identification key](https://experienceleague.adobe.com/docs/campaign-standard/using/developing/adding-or-extending-a-resource/uc-calling-resource-id-key.html?lang=en)を参照してください。</li><li>検索結果が複数のプロファイルを返した場合、最初のプロファイルのみが更新されます。</li></ul> |
| カスタムフィルター | <ul><li>選択したフィルターがカスタムの場合、このオプションを選択します。</li><li>詳細については、[Campaign: Custom filters](https://experienceleague.adobe.com/docs/campaign-standard/using/working-with-apis/global-concepts/additional-operations/filtering.html?lang=en#custom-filters)を参照してください。</li></ul> |
| フィルターパラメータ | <ul><li>検索に使用されるフィルターパラメータ。</li></ul> |
| テンプレート変数 | <ul><li>データ入力としてテンプレート変数を提供します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`。</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
| テンプレート | <ul><li>本文データで参照されるテンプレートを提供します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>テンプレートは、サポートされるフィールドに名前で二重中括弧を使用して注入されます。例：`{{SomeTemplateName}}`。</li></ul> |
