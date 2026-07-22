---
title: Adobe Target コンテンツ変更拡張
description: Adobe Target コンテンツ変更拡張を Adobe Target タグまたは Adobe Experience Platform Web SDK タグと一緒に使用して、HTML要素のコンテンツを変更します。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/adobe-target-content-modification-extension/
---
## 前提条件

* utag v4.38 またはそれ以降。`utag.js` テンプレートの更新についての詳細は、ナレッジベースの記事 [utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470) を参照してください。
* [utag.sync.js でのグローバル Mbox の使用](https://docs.tealium.com/adobe-target-using-global-mbox-with-utagsyncjs/)

## 仕組み

Adobe Target コンテンツ変更拡張は、Adobe Target タグまたは Adobe Experience Platform Web SDK タグと一緒に使用して、HTML要素のコンテンツを変更します。これは、条件に基づいてA/Bコンテンツを表示するために使用されます。この拡張機能を動作させるためには、[Adobe Target タグ](https://docs.tealium.com/adobe-test-target-tag/)または [Adobe Experience Platform Web SDK タグ](https://docs.tealium.com/adobe-experience-platform-web-sdk-tag/)にスコープを構成する必要があります。

この拡張機能は初期化コードを必要とします。これは、`utag.sync.js` スニペットをページの `<head>` セクションに配置することで行われます。[utag.sync.jsの使用]()について詳しく学びましょう。

### 拡張機能の使用

始める前に、[拡張機能の仕組み]()について理解しておいてください。

この拡張機能のスコープは、Adobe Target タグまたは Adobe Experience Platform Web SDK タグに構成する必要があります。

拡張機能が追加されたら、グローバル mbox 以外に追加の mbox が必要な場合は、**mbox を追加** ボタンをクリックして拡張機能を構成します。以下の構成オプションが利用可能です：

* **要素タイプ**：要素を識別するためには、ページのコンテンツが大幅に変更されると XPath 識別子が変更されるため、DOM ID の使用を推奨します。
    * **DOM ID** または **XPath** を選択します。

* **DOM ID**：要素の DOM ID または XPath 識別子の値を入力します。
* **Mod Position**：新しいコンテンツを配置する場所を、識別した要素に対して指定します：
    * **Before Node**：識別した要素の前にコンテンツを配置します。
    * **After Node**：識別した要素の後にコンテンツを配置します。
    * **Beginning of Node**：識別した要素の始まりにコンテンツを配置します。
    * **End of Node**：識別した要素の終わりにコンテンツを配置します。
    * **Replace Node Content**：要素のコンテンツを置き換えます。
    * **Replace Node**：要素全体を置き換えます。
    * **Replace Node Content (leave default)**：要素のコンテンツを置き換えますが、Adobeの Target サービスが一時的に利用できない場合は、テストコンテンツの代わりにデフォルトのコンテンツが表示されます。フリッカーフリー機能を使用する場合は、**この Mod Position** を選択する必要があります。

* **mBox Div ID**：（Adobe から提供）テストの mBox ID を入力します。
* **Static Params**（オプション）このフィールドにクエリ文字列形式で静的パラメータを追加します。これはアンパサンド (`&`) 文字で区切ります。
* **Timeout**：Adobeからの応答を待つ時間（ミリ秒）。この機能は、通信問題や同意構成のために Adobe Target タグまたは Adobe Experience Platform Web SDK タグのパーソナライゼーションデータが利用できない場合に、ページのレンダリングを完了させることができます。

**条件を追加**をクリックして、拡張機能がコンテンツを変更するタイミングと場所を決定するロジックステートメントを作成します。さらにコンテンツ変更エントリを追加するには、拡張機能構成の右上隅にある **+** ボタンをクリックします。別のオプションとして、各エントリごとに拡張機能を複製することも可能ですが、一つの拡張機能に複数のエントリを保持する方が、この拡張機能内のすべてのエントリが拡張機能のロード条件を共有するため、実装がすっきりします。
