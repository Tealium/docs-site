---
title: コネクタの管理
description: この記事では、コネクタの管理方法について説明します。これには、コネクタの有効化または無効化、コネクタの複製と削除、コネクタまたはアクションUIDの取得が含まれます。
url: https://docs.tealium.com/ja/server-side/connectors/manage/
---
コネクタを追加する方法については、[コネクタの追加]()を参照してください。

## コネクタの有効化または無効化

コネクタを無効化すると、そのコネクタのアクションは一切実行されません。特定のアクションを無効化するには、そのアクションを無効化してください。詳細については、[コネクタアクションの有効化または無効化]()を参照してください。

コネクタを有効化または無効化するには、以下の手順を実行します：

1. **Server-Side > Connect > Connectors** に移動します。
1. 有効化または無効化するコネクタの横にあるチェックボックスをクリックします。  
同じステータスの複数のコネクタを選択することができます。選択したコネクタの数と取れるアクションが表示されるツールバーが表示されます。例：  
![](https://docs.tealium.com/images/server-side/connectors/activate-deactivate.png)
1. **Activate** または **Deactivate** をクリックします。
1. 保存して公開します。

コネクタを有効化した後、コネクタアクションを有効化することができます。

## アクションの有効化または無効化

アクションを有効化または無効化するには、以下の手順を実行します：

1. **Server-Side > Connect > Connectors** に移動します。
1. コネクタをクリックし、**Actions** タブをクリックします。
1. 有効化または無効化するアクションの横にあるチェックボックスをクリックします。  
同じステータスの複数のアクションを選択することができます。選択したアクションの数と取れるアクションが表示されるツールバーが表示されます。例：  
![](https://docs.tealium.com/images/server-side/connectors/activate-actions.png)
1. **Activate** または **Deactivate** をクリックします。
1. 保存して公開します。

## アクションタイプの変更

アクションのアクションタイプを変更するには、以下の手順を実行します：

1. **Server-Side > Connect > Connectors** に移動します。
1. コネクタをクリックし、**Actions** タブをクリックします。
1. アクションをクリックします。**Action Details** 画面が表示されます。
1. 画面の右上隅にあるその他のアクションボタンをクリックし、**Change Action Type** をクリックします。
    ![](https://docs.tealium.com/images/server-side/connectors/change-action-type.png)
1. 使用したいアクションタイプを選択し、**Done** をクリックします。警告メッセージが表示されます。
1. 変更を確認するには **Change Action Type** をクリックし、キャンセルするには **Cancel** をクリックします。
1. 必要に応じてデータマッピングを更新します。詳細については、[データマッピング](https://docs.tealium.com/add-connector/#data-mappings)を参照してください。
1. **Done** をクリックします。
1. 保存して公開します。

## コネクタの複製

コネクタと関連するアクションを複製するには、以下の手順を実行します：

1. **Server-Side > Connect > Connectors** に移動します。
1. コネクタメニューをクリックし、**Duplicate** をクリックします。  
    ![](https://docs.tealium.com/images/server-side/connectors/duplicate-connector.png)  
    リストに新しい、同一のコネクタが表示されます。これには関連するアクションも含まれ、コネクタ名には **- copy** が追加されます。  
    ![](https://docs.tealium.com/images/server-side/connectors/duplicate-copy.png)
1. (推奨) 複製したコネクタをクリックし、コネクタ名を変更します。
1. (オプション) 新しいコネクタに関連するアクションを追加または編集するには、**+ New Action** をクリックし、アクションを追加する通常の手順に従います。
1. **Done** をクリックします。
1. 保存して公開します。

## コネクタの削除

コネクタを削除するには、以下の手順を実行します：

1. **Server-Side > Connect > Connectors** に移動します。  
1. コネクタメニューをクリックし、**Delete** をクリックします。  
コネクタに関連するアクションがある場合、コネクタのすべてのアクションを削除するかどうかを確認するプロンプトが表示されます。
1. コネクタとすべてのアクションを削除するには **Delete** をクリックします。
1. コネクタとすべてのアクションを保持するには **Cancel** をクリックします。
1. 保存して公開します。

## コネクタアクションの削除

コネクタアクションを削除するには、以下の手順を実行します：

1. **Server-Side > Connect > Connectors** に移動します。
1. その行をクリックしてコネクタを選択します。**Connector Details** 画面が表示されます。
1. **Actions** タブをクリックします。
1. 削除したいアクションのアクションメニューをクリックし、**Delete** を選択します。
1. 確認ダイアログで **Delete** をクリックします。
1. 保存して公開します。


## お気に入りに追加

**Favorite** フィルターメニューを使用して簡単に見つけるために、コネクタをお気に入りにマークします。

コネクタをお気に入りにマークする方法はいくつかあります：

**Connectors Overview** 画面で、コネクタ名の横にある星をクリックします。  
![](https://docs.tealium.com/images/server-side/connectors/connectors-favorites-star.png)

コネクタの詳細画面で、上部のアクションバーで **Favorite** をクリックします。  
![](https://docs.tealium.com/images/server-side/connectors/connectors-details-favorite.png)

## コネクタアクションに対する一括アクションの実行

複数のアクションに対して同時に以下のアクションを実行することができます：

* 有効化
* 無効化
* ラベルの編集
* 削除

コネクタアクションに対して一括アクションを実行するには、以下の手順を実行します：

1. **Server-side > Connect > Connectors** に移動します。
1. その行をクリックしてコネクタを選択します。**Connector Details** 画面が表示されます。
1. **Actions** タブをクリックします。
1. 変更または削除したい各アクションのボックスをクリックします。  
または、すべてのアクションを選択するには、テーブル見出しの **Name** の横のボックスをクリックします。  
次のようにアクションツールバーが表示されます：  
![](https://docs.tealium.com/images/server-side/connectors/bulk-actions-toolbar.png)
1. 適切なアクションをクリックします：**Edit Labels** または **Delete**。  
**Delete** を選択した場合、確認ダイアログで **Delete** をクリックします。**Edit Labels** を選択した場合、追加または削除するラベルを選択します。

## コネクタIDの取得

コネクタのコネクタIDを取得するには、以下の手順を実行します：

1. **Server-Side > Connect > Connectors** に移動します。
1. その行をクリックしてコネクタを選択します。  
**Connector Details** 画面が表示され、コネクタ名の下にコネクタのUIDが表示されます。例：  
![](https://docs.tealium.com/images/server-side/connectors/get-uid.png)
1. コネクタUIDをコピーするには、UIDテキストを選択し、右クリックして **Copy** を選択します。

## アクションIDの取得

コネクタアクションのアクションIDを取得するには、以下の手順を実行します：

1. **Server-Side > Connect > Connectors** に移動します。
1. その行をクリックしてコネクタを選択します。
1. **Connector Details** 画面で、**Actions** タブをクリックします。
1. その行をクリックしてアクションを選択します。  
**Action Details** 画面が表示され、アクション名の下にアクションのUIDが表示されます。例：  
![](https://docs.tealium.com/images/server-side/connectors/get-action-uid.png)
1. アクションUIDをコピーするには、UIDテキストを選択し、右クリックして **Copy** を選択します。

## 以前のコネクタバージョンに戻す

**Version History** を使用して以前のコネクタバージョンに戻すことができます。詳細については、[サーバーサイドバージョン履歴]()を参照してください。