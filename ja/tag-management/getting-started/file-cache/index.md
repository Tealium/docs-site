---
title: Tealiumによるファイルのキャッシュ方法
url: https://docs.tealium.com/ja/tag-management/getting-started/file-cache/
---
Tealiumから配信されるファイルでは、`Cache-Control`ヘッダーを構成し、新しいバージョンを確認するまでファイルをキャッシュする期間をブラウザに指示します。キャッシュ期間（「生存時間」を意味するTTLと呼ばれることもあります）が終了すると、ブラウザはTealiumのサーバーにヘッダーリクエストを送信し、ファイルが変更されているかどうかを確認します。変更されている場合、ブラウザは最新のファイルを取得します。変更されていない場合は、キャッシュされたファイルを引き続き使用します。

Universal Tag（`utag.js`）のTTLは短く構成されています。これにより、パブリッシュ後、Webサイトの訪問は最新バージョンの`utag.js`ファイルをできるだけ早く取得できます。

## ブラウザのキャッシュ時間

Tag Managementからパブリッシュされるファイルのブラウザキャッシュ有効期限は、次のとおりです。

|Tealiumファイル|キャッシュ有効期限（TTL）|
|---|---|
|`utag.js`|5分|
|`utag.#.js`|5分|
|`utag.sync.js`|5分|
|`mobile.html`|1時間（qa/prod）<br>5分（dev）|

## Universal Tagのキャッシュ

Universal Tagの4.26より前のバージョンでは、パブリッシュ後にすべての`utag.js`ファイルが更新されていました。パブリッシュのたびに`utag.js`ファイルのキャッシュが無効化され、ブラウザが変更されていないファイルを取得するために不要なネットワーク呼び出しを行っていたため、ページ読み込みのパフォーマンスに影響していました。

[バージョン4.26以降](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2014-01-01)では、ブラウザのキャッシュが利用されるため、ネットワーク呼び出しが減少し、ページ読み込みのパフォーマンスが向上します。


<blockquote>
For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
</blockquote>


## 仕組み

キャッシュ動作は、パブリッシュされたファイルのURLに追加される`utv`という名前のタイムスタンプパラメータによって制御されます。これは「キャッシュバスティング」パラメータと呼ばれます。キャッシュバスティングパラメータによってファイルのURLが変更されるため、ブラウザはキャッシュ済みのファイルを強制的に更新します。Universal Tagのバージョン4.39以降では、`utv`パラメータの値にタイムスタンプとバージョン番号が含まれます。

Universal Tagのバージョン別のキャッシュバスティングパラメータ値は、次のとおりです。

|バージョン|説明|例|
|---|---|---|
|v4.26～v4.38|タイムスタンプにバージョン番号が含まれない|`utag.#js?utv=201510202208`|
|v4.39以降|タイムスタンプの先頭にバージョン番号がエンリッチメントされる|`utag.#.js?utv=ut4.39.201510202208`|

変更されていない`utag.#.js`ファイルでは、パブリッシュ間でタイムスタンプ値が変わらないため、ブラウザにキャッシュされた状態が維持されます。


<blockquote>
The [Currency Converter Extension](https://docs.tealium.com/currency-converter-extension/) is never cached.
</blockquote>


## 例

次の例では、UID #4のタグを変更または追加し、タグ#1を非アクティブ化しています。タグ#2とタグ#3には変更を加えていません。

![](https://docs.tealium.com/images/tag-management/example-tags.png)

WebコンソールのパブリッシュURLビューでは、`utag.4.js`が新規ファイルまたは変更されたファイルであるため、サーバーから取得されていることがわかります。`utag.2.js`と`utag.3.js`は変更されていないため、どちらもキャッシュから取得されています。`utag.1.js`は非アクティブ化されているため、ページに読み込まれていません。

![](https://docs.tealium.com/images/tag-management/timestamps-on-qa.png)