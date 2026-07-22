---
title: 環境の管理
description: 環境管理画面では、ウェブサイトにユニバーサルタグ（utag.js）を追加するためのコードスニペットを取得したり、カスタム公開環境を作成することができます。
url: https://docs.tealium.com/ja/iq-tag-management/save-publish/manage-environments/
---

<blockquote>
[Code Center](https://docs.tealium.com/code-center/) 画面は、[platform permissions](https://docs.tealium.com/about-platform-permissions/) を使用するアカウントでは [Manage Environments](https://docs.tealium.com/manage-environments/) 画面に置き換えられました。レガシー権限を使用するアカウントは引き続き Code Center 画面を使用します。
</blockquote>


ウェブサイトに Tealium をインストールする方法の詳細については、[Web用クイックスタートガイド](https://docs.tealium.com/getting-started-web/)を参照してください。

## 環境管理へのアクセス

環境管理画面にアクセスするには、管理メニューで **環境の管理** をクリックします。

![](https://docs.tealium.com/images/iq-tag-management/save-publish/manage-environments.png)

**公開環境の構成** テーブルには、アカウントで利用可能な環境がリストされています：

* **環境名**: 環境名は、デフォルトの3つの環境（Dev、QA、Prod）または Tealium が公開するカスタム環境のいずれかです。デフォルト環境名は変更できませんし、カスタム環境名も作成後に変更することはできません。
* **環境エイリアス**: エイリアスはプラットフォーム全体で表示されます。デフォルト環境のエイリアスは変更できます。
* **必要な公開権限**: この環境に公開するために必要な権限です。公開環境に必要な権限を変更できるのは [profile admins](https://docs.tealium.com/admin-roles/#profile-admin) のみです。

各環境には編集アイコンと削除アイコンが表示されます。3つのデフォルト環境は削除できません。

## 環境の表示または編集

**環境管理** 画面で環境名をクリックして、環境の詳細を表示します：

![](https://docs.tealium.com/images/iq-tag-management/save-publish/edit-environment.png)

環境を編集するには：

1. 環境名をクリックします。
   **環境の編集** 画面が表示されます。
1. デフォルト公開環境の場合、環境の新しいエイリアスを入力します。プラットフォームはエイリアスを環境名の代わりに表示します。たとえば、DevをDevelopmentに変更すると、**保存/公開** ウィンドウに次のように表示されます：![](https://docs.tealium.com/images/iq-tag-management/save-publish/environment-aliases.png)
1. カスタム公開環境の必要な権限を変更できます。新しい環境の必要な公開権限を選択します：
    * Devへの公開
    * QAへの公開
    * Prodへの公開
1. **保存** をクリックします。

### コードスニペット

ユニバーサルタグは `utag.js` と呼ばれる小さな JavaScript コードで、サイトにサードパーティのタグを読み込むために必要なすべての生成コードを含んでいます。これにより、Tealium iQ タグ管理は以下のコードをページに挿入することでタグを発火させます：

<!-- Tealium Universal Tag -->
<script type="text/javascript">
  (function(a,b,c,d) {
      a='//tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/utag.js';
      b=document;c='script';d=b.createElement(c);d.src=a;
      d.type='text/java'+c;d.async=true;
      a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a)})();
</script>

**環境の編集** 画面の **コードスニペット** セクションには、ウェブページにユニバーサルタグ (`utag.js`) を追加する際に `a=` 行を更新する必要があるコードスニペットが表示されます。

`utag.js` のコードスニペットは次のようになります：

```html
//tags.tiqcdn.com/utag/[ACCOUNT]/[PROFILE]/[ENV]/utag.js
```

画面には `utag.sync.js` バージョンのコードも提供されます：

```html
//tags.tiqcdn.com/utag/[ACCOUNT]/[PROFILE]/[ENV]/utag.sync.js
```

* `[ACCOUNT]` はアカウント名を表します。
* `[PROFILE]` はプロファイル名を表します。
* `[ENV]` は環境名を表します。

たとえば、`example` アカウントの `sample` プロファイルの `prod` 環境の場合、**環境の編集** 画面には次のように表示されます：

```html
//tags.tiqcdn.com/utag/example/sample/prod/utag.js
```

**クリップボードにコピー** をクリックしてコードスニペットをコピーします。

ウェブページにユニバーサルタグをインストールする方法の詳細については、[ユニバーサルタグ (`utag.js`) のインストール](https://docs.tealium.com/ja/platforms/javascript/install#universal-tag-utag-js)を参照してください。

## カスタム公開環境

3つのデフォルト環境以上が必要な場合は、カスタム環境を作成できます。

詳細については、[カスタム公開環境](https://docs.tealium.com/custom-publish-environments/)を参照してください。

## カスタム公開環境の追加

カスタム公開環境を作成するには：

1. 管理メニューで **環境の管理** をクリックします。**環境の管理** ダイアログが表示されます。
1. **+ 環境を追加** をクリックします。
1. 新しい環境の名前を入力します。環境名には数字と文字のみを含めることができます。環境名にスペースや特殊文字は使用できません。
1. 新しい環境の必要な公開権限を選択します：
    * Devへの公開
    * QAへの公開
    * Prodへの公開
1. **環境を追加** をクリックします。
1. プロファイルを保存して公開します。

カスタム公開環境を作成すると、プロファイルのすべてのタグ、拡張機能、イベントリスナーの **公開場所** に追加されます。

カスタム公開環境についての詳細は、[custom-publish-environments](https://docs.tealium.com/custom-publish-environments/)を参照してください。

## カスタム公開環境の削除

カスタム環境を削除するには、**環境の管理** 画面で削除アイコンをクリックします。削除を確認するプロンプトが表示されます。