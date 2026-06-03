---
title: トラッキングコールの変換
url: https://docs.tealium.com/ja/iq-tag-management/data-layer/data-layer-converter/convert-tracking-calls/
---
Tealiumのトラッキングコールにサードパーティのデータレイヤーオブジェクトを渡している場合、トラッキングコールのデータレイヤーを変換する必要があります。

例：

```js
utag.link({
    &#34;event&#34; : {
        &#34;type&#34;: &#34;cart&#34;,
        &#34;name&#34;: &#34;add to cart&#34;,
        &#34;items&#34; : [{
            &#34;id&#34;: &#34;prod123&#34;,
            &#34;price&#34;: &#34;123.45&#34;,
            &#34;qty&#34;: &#34;2&#34;
        }]
    }
});
```

## 拡張機能を追加する

以下の手順でデータレイヤーのトラッキングコールを変換します：

1. 左側のサイドバーで、**iQ Tag Management &gt; Extensions**に移動します。
1. [JavaScript extension]()を追加します。
1. **Title**フィールドに`Convert Tracking Calls`と入力します。
1. **Draft Name**フィールドにドラフトの名前を入力します。
1. **Scope**フィールドで**All Tags**を選択します。
1. 実行を**Before Load Rules**に変更します。
1. 次のコードを拡張機能のJavaScriptフィールドにコピーして貼り付けます：  
    ```js
        teal.flattenObject(b,b);
    ```
1. **Approve for Publish**をクリックします。
1. 一つ以上の公開環境を選択し、**Apply**をクリックします。  
1. 変更を保存し、公開します。
