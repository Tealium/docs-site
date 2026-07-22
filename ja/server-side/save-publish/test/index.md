---
title: テストについて
description: この記事には、Tealiumプラットフォームのサーバーサイドでの公開プロセスに関するメモが含まれています。
url: https://docs.tealium.com/ja/server-side/save-publish/test/
---
サーバーサイドの構成には**Dev**環境や**QA**環境がないため、ライブ環境にリリースする前に変更をテストするには追加のステップが必要です。テストフラグ、バッジ、ルールの力を利用して、いくつかの方法で構成可能なテストユーザーに新機能を簡単に制限できます。

## テストイベント

ライブイベントとテストイベントを分離する方法はいくつかあります。目標は、すべての関連テストデータイベントにこのテスト識別子を含めることです。

### イベント属性のエンリッチメント

既存のイベント属性に基づいて、イベントブール属性 `test_data` を構成できます。

![](https://docs.tealium.com/images/server-side/save-publish/test-data-event-boolean.png)

### 拡張

サーバーサイドにデータを渡す前にテストフラグを構成するために拡張を使用できます。

![](https://docs.tealium.com/images/server-side/save-publish/test-data-iq-extension.png)

この値を使用して、クエリ文字列を通じて構成した既存のデータまたはクッキー値を活用します。

### ウェブサイトのテストフラグ

**QA**サイトまたは**Dev**サイトのコード内でデータレイヤーの一部としてテストフラグを構成できます：

```html
<script>
utag_data.test_data = 'true';
</script>
```

### ファイルインポート

ファイルインポートでテストするには、`test_data` の列を追加し、テスト行には値 `true` を構成します。作成した `test_data` イベント属性に `test_data` 列をマッピングします。

ライブファイルインポートファイルの場合、ファイルから列を省略しても処理は行われ、テストデータとしてフラグが立てられることはありません。

### APIコール

APIを通じてイベントを送信する場合は、コールに `test_data=true` を追加し、追加のエンリッチメントは必要ありません。

```
curl -i "https://collect.tealiumiq.com/event?tealium_account=YOURACCOUNT&tealium_profile-YOURPROFILE&tealium_datasource-ABCDEF&tealium_event=user_login&customer_email=user@example.com&test_data=true"
```

Collect APIと`POST`メソッドを使用する場合は、JSONペイロードに`test_data`属性を含め、値を`true`に構成します：

```json
{
    "test_data" : true
}
```

### テストイベントフィード

テストイベントを識別するテスト属性を持っている場合、各イベントフィードの複製と`test_data`フラグを作成します：

![](https://docs.tealium.com/images/server-side/save-publish/test-data-event-feed.png)

![](https://docs.tealium.com/images/server-side/save-publish/test-data-event-feed-details.png)

### テストコネクタ

テストフィード用に別のコネクタを作成することをお勧めします。

![](https://docs.tealium.com/images/server-side/save-publish/test-data-separate-connectors.png)

また、テストコネクタのタイトルを次のように構成することをお勧めします：

* イベントタイプ：アクションのソースとして使用されるイベントフィード。
* バージョン：テストステータスを示すために`Test`または`Live`を使用します。

例：`Test Cart Add Events`


<blockquote>
この方法を使用する場合は、変更を行いたいときにすべてのコネクタアクションが更新されていることを確認してください。
</blockquote>


### コネクタとアクションの更新

コネクタとそのアクションを更新したい場合は、次の手順を使用します：

1. 変更を加えたいライブコネクタの複製を作成します。
1. タイトルを`Live`から`Test`に編集します。
1. コネクタアクションのそれぞれについて、ソースを`Test Data`イベントフィードに指すように更新します。
1. 保存して公開します。

ここから、この新しいテストコネクタで変更を行い、期待通りに動作するまでテストします。

### 更新の公開

テストが完了し、変更をデプロイする準備ができたら、テストコネクタをライブ環境に昇格させるために次の手順に従います：

1. ライブ環境にあるコネクタを削除します。
1. テストコネクタを更新します：
    * 名前を`Live version`に変更します。
    * テストフラグを削除します。
    * すべてのコネクタアクションソースを非テストイベントフィードを使用するように切り替えます。    
1. 保存して公開します。

### 使用ノート

各コネクタに追加情報を提供するために、**Notes**フィールドの使用を強くお勧めします。例えば：

* 変更を行う人。
* 変更の目的と理由。
* 追加または削除される内容。

## テスト訪問とオーディエンス

### テスト用のバッジを構成する

この例では、`Test User`というバッジ属性を使用します。このバッジは、クエリ文字列パラメータが`tealiumtest=true`を含む任意のイベントで評価されるルールを使用します。このバッジは、クエリ文字列パラメータが`tealiumtest=false`を含む場合にそれを訪問から割り当て解除するための第二のルールを使用します。

![](https://docs.tealium.com/images/server-side/save-publish/test-user-badge-rules.png)


<blockquote>
バッジとルール条件はカスタマイズ可能ですが、通常のサイト訪問にこのバッジが適用されないようにユニークであるべきです。
</blockquote>


### テスト用の属性を構成する

特定の属性をテストする場合、例えば文字列であれば、`Test User`バッジが割り当てられる特定のルールを含めます。

![](https://docs.tealium.com/images/server-side/save-publish/attribute-for-testing.png)

### テスト用のオーディエンスを構成する

特定のオーディエンスをテストしている場合、`Test User`バッジが割り当てられている条件を追加します。これにより、他のユーザーがそのオーディエンスに参加するのを防ぎ、その特定のオーディエンスに依存するコネクタアクションをテストできます。

![](https://docs.tealium.com/images/server-side/save-publish/audience-for-testing.png)

### テスト

トレースセッションを開始するときは、テスト構成で使用されるテスト条件を満たす必要があります。この例では、ルールで使用されるクエリ文字列パラメータと値を追加してサイトにアクセスします。

例：`http://www.example.com/?tealium_test=true`

トレースが開始されると、**Test User**バッジが割り当てられているのが確認できます。

![](https://docs.tealium.com/images/server-side/save-publish/test-badge-trace-example.png)

この方法でテストすることにより、ライブ環境に公開する前に構成を検証し、エラーを減らし、戦略の正確性を高めることができます。