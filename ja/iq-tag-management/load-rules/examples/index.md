---
title: ロードルールの例
url: https://docs.tealium.com/ja/iq-tag-management/load-rules/examples/
---以下は、一般的なロードルールの例です。

## ANDロジック

以下の例は、靴を購入している顧客のサイトのチェックアウトページを識別するためのロードルールを示しています。この例ではAND条件を使用しているため、以下の2つの条件を満たす必要があります：

* `pathname contains checkout.html`
* `product_category contains (ignore case) shoes`

両方の条件が真であれば、ロードルールは`true`と評価されます。
ANDステートメントの条件のいずれかが偽であれば、ロードルールは`false`と評価されます。

![](/images/iq-tag-management/load-rules-and-logic.png)

## ORロジック

以下の例はOR条件を使用しています。このルールは、`pathname`が`checkout.html`を含む場合、または`product_category`が`shoes`を含む場合に、ページ上のタグをロードします。ステートメントのいずれかが真であれば、ルールは真と評価されます。ORステートメントのすべてのステートメントが偽であれば、ロードルールは偽と評価されます。

![](/images/iq-tag-management/load-rules-or-logic.png)

ルールに複数のOR条件が含まれている場合、真のステートメントが見つかった時点でルールの評価が停止します。真のステートメントがあるということは、ルールが真であることを意味するため、残りのステートメントは評価されません。

## URLコンポーネントの使用

URLのコンポーネントは、ロードルール条件を作成する際に役立ちます。URLは通常、以下のコンポーネントで構成されています：

* **プロトコル** – URLを処理するための方法。例えば、HTTPまたはHTTPS。
* **ドメイン** – ドメイン名。例えば、[www.tealium.com.](http://www.tealium.com)
* **パス** – サイト上のセクションとページ。
* **ハッシュ** – ハッシュマーク（`#`）で始まり、ページ内のセクションを識別します。
* **クエリストリング** – クエスチョンマーク（`?`）で始まり、ページに渡される動的データを含むキー値パラメータを指定します。

URLの例：

`http://www.tealium.com/app/solutions/?example=test&amp;example2=test2#section3`

## データレイヤー変数

データレイヤーでは、ページURLのコンポーネントは以下のようにDOM変数に格納されます：

```
dom.domain       : &#34;www.tealium.com&#34;
dom.pathname     : &#34;/app/solutions/&#34;
dom.query_string : &#34;example=test&amp;example2=test2&#34;
dom.hash         : &#34;section3&#34;
dom.url          : &#34;http://www.tealium.com/app/solutions/?example=test&amp;example2=test2#section3&#34;
```

## ドメイン名の使用

サイトが複数のドメインで構成されている場合、特定のドメインのページにタグをロードするロードルールを作成する必要があるかもしれません。以下の例は、`domain1.com`のページのロードルールを示しています：

![](/images/iq-tag-management/load-rules-domain.png)

## ドメインとパス名の使用

`domain1.com`のホームページにタグをロードするには、以下のルールを使用します：

![](/images/iq-tag-management/load-rules-domain-pathname.png)

## パス名を使用してドメインのセクションを指定

`domain1`の`support`セクションのページにタグをロードするには、以下のルールを使用します：

![](/images/iq-tag-management/load-rules-any-support-page.png)

## パス名とハッシュ、またはクエリストリングの使用

`section2`というセクションを含む`support`ページ、またはクエリストリングが`support=true`を含む場合にタグをロードするには、以下のルールを使用します：

![](/images/iq-tag-management/load-rules-support-query-string.png)

## 時間ベースの条件の使用

ロードルールには、日付と時間の範囲を指定する時間ベースの条件を使用できます。日付と時間の範囲は、ルールがアクティブである時間期間を指定します。

ロードルールで使用される時間/タイムゾーンは、サーバーや訪問の時間/タイムゾーンではなく、訪問のブラウザによって決定されます。

ロードルールに日付範囲条件を追加するには、以下の手順を使用します。

1. **日付範囲条件を追加**をクリックします。  
日付と時間の範囲ダイアログが表示されます。  
    ![](/images/iq-tag-management/load-rules-date-time-range.png)
1. **開始日**フィールドをクリックして、カレンダーから開始日を選択します。
1. デフォルトの時間をクリックして、異なる開始時間を選択します。
1. **終了日**フィールドをクリックして、カレンダーから終了日を選択します。
1. デフォルトの時間をクリックして、異なる終了時間を選択します。
1. **適用**をクリックします。

## 特別な注意事項

以下の特別な注意事項が適用される場合があります：

* 時間範囲が指定されていない場合、デフォルトの値`any day`と`any time`が使用されます。
* フィールドをクリックしたときにハイライトされる日付または時間は、現在の日付または時間です。
* ロードルールごとに1つの日付範囲条件しか指定できません。  
タグに複数の日付範囲を適用するには、2つ目の日付範囲を持つ別のロードルールを作成する必要があります。

ブラウザのローカル時間の代わりにUTC時間を使用するには、[Time-based Load Rule using UTC](https://support.tealiumiq.com/en/support/solutions/articles/36000363440-time-based-load-rule-with-utc)を参照してください。