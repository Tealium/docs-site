---
title: utag.js のセルフホスティング
description: このガイドでは、utag.js ファイルをセルフホスティングするための構成とワークフローについて説明します。
url: https://docs.tealium.com/ja/tag-management/getting-started/install/self-host/
---

<blockquote>
開始する前に、アカウントマネージャーに連絡して、この機能に関する契約条件を確認し、機能の利用可否と適切なライセンスが維持されていることを確認してください。
</blockquote>


## 概要

Tealium は、`utag.js` ファイルを Tealium のサーバーにパブリッシュします。ウェブサイトに `utag.js` を実装すると、ファイルは `tags.tiqcdn.com` から読み込まれます。外部の JavaScript ファイルを読み込めない要件がある場合（またはその他の制約がある場合）は、これらのファイルを独自のサーバーでセルフホスティングできます。生成された `utag` ファイルは引き続き Tealium のサーバーにパブリッシュされますが、システムに転送可能な `.zip` アーカイブとしても提供されます。

セルフホスティングにおける主な違いは、ウェブサイトで `utag.js` を読み込むために使用するコードスニペットです。ファイルのドメインとパスを、そのファイルをホストするサーバーの場所に合わせて更新する必要があります。次の例では、URL を Tealium の標準の場所からセルフホスティング先へ変更しています。

## セルフホスティングされた Universal Tag

セルフホスティングされた Universal Tag の場合、コードスニペット内の `tags.tiqcdn.com` を、タグをホストするサーバーのアドレスに置き換えます。

```html
<!-- Tealium Universal Tag -->
<script type="text/javascript">
(function(a,b,c,d){
a='//YOURDOMAIN.com/CUSTOM/PATH/[ENV]/utag.js';
b=document;c='script';d=b.createElement(c);d.src=a;
d.type='text/java'+c;d.async=true;
a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a)
})();
</script>
```

サイトへのタグの追加について詳しくは、[Universal Tag（utag.js）のインストール](https://docs.tealium.com/ja/platforms/javascript/install/#universal-tag-utag-js)を参照してください。

## .zip アーカイブの有効化

最初の手順は、Tealium から必要なファイルを取得できるように、zip アーカイブの生成を有効にすることです。zip アーカイブの名前は `distro.zip` で、パブリッシュが行われるたびに更新されます。このアーカイブには、`utag.js` のインスタンスを実行するために必要なすべてのファイルが含まれています。このファイルはデフォルトでは生成されないため、有効にする必要があります。

distro ファイルを有効にするには、次の手順を実行します。

1. 管理メニューで、**パブリッシュ構成を構成**をクリックします。**パブリッシュ構成**ダイアログが表示されます。
1. **一般パブリッシュ**タブの**実装**セクションで、**distro.zip ファイルを生成**構成を見つけて、**オン**に切り替えます。
1. **保存**をクリックします。

![](https://docs.tealium.com/images/tag-management/iq-self-hosting-generate-distro-zip.jpg)

### パブリッシュ済みファイルの場所の構成

パブリッシュ済みファイルの場所は、後続の utag ファイル（たとえば、`utag.4.js`）をどこから読み込むかを `utag.js` コードに指示する構成です。`utag.js` を読み込むコードスニペットは、カスタムのセルフホスティング先を使用するように調整されますが、その他の utag ファイルは `utag.js` 内のロジックに基づいて動的に読み込まれ、デフォルトでは Tealium のサーバーから読み込まれることに注意してください。

パブリッシュ済みファイルの場所を変更するには、次の手順を実行します。

1. 管理メニューで、**パブリッシュ構成を構成**をクリックします。**パブリッシュ構成**ダイアログが表示されます。
1. **一般パブリッシュ**タブの**パブリッシュ URL**セクションで、セルフホスティングされたファイルのドメインと完全なパスを環境ごとに入力します（実際のファイル名は省略します）。例：`//example.com/custom/path/prod/`
1. **保存**をクリックします。


<blockquote>
組み込みの開発、QA、本番の各ターゲットをサポートするため、パスに環境を含めてください。
</blockquote>


### すべての環境へのパブリッシュ

これで、ダウンロード可能な `distro.zip` ファイルが有効になりました。**コードセンター**のコードスニペットに、Tealium の場所ではなく、ホストしている `utag.js` のカスタムの場所が表示されるようになります。

![](https://docs.tealium.com/images/tag-management/iq-self-hosting-code-center.jpg)

最後の手順は、プロファイルをすべての環境ターゲット（開発、QA、本番）にパブリッシュすることです。この手順により、環境ごとに `distro.zip` ファイルが生成されます。

### パブリッシュワークフロー

![](https://docs.tealium.com/images/tag-management/iq-self-hosting-version-download.jpg)

タグの管理は引き続き Tealium 内で行いますが、保存してパブリッシュするたびに、新しい `distro.zip` ファイルをダウンロードし、独自のサーバー上でファイルを展開する必要があります。

`distro.zip` ファイルをダウンロードして確認するには、次の手順を実行します。

1. **バージョン**タブで、最後にパブリッシュされたバージョンを探し、各環境の**パブリッシュの詳細**を展開して、**Distro Zip ファイルをダウンロード**をクリックします。
1. カスタムの**パブリッシュ URL**構成で指定したサーバー上の場所に、`distro.zip` ファイルを展開します。`distro.zip` には、次のファイルが含まれている必要があります。
    * `utag.js`：Universal Tag。ロードルールと条件に基づいてタグを読み込み、実行するコードをロードして実行します。
    * `utag.#.js`：個々のタグコード。`#` はタグの UID を表します。例：`utag.1.js`
    * `utag.sync.js`：A/B テストおよび多変量テストのタグをサポートするため、ページの読み込み前に実行されるコードです。
    * `utag.v.js`：セッション数の計測と請求に必要なファイルです。
    * `mobile.html`：モバイル構成ファイルです。
1. **コードセンター**のコードを使用して、`utag.js` のコードスニペットをウェブサイトに追加します。
1. ブラウザーコンソールを使用して、ウェブページが Tealium（たとえば、`tags.tiqcdn.com`）ではなく、セルフホスティング先から `utag.js` を読み込んでいることを確認します。

#### バージョンラベルの使用

最後に、`utag` ファイルを本番サイトで利用可能にした後、**[バージョンラベル]()**を使用して、Tealium でリリース済みバージョンにラベルを付けることをお勧めします。バージョンラベルは、社内のソフトウェアリリースサイクルを完了したバージョンを、アカウントのユーザーに示します。

![](https://docs.tealium.com/images/tag-management/self-hosted-version-label.jpg)

### SHA256 ダイジェスト署名

セキュリティをエンリッチメントするには、`distro.zip` をダウンロードしたパブリッシュ詳細領域で、**Distro 検証**リンクをクリックしてファイルの内容を確認します。**Distro 検証**には、アーカイブ内の各ファイルの SHA-256 チェックサムが表示されます。

![](https://docs.tealium.com/images/tag-management/self-hosted-sha256-digest.jpg)

任意の[チェックサム](https://en.wikipedia.org/wiki/Checksum)ユーティリティを使用して、ホスティング先にあるファイルのダイジェスト署名を確認します。次の図は `utag.js` の SHA-256 チェックサムを示しており、Tealium に表示される値と一致しています。

![](https://docs.tealium.com/images/tag-management/self-hosted-shasum.jpg)