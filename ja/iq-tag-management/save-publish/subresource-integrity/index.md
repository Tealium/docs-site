---
title: サブリソースインテグリティ公開ワークフロー
description: この記事では、訪問がTealium CDNを通じて有効なutag.jsファイルを受け取ることを保証するために、サブリソースインテグリティを実装する方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/save-publish/subresource-integrity/
---
## 仕組み

SRI（Subresource Integrity）がTealiumプロファイルで有効になっている場合、ユーザーはハッシュコードを生成し、ブラウザはそれをTealium CDNが提供する`utag.js`ファイルと照合します。

以下の例は、新しい`integrity`パラメータを示しています：

```
&lt;script src=&#34;https://tags.tiqcdn.com/utag/account/profile/PROD-A/utag.v202012030630.js&#34; integrity=&#34;sha256-9/abcdefghijklmnopqrstuvwx/abcdefghijklmnopq0=&#34; crossorigin=&#34;anonymous&#34; async&gt;&lt;/script&gt;
```

訪問がブラウザを通じて`utag.js`ファイルをロードすると、ハッシュはファイルの検証に使用されます。ハッシュがファイルの内容と一致する場合、`utag.js`ファイルは有効であり、ページにロードされます。ハッシュが一致しない場合、これはファイルがソースから変更されたことを示し、予防措置として、ブラウザは`utag.js`ファイルのロードをブロックします。

SRIについての詳細は、[Mozillaの開発者向けドキュメンテーションのSubresource Integrity](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)を参照してください。

## 前提条件

* すべてのタグをバンドルする必要があります。
* 公開権限を持つすべてのユーザーに**Devへの公開**の権限を付与し、カスタム環境に公開できるようにします。
* 新しい`integrity`パラメータと正しいプロファイル名を含めるように、すべての影響を受けるページのソースコードを更新します。例えば、**DEV-A**、**QA-2**、**PROD-BETA1**などです。詳細は、以下の[Naming convention](#naming-convention)を参照してください。
* 公開環境を変更するプロセス（例えば、**PROD-A**から**PROD-B**へ）を開発し、トラッキングのギャップを避けるために、同時に`integrity`パラメータを更新します。詳細は、以下の[Hash coordination](#hash-coordination)を参照してください。

### 命名規則

プロファイルにSRIを実装するには、各プロファイルの公開URLで特定の命名規則に従う必要があります。また、この命名規則に従ったカスタム環境を各プロファイルで作成する必要があります。

SRI用に作成するカスタム公開環境は、以下の命名規則を使用する必要があります：

1. 次のいずれかのプレフィックスで始めます：
	* **DEV-**
	* **QA-**
	* **PROD-**
		
1. 上記のプレフィックスに続いて、任意の大文字（A-Z）または数字（0-9）を使用できます。例えば、**DEV-A**、**QA-2**、**PROD-BETA1**などです。

有効な公開URLは以下のようになり、`PROD-C`はカスタム公開環境名を表します：
```
https://tags.tiqcdn.com/utag/account/profile/PROD-C/utag.js
```
ベストプラクティスとして、必要な数のSRI環境を各環境カテゴリーごとに作成し、公開時にそれらをローテーションさせることをお勧めします。例えば、プロファイルを**DEV-A**、**QA-A**、**PROD-A**に公開した場合、次回の公開では**DEV-B**、**QA-B**、**PROD-B**に公開し、アクティブなプロファイルを操作してSRIチェックを無効にしないようにします。

### ハッシュの調整

プロファイルを公開し、ライブサイトを更新するときは、`utag`パスと`integrity`パラメータのSRIハッシュを同時に更新して、正しいカスタム環境を使用する必要があります。そうしないと、パスとSRIハッシュが競合し、ブラウザは`utag`をロードしません。

 ベストプラクティスとして、開発チームと協力して、これをCMSワークフローに組み込み、一緒に更新できるようにすることをお勧めします。

## SRIのプロファイル構成

SRIのプロファイルを構成するには、以下の手順を実行します：

### ステップ1 - カスタム環境を有効にする

プロファイルでカスタム環境を有効にするには、[Custom publish environments]()を参照してください。

### ステップ2 - カスタム環境を作成する

SRIのために必要なカスタム公開環境を作成するには：

1. 管理メニューで、**Code Center**をクリックします。
1. **Add Environment**をクリックします。
1. **Environment Name**の下に、有効なプレフィックス（**DEV-**、**QA-**、または**PROD-**）で始まる命名規則に従った名前を入力します。![](/images/iq-tag-management/save-publish/subresourceintegrity1.png)
1. 新しいカスタム環境をすべて作成した後、プロファイルの**Environments**リストは次のようになります：![](/images/iq-tag-management/save-publish/subresourceintegrity2.png)
1. **OK**をクリックします。
1. 新しいカスタム環境をすべて作成するために、プロファイルを任意の環境で**Save/Publish**します。

詳細については、[Custom publish environments]()を参照してください。

### ステップ3 - カスタム環境に公開する

SRI環境を持つプロファイルへの保存と公開のプロセスは、デフォルトの公開ワークフローとほぼ同じですが、一度に公開できる環境は1つだけです。

詳細については、[Custom publish environments]()を参照してください。

