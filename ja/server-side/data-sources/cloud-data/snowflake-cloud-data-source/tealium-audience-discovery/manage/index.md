---
title: Tealium Audience Discovery for Snowflakeでオーディエンスを管理する
description: Snowflakeのデータからオーディエンスを作成し、Tealiumで管理します。
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/manage/
---
Snowflakeのデータからオーディエンスを作成し、時間をかけて管理します。Tealium Audience Discovery for Snowflakeは、各オーディエンスをテーブルとして保存し、Tealiumに接続するビューを持っています。

## 要件

* Tealium Audience Discovery for SnowflakeがSnowflakeアカウントにインストールされ、必要なロールと権限が構成されていること。[Tealium Audience Discovery for Snowflakeのインストール](https://docs.tealium.com/install-tealium-audience-discovery/)の手順を参照してください。
* 必要なデータベース、スキーマ、テーブルへのアクセス。

## オーディエンスを作成する

### ソースデータセット

1. Tealium Audience Discovery for Snowflakeを開く。
1. **Audiences**から**+ Create new audience**をクリックする。
1. オーディエンス名と説明を入力する。
1. データセットを定義する方法を選択する：

   * **Point & Click**
     1. **Database**、**Schema**、**Table / View**を選択する。
     1. 各ユーザーを一意に識別する**User ID column**を選択する。この列はレコードの重複を排除し、定期的な実行を通じて各ユーザーが一度だけ表示されることを保証するために使用されます。

   * **SQL (Advanced)**
     1. **Available Tables**からテーブルを選択する。
     1. データセットを定義するSQLクエリを入力する。
     1. (オプション) **AI Assistant**を使用して自然言語プロンプトからクエリを生成する。
     1. (オプション) **AI Syntax Check**を使用してクエリを検証する。
     1. **Preview Query**をクリックして結果を確認する。
     1. 各ユーザーを一意に識別する**User ID column**を選択する。

   * **Cortex**
     1. セマンティックビューを選択する。
     1. 大規模言語モデル（LLM）を選択する。
     1. オーディエンスセグメンテーションルールを説明する。
     1. **Generate Query**をクリックしてデータセットを作成する。
     1. **Preview Query**をクリックして結果を確認する。
     1. 各ユーザーを一意に識別する**User ID column**を選択する。

    
<blockquote>
Cortexメソッドは、Snowflakeアカウントにセマンティックビューが構成されていることを要求します。
</blockquote>


1. **Data Preview**を確認してデータセットを検証する：

   * プレビューには列名、データタイプ、行数が表示されます。
   * 各列のヒストグラムを使用して値の分布を理解します。
   * フィルタ条件を追加するとライブレコード数が更新されます。

   
<blockquote>
**User ID column**には各ユーザーの一意の値が含まれている必要があります。列に重複が含まれている場合、アプリは警告を表示し、続行を防ぎます。各ユーザーが一度だけ表示されるようにフィルタを定義するか、正しい列を特定するためにSnowflakeのデータチームと協力してください。
</blockquote>


1. **Next**をクリックする。

ソースデータセットからすべての列に加えて、オーディエンスメンバーシップを時間をかけて追跡するために使用される追加のTealium制御列がオーディエンステーブルに含まれます：

* `TEALIUM_CTRL_COL_INCREMENTAL_ID` — ユーザーがオーディエンスに初めて参加したときに割り当てられる連続増加ID
* `TEALIUM_CTRL_COL_CREATED_AT` — ユーザーが最初に追加されたとき
* `TEALIUM_CTRL_COL_LAST_UPDATED_AT` — ユーザーが最後にリフレッシュ処理されたとき
* `TEALIUM_CTRL_COL_MEMBERSHIP_CHANGED_AT` — ユーザーのメンバーシップステータスが最後に変更されたとき
* `TEALIUM_CTRL_COL_IS_ACTIVE` — ユーザーが現在オーディエンス基準に一致しているかどうか

これらの列は自動的に追加され、変更することはできません。

### オーディエンス基準

1. (オプション) オーディエンス基準を構成する：

   * フルデータセットプレビューを確認する。
   * **Point & Click**を使用して1つ以上のフィルタブロックを追加する。
   * 各ブロック内に条件を追加する。
   * 条件を定義する際に固定値（**VAL**）と参照列（**COL**）の間で切り替えるために**VAL** / **COL**トグルを使用する。
   * 各ブロックに単一のオペレータ（**AND**または**OR**）を選択する。

   
<blockquote>
フィルタブロック内のすべての条件は同じオペレータを使用します。異なるロジックを適用するには、複数のフィルタブロックを作成します。
</blockquote>


   ![](https://docs.tealium.com/images/server-side/data-sources/tealium-audience-discovery-filter-builder.png)

   * **Preview filtered dataset**をクリックして結果を確認する。
   * または、**SQL (Advanced)**を使用してWHERE句を使用してフィルタリングロジックを定義する。

1. **Next**をクリックする。

### リフレッシュスケジュール

1. リフレッシュスケジュールとタイムゾーンを構成する。

   初回実行がすべての一致するレコードを処理した後、後続の実行はユーザーID列に基づいて新しいレコードのみをロードします。

   
<blockquote>
より頻繁なスケジュールは、Snowflakeアカウントの計算コストを増加させます。
</blockquote>


1. **Next**をクリックする。

### レビューと作成

構成を確認し、**Create audience**をクリックします。

アプリはオーディエンスを作成し、初回ロードを実行し、すべての一致するレコードを処理します。オーディエンスの概要には、初回実行が完了するにつれてレコード数がゼロから増加することが表示されます。後続のスケジュールされた実行は新しいレコードのみを追加します。


<blockquote>
**Save as draft**を使用して、不完全なオーディエンス構成を保存し、後で続行します。ドラフトオーディエンスは、アクティブ化されるまで下流での使用はできません。
</blockquote>


## オーディエンスを管理する

**Audiences**画面を使用して、オーディエンスを表示、更新、管理します。

### オーディエンスの詳細を表示する

1. Tealium Audience Discovery for Snowflakeで**Audiences**に移動する。
1. テーブルからオーディエンスを選択する。

オーディエンスの詳細ビューには次の情報が表示されます：

* 現在のユーザー数と最後のリフレッシュからの変更
* データセット、クエリ、スケジュールを含むオーディエンス構成
* オーディエンス履歴グラフとリフレッシュ履歴
* データプレビュー

![](https://docs.tealium.com/images/server-side/data-sources/tealium-audience-discovery-audience-details.png)

### オーディエンスアクション

オーディエンスの詳細ビューまたはテーブルの**Actions**メニューから、次のアクションを実行します：

* **Edit** — データセット、基準、またはリフレッシュスケジュールを更新する  
* **Use as template** — 既存のものを基に新しいオーディエンスを作成する  
* **Share** — 接続の詳細をコピーして下流のユーザーと共有する  
* **Download CSV** — オーディエンスデータをエクスポートする  
* **Deactivate** — スケジュールされた更新を停止し、下流のユーザーからオーディエンスを非表示にする  
* **Delete** — オーディエンスを永久に削除する  


<blockquote>
**Share**を使用して、TealiumでSnowflakeデータソースを構成する際に必要な接続の詳細をコピーします。
</blockquote>


### オーディエンスデータをリフレッシュする

オーディエンスの詳細ビューで**Manual refresh**を使用して、すぐに更新を実行します。

スケジュールされたリフレッシュは、構成されたスケジュールに基づいて自動的に実行されます。各実行はオーディエンス履歴に記録され、実行が正常に完了していることを確認し、時間の経過とともにオーディエンスサイズがどのように変化するかを追跡します。

## オーディエンスメンバーシップの変更が追跡される方法

ユーザーがもはやオーディエンス基準を満たさなくなった場合、アプリはオーディエンステーブルからレコードを削除しません。

代わりに：
* `TEALIUM_CTRL_COL_IS_ACTIVE`は`false`に構成されます
* メンバーシップと更新のタイムスタンプが更新されます

ユーザーが再び基準を満たした場合：
* `TEALIUM_CTRL_COL_IS_ACTIVE`は`true`に構成されます
* タイムスタンプが再度更新されます

この動作は異なるアクティベーション戦略を可能にします：
* ユーザーが初めてオーディエンスに参加したときだけアクションをトリガーする
* ユーザーが再び資格を得たときに再度アクションをトリガーする

## 次のステップ

[TealiumにSnowflakeオーディエンスを接続する](https://docs.tealium.com/connect-snowflake-audiences/)ことで、アクティベーションのためのデータのロードを開始します。