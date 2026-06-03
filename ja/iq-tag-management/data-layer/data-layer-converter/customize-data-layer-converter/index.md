---
title: データレイヤーコンバーターのカスタマイズ
url: https://docs.tealium.com/ja/iq-tag-management/data-layer/data-layer-converter/customize-data-layer-converter/
---
以下のユーティリティ関数を使用して、コンバーターの動作をカスタマイズします：

### `teal.ignore_keys`

オブジェクトのキーがこのテキストで始まる場合、そのキーは取り込まれないテキストの文字列を指定します。

例のオブジェクト：  
```js
teal.ignore_keys = {
  &#34;user&#34; : 1,
  &#34;util&#34; : 1
};
```

このアクションは、ソースデータオブジェクトからのすべてのキーが、文字列 &#34;user&#34; または &#34;util&#34; で始まる場合にスキップされる結果となります。

### `teal.prefix`

変換されたすべてのキー名に使用する文字列を構成します。例えば、`utag_data`と`dataLayer`をマージする場合、変換された変数に`dl_`のプレフィックスを構成できます。上記の`dataLayer`の例を使用すると、変換されたオブジェクトは以下を含むことになります：

```json
{
   &#34;dl_user.userInfo.sub_industry&#34; : &#34;data &amp; technical services&#34;,
   &#34;dl_user.userInfo.web_site&#34;     : &#34;tealium.com&#34;
}
```

### `teal.nested_delimiter`

変換された名前のサブキー名を区切るために使用される文字を構成します。デフォルトの区切り文字はピリオド（**.**）です。

### `teal.replace_keys`

変換されたキーの新しい名前を指定します。キー名を新しい名前に置き換えるか、キーを削除することができます。

例：  
```js
teal.replace_keys = {
    &#34;pageInfo&#34; : &#34;&#34;
};
```

ソースオブジェクトには`pageInfo`が含まれており、これを変換オブジェクトでは`pi`として表示したい場合、例えば、`digitalData.page.pageInfo.pageName`は`digitalData.page.pi.pageName`に変更されます。
