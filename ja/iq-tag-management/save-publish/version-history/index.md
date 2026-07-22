---
title: バージョン履歴
url: https://docs.tealium.com/ja/iq-tag-management/save-publish/version-history/
---

<blockquote>
[プラットフォーム権限](https://docs.tealium.com/about-platform-permissions/)が有効なアカウントでは、クライアントサイドバージョンの権限を持つユーザーのみがこの画面にアクセスできます。詳細については、[権限グループ](https://docs.tealium.com/permission-groups/)を参照してください。
</blockquote>


保存と公開の履歴を表示するには、**クライアントサイドバージョン**に移動します。

![](https://docs.tealium.com/images/iq-tag-management/save-publish/versionhistory1.png)

* 現在公開されているリビジョンは青いフォルダとして表示されます。
* 以前のリビジョンは灰色のフォルダとして表示されます。
* バージョンは新しいレベルに表示されます。
* バージョン内のリビジョンは同じレベルに表示されます。
* 青いピンアイコンは、表示中のバージョンを示します。

## ビューフィルター

以下の基準の一つまたは複数を選択してバージョンをフィルタリングします：

* バージョンタイトル。デフォルトのタイトルはタイムスタンプで、バージョンが[アーカイブされている](#archived-versions)場合は**(アーカイブ済み)**が含まれます。
* ユーザー
* [バージョンラベル](https://docs.tealium.com/version-labels/)
* デフォルトの[公開環境](https://docs.tealium.com/about-publishing/)（**Dev**、**QA**、**Prod**、および**カスタム**）
* 公開/非公開の保存
* 時間範囲（日数）

![](https://docs.tealium.com/images/iq-tag-management/save-publish/versionhistory2.png)

## バージョンオプション

バージョンタイトルの横にある下矢印をクリックして、以下のアクションのいずれかを実行します：

![](https://docs.tealium.com/images/iq-tag-management/save-publish/versionhistory3.png)

* **このバージョンに切り替える**  
選択したバージョンを読み込みます。別のバージョンに切り替えると、表示中のバージョンのタイトルの隣にピンアイコンが自動的に移動します。
<blockquote>
[アーカイブされたバージョン](#archived-versions)には切り替えることができません。
</blockquote>

* **詳細の展開/非表示**  
公開タイムスタンプ、環境、およびそのバージョンを公開したユーザーを表示します。このオプションを使用して、各環境の`utag`ファイルを表示およびダウンロードします。
* **名前の変更**  
バージョンの名前をより説明的なタイトルに変更します。
* **コピーを作成する**  
現在のバージョンを複製します。バージョンを複製すると、保存され、バージョン名の先頭に**Duplicate of...**が追加されます。
<blockquote>
複製は自動的に公開されません。保存されたバージョンに戻り、公開を実行してください。
</blockquote>

* **このバージョン以降のメモを表示する**  
選択したバージョンおよびその後の公開のメモを表示します。メモは公開および保存されたバージョンの親バージョン内でインデントされた順に並べられます。

## 現在のセッションに変更をマージする

現在のセッションにマージ可能な変更がある場合、**現在のセッションに変更をマージする**オプションがバージョンアクションのリストとバージョン図の上に表示されます。

* **現在のセッションにマージする**ドロップダウンリストから、[このセッションにマージする](https://docs.tealium.com/merging-versions/)バージョンを選択します。受信バージョンと現在のバージョンは、同じ起源または祖先から派生している必要があります。
* ダッシュボードで**バージョン関係を表示する**フィルターを有効にして、各バージョンが他のバージョンとどのように関連しているか、およびどのバージョンをマージできるかまたはできないかを表示します。

## 以前のバージョンを公開する

プロファイルの以前のバージョンに戻って、任意の環境に再公開することができます。再公開されたバージョンには、古いバージョンの構成または構成が含まれます。

以前のバージョンを公開するには：

1. **タグ管理 > クライアントサイドバージョン**に移動します。  
すべてのバージョンが表示されます：**公開済み**、**未公開**、および**現在デプロイされている**。青いピンアイコンは現在のバージョンを示します。青いボタンは現在デプロイされているバージョンを示し、灰色のボタンは古いバージョンを指します。![](https://docs.tealium.com/images/iq-tag-management/save-publish/versionhistory4.png)
1. 以前のバージョンの下矢印をクリックし、**このバージョンに切り替える**を選択します。  
次のアラートメッセージが画面の上部に表示されます：  
**古いバージョンを表示しています。最新のバージョンに切り替える：バージョン名**
1. **保存/公開**をクリックします。
1. 再公開する環境を選択します：**Dev**、**QA**、または**Prod**。
1. バージョンに加えた変更についてのメモを追加します。
1. **公開**ボタンをクリックして確認します。  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-versions-bluepin-moves-to-latest-saved-version.png)  

    青いピンアイコンが公開されたバージョンに移動します。

## 公開されたutag.jsファイルを表示する

公開された`utag.js`ファイルを表示するには：

1. 現在公開されているバージョンの横にある下矢印をクリックし、**詳細を展開する**を選択します。
1. **Dev公開の詳細**の横にある下矢印をクリックして展開します。
1. **utag.jsを表示する**をクリックします。  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-versions-viewpublishdetails-view-utag-js.png)<br>
    対応する`utag.js`ファイルが新しいタブで開きます。

## タグとタグアイテムの履歴を表示する

タグ、拡張機能、ロードルール、イベントの変更履歴を個別に表示できます：

* **タグ**：[タグ詳細ページ](https://docs.tealium.com/manage-tags/#view-tag-history)で**変更履歴**をクリックします。
* **拡張機能**：[拡張機能詳細ページ](https://docs.tealium.com/manage-extensions/#view-extension-change-history)で**変更履歴を表示する**をクリックします。
* **ロードルール**：[ロードルール詳細ページ](https://docs.tealium.com/manage-load-rules/#view-load-rule-details)で**変更履歴**をクリックします。
* **イベント**：[イベント詳細ページ](https://docs.tealium.com/manage-events/#view-event-details)で**変更履歴**をクリックします。

## diffツールの使用

diffツールを使用すると、2つの公開されたバージョンを比較し、それらのディストリビューションファイルからのコード変更を確認できます。バージョン間のコードの違いは強調表示され、並べて表示されるため、変更を区別するのが簡単です。

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-distrofilecomparison.png)

詳細については、[バージョンdiffツール](https://docs.tealium.com/version-diff-tool/)の記事を参照してください。

## バージョン間の変更をマージする

バージョン間の変更をマージすることは、古いバージョンから現在公開されているバージョンに変更を取り込むプロセスを簡素化します。2つのバージョンをマージするには、それらが同じ起源から分岐している必要があります。詳細については、[現在のセッションにマージする](https://docs.tealium.com/merging-versions/)を参照してください。

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-versions-merge-into-current-session.png)

## アーカイブされたバージョン

古くて使用されていないバージョンは、サイトのパフォーマンスを向上させるためにアーカイブされます。アーカイブされたバージョンは、タイトルに**(アーカイブ済み)**が含まれてバージョン履歴に表示されます。アーカイブされたバージョンは読み込むことができません。アーカイブされたバージョンを使用する必要がある場合は、Tealiumサポートに連絡してください。