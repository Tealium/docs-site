---
title: テストについて
description: この記事では、Tealiumプラットフォームのサーバーサイドにおける公開プロセスについて説明します。
url: https://docs.tealium.com/ja/server-side/save-publish/test/
---
サーバーサイド構成には**Dev**環境や**QA**環境がないため、変更を本番環境にリリースする前にテストするには、追加の手順が必要です。テストフラグ、バッジ、ルールを活用すると、複数の方法で構成できるテストユーザーのみに新機能を簡単に制限できます。

## テストイベント

本番イベントとテストイベントを分離する方法はいくつかあります。目的は、関連するすべてのテストデータイベントに、このテスト識別子を含めることです。

### イベント属性のエンリッチメント

既存のイベント属性に基づくエンリッチメントを使用して、イベントのブール属性`test_data`を構成できます。

![](https://docs.tealium.com/images/server-side/save-publish/test-data-event-boolean.png)

### 拡張機能

データがサーバーサイドに渡される前に、拡張機能を使用してテストフラグを構成できます。

![](https://docs.tealium.com/images/server-side/save-publish/test-data-iq-extension.png)

この値を使用して、既存のデータやクエリ文字列を通じて構成したCookie値を活用します。

### Webサイトのテストフラグ

データレイヤーの一部として、**QA**サイトまたは**Dev**サイトのコード内にテストフラグを構成できます。

```html
<script>
utag_data.test_data = 'true';
</script>
```

### ファイルインポート

ファイルインポートでテストするには、`test_data`列を追加し、テスト行の値を`true`に構成します。`test_data`列を、作成した`test_data`イベント属性にマッピングします。

本番用のファイルインポートでは、ファイルからこの列を省略しても処理は実行され、テストデータとしてフラグ付けされることはありません。

### API呼び出し

APIを介してイベントを送信する場合は、呼び出しに`test_data=true`を追加します。追加のエンリッチメントは必要ありません。

```
curl -i "https://collect.tealiumiq.com/event?tealium_account=YOURACCOUNT&tealium_profile-YOURPROFILE&tealium_datasource-ABCDEF&tealium_event=user_login&customer_email=user@example.com&test_data=true"
```

Collect APIと`POST`メソッドを使用する場合は、JSONペイロードに値が`true`の`test_data`属性を含めます。

```json
{
    "test_data" : true
}
```

### テストイベントフィード

テストイベントを識別するテスト属性を用意したら、各イベントフィードを複製し、`test_data`フラグを追加します。

![](https://docs.tealium.com/images/server-side/save-publish/test-data-event-feed.png)

![](https://docs.tealium.com/images/server-side/save-publish/test-data-event-feed-details.png)

### テストコネクタ

テストフィード用に個別のコネクタを作成することをお勧めします。

![](https://docs.tealium.com/images/server-side/save-publish/test-data-separate-connectors.png)

また、テストコネクタのタイトルには、次の情報を構成することをお勧めします。

* イベントタイプ：アクションのソースとして使用するイベントフィード。
* バージョン：テストステータスを示すために`Test`または`Live`を使用します。

例：`Test Cart Add Events`


<blockquote>
If you use this method, ensure that all connector actions are updated when you are looking to do make changes.
</blockquote>


### コネクタとアクションの更新

コネクタとそのアクションを更新する場合は、次の手順を実行します。

1. 変更する本番コネクタを複製します。
1. タイトルを`Live`から`Test`に変更します。
1. 各コネクタアクションについて、ソースを対応する`Test Data`イベントフィードに変更します。
1. 保存して公開します。

以降は、期待どおりに動作するまで、この新しいテストコネクタに変更を加えます。

### 更新の公開

テストが完了し、変更をデプロイする準備ができたら、次の手順に従ってテストコネクタを本番環境に昇格させます。

1. 本番環境にあるコネクタを削除します。
1. テストコネクタを更新します。
    * 名前を`Liveバージョンに変更します。
    * テストフラグを削除します。
    * すべてのコネクタアクションのソースを、テスト用ではないイベントフィードに切り替えます。
1. 保存して公開します。

### メモの使用

各コネクタの**Notes**フィールドを使用して、次のような追加情報を記載することを強くお勧めします。

* 変更を行っている担当者。
* 変更の目的と理由。
* 追加または削除する内容。

## テスト訪問とオーディエンス

### テスト用バッジの構成

この例では、`Test User`というバッジ属性を使用します。このバッジでは、クエリ文字列パラメータに`tealiumtest=true`が含まれている場合に、任意のイベントで評価されるルールを使用します。また、クエリ文字列パラメータに`tealiumtest=false`が含まれている場合に、訪問からバッジの割り当てを解除する2つ目のルールも使用します。

![](https://docs.tealium.com/images/server-side/save-publish/test-user-badge-rules.png)


<blockquote>
The badge and rule condition can be customized, but they should be unique so that regular site visitors do not get this badge applied to them.
</blockquote>


### テスト用属性の構成

文字列などの特定の属性をテストするには、`Test User`バッジが割り当てられていることを条件とする特定のルールを含めます。

![](https://docs.tealium.com/images/server-side/save-publish/attribute-for-testing.png)

### テスト用オーディエンスの構成

特定のオーディエンスをテストする場合は、`Test User`バッジが割り当てられていることを必須条件として追加します。これにより、ほかのすべてのユーザーがそのオーディエンスに参加することを防ぎ、その特定のオーディエンスに依存するコネクタアクションをテストできます。

![](https://docs.tealium.com/images/server-side/save-publish/audience-for-testing.png)

### テスト

トレースセッションを開始するときは、テスト構成で使用されているテスト条件を満たす必要があります。この例では、サイトに移動し、ルールで使用されているクエリ文字列パラメータと値をURLに追加します。

例：`http://www.example.com/?tealium_test=true`

トレースが開始されると、**Test User**バッジが割り当てられたことを確認できます。

![](https://docs.tealium.com/images/server-side/save-publish/test-badge-trace-example.png)

本番環境に公開する前にこの方法でテストすると、構成を検証し、エラーを減らして、施策の精度を高めることができます。