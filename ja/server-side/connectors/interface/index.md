---
title: コネクタインターフェース
description: コネクタインターフェースでは、Customer Data Platform（CDP）Customer Data Platform（CDP）および Event Streaming API Hub 向けのサーバーサイドコネクタとアクションを追加、編集、削除するための直感的なワークフローを利用できます。
url: https://docs.tealium.com/ja/server-side/connectors/interface/
---
**コネクタの概要**画面では、新しいコネクタの追加と構成、既存のコネクタに対するアクションの表示と編集、成功数およびエラー数に関するコネクタメトリクスのエクスポートを行えます。

次の一覧では、コネクタインターフェースから利用できる機能の概要を説明します。

## コネクタの概要

コネクタにアクセスすると、**コネクタの概要**画面に現在のサーバーサイドコネクタの一覧が表示されます。

![](https://docs.tealium.com/images/server-side/connectors/overview-screen.png)

## コネクタを検索する

検索を使用すると、ベンダー名またはコネクタ名に含まれる単語を入力して、コネクタをすばやく見つけることができます。入力に応じて検索語に一致するコネクタが表示されるため、必要なコネクタを簡単に見つけて選択できます。

![](https://docs.tealium.com/images/server-side/connectors/spotlight-search.png)

## お気に入り

コネクタをお気に入りに登録すると、フィルターメニューからすばやくアクセスできます。頻繁に使用するコネクタや重要なコネクタに対して、この機能を使用してください。

![](https://docs.tealium.com/images/server-side/connectors/connectors-favorite-filter-view.png)

## コネクタの概要情報

マーケットプレイスでコネクタを選択すると、**コネクタの概要情報**に、サポートされているデータ型（イベントデータまたは訪問データ）、要件、サポートされているアクション、コネクタに関連する内部および外部リソースなどの情報が表示されます。

![](https://docs.tealium.com/images/server-side/connectors/connector-summary.png)

## アクションを有効化または無効化する

![](https://docs.tealium.com/images/server-side/connectors/connectors-active-label.png)
![](https://docs.tealium.com/images/server-side/connectors/connectors-inactive-label.png)

コネクタまたはその個々のアクションを有効化または無効化できます。アクションを有効化する前に、コネクタを有効化する必要があります。

詳細については、を参照してください。

## アクションタイプを変更する

コネクタのアクションを構成した後で、そのコネクタがサポートする別のアクションの方が適していることに気付く場合があります。別のアクションを一から構成し直す代わりに、既存のアクションを再利用して、そのアクションタイプを変更できます。

詳細については、を参照してください。

## テンプレートを編集する

拡張エディターを使用して、コネクタテンプレートを作成および編集できます。構文の強調表示や自動補完などを活用して、カスタムインテグレーションをすばやく作成できます。

![](https://docs.tealium.com/images/server-side/connectors/connector-templates-custom-json.png)

詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。

## レポート

コネクタレポートには、成功とエラーの合計件数がリアルタイムで表示されます。また、エラー情報をCSVファイルとしてダウンロードできます。

## 以前のバージョンに戻す

**バージョン履歴**を使用して、コネクタを以前に公開された任意のバージョンに戻すことができます。詳細については、[サーバーサイドのバージョン履歴]()を参照してください。