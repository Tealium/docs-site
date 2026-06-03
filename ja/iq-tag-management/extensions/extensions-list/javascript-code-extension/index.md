---
title: JavaScriptコード（基本）拡張
description: JavaScriptコード拡張は、Tealium iQタグ管理を通じてカスタムJavaScript ES5コードを実装するために設計されています。組み込みのコードエディタとコードを実行するタイミングと場所の構成オプションが付属しています。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/javascript-code-extension/
---
これはJavaScriptコード拡張の基本バージョンです。高度なニーズについては、[Advanced JavaScript Code Extension]()を参照してください。

## 前提条件

* [JSコード拡張の管理権限]()
  * この権限は、アカウントにJavaScriptコード拡張を追加または編集するために必要です。
* utagバージョン4.38以降。`utag.js`テンプレートの更新についての詳細は、当社のナレッジベース記事[Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)を参照してください。
  * このバージョンは、All Tagsスコープの下の実行オプションのサポートを提供します
  * まだ行っていない場合は、このバージョンにアップグレードしてください。

## 仕組み

JavaScriptコード拡張は、サイトで読み込むファイルに含めるカスタムコードを作成する力を与えます。拡張のスコープにより、コードはutag.jsまたはベンダーのutag.#.jsファイルのいずれかで読み込まれます。拡張のテキストボックスに入力されたコードは、そのままの形でutagファイルに含まれますが、コードは次の例に示すように、匿名関数ラッパーから実行されることに注意が必要です：

```js
function(a, b) {
    // JavaScriptコード拡張の内容はここで実行されます
}
```

パラメータは次のように表されます：

* `a`：行われたトラッキングコールを示します。`utag.view()`の場合は&#34;view&#34;、`utag.link()`の場合は&#34;link&#34;。
* `b`：トラッキングコールに渡されたデータオブジェクトへの参照。

JavaScriptコード拡張は柔軟で、タグ管理ソリューション内で達成したいほとんどのことに使用できますが、それがアカウントに与える影響を理解することが重要です。他の組み込み拡張を使用してタスクを達成しようと試みることをお勧めします。

JavaScriptコード拡張の使用に関する以下の利点と欠点を考慮してください：

**利点**

* 完全にカスタマイズ可能なコードは、JavaScriptを使用して達成できるほとんどすべてのことを達成できます。
* フロントエンドのJavaScriptを書くのに慣れている開発者にとっては、より速く、より馴染み深い。

**欠点**

* 非開発者にとって理解し、編集するのが難しい。
* 時間の経過とともに維持するのが難しくなる。
* タイプミスや論理エラーが発生しやすい。
* 変数名がハードコーディングされているため、Data Layerタブで変数の名前を変更しても更新されません。
* 変更された変数名はJavaScriptコード拡張に伝播されません。例えば、変数の名前を変更する場合、JavaScriptコード拡張内のその変数のすべての出現を変更する必要があります。

### 条件

条件は、スコープの上にさらなる制御層を追加します。[Set Data Values]()と[Join Data Values]()拡張に任意の数の条件文を適用できます。これらの条件は、JavaScriptコード拡張が実行されるタイミングを制御します。

### 実行順序と一度だけ実行

JavaScriptコード拡張は、コードが実行されるタイミングを決定するための以下のオプションを提供します。
`utag.js`の操作順序については、[Order of Operations]()を参照してください。

* utag Sync
* Load Rules前
* Load Rules後（デフォルト）
* Tags後
* Load Rules後に一度だけ実行
* Load Rules前に一度だけ実行
* Tags後に一度だけ実行

デフォルトでは、JavaScriptコード拡張はすべての[tracking call](/ja/platforms/javascript/track/)で実行され、ページ内イベントトラッキングを含むため、ページの読み込みごとに複数回実行される可能性があります。コードの複数回の実行を防ぎたい場合は、実行ドロップダウンリストのRun Onceオプションのいずれかを選択します。これらのオプションは、All Tagsスコープでのみ利用可能で、utag v4.38以降が必要です。

## 開始する前に

開始する前に以下を考慮してください：

* テキストボックスの内容は、入力した通りにJavaScriptファイルに含まれるため、コードを`&lt;script&gt;`タグで囲まないでください。
* `utag_data`オブジェクトから変数を参照している場合、例えば`page_name`や`language`など、`b[&#39;VARIABLE&#39;]`を使用します。  
[b object]()について詳しく学びましょう。
* スコープされたタグのタグテンプレートで定義された変数を参照している場合、例えば`account_id`や`base_url`など、`u[&#39;VARIABLE&#39;]`を使用します。

## 構成手順

JavaScriptコード拡張を構成するための以下の手順を使用します：

1. **Extensions Marketplace**に移動し、[AdvancedタブからJavaScriptコード拡張を追加]()します。
1. **Title**：この拡張の名前を入力します。
1. **Scope**：以下のオプションから選択します：  
    * Preloader（Conditionsをサポートしていません）
    * DOM Ready
    * All Tags
    * Vendor Tag(s)
1. **Execution**：このドロップダウンリストは**All Tags**スコープにのみ利用可能です。以下のオプションから一つを選択します：
    * Before Load Rules
    * After Load Rules (default)
    * After Tags
    * Run Once after Load Rules
    * Run Once before Load Rules
    * Run Once after Tags
1. エディタにJavaScriptコードを入力します。エディタはエラーや警告を表示します。
1. **Condition**（オプション）
    * **Add Condition**をクリックし、条件文を作成します。
    * 最初のドロップダウンリストは変数で、2つ目のドロップダウンリストは[評価演算子]()のリストを提供します。
    * 条件ロジックを値に対して実行している場合は、テキストフィールドにそれを入力します。
    * 複数の条件を適用する場合は、**AND**と**OR**のロジックの間で選択します。
1. 変更を保存し、公開します。

## FAQ

#### 新しいJavaScriptコード拡張を追加または編集できないのはなぜですか？

あなたのTealium iQアカウントに[JSコード拡張の管理権限]()がありません。権限を取得するためにTealiumアカウント管理者に連絡してください。

#### なぜPreloaderとConditionsを選択できないのですか？

Preloader状態では、Data Layerはまだ満たされておらず、条件ロジックを評価するためのutagデータがありません。このため、Preloaderが選択されているときには、Conditionsのドロップダウン選択肢はグレーアウトされます。

#### PreloaderとLoad Rules前のRun Onceの違いは何ですか？

どちらもData Layerが満たされる前に一度拡張を実行しますが、Preloaderは条件をサポートしていません。この制約を考慮に入れてスコープを構成してください。

