---
title: Tealiumイベント拡張
description: Tealiumイベント拡張は、最も一般的に追跡されるイベントのための標準的な条件を定義します。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/tealium-events-extension/
---
この拡張機能は、`tealium_event`変数をデータレイヤーに追加し、タグマッピング、ロードルール、または他の条件の簡素化に役立ちます。また、Tealium Collectタグを介してTealium EvenStreamに渡すこともできます。

## 前提条件

* utag v4.38以降

## 仕組み

この拡張機能は、標準化されたイベント名をあなたのソリューションに導入し、データレイヤーに新しい変数`tealium_event`を追加します。これは標準のeコマースの顧客旅行をカバーし、**カートに追加**、**商品詳細ページの表示**、**購入完了**などの馴染み深いイベントを含みます。これらのイベントは通常、`page_type`と`event_name`を使用してデータレイヤーで表現されるため、この拡張機能は現在のページ/イベント追跡条件と新しい標準化されたTealiumイベント名との間の翻訳として機能します。

各イベントは、データレイヤーの実装に一致するカスタム条件に割り当てることができます。イベント条件が真と評価されると、`tealium_event`は事前に定義されたイベント値に構成されます。例えば、**カートに追加**の条件が`true`と評価されると、`tealium_event`は`cart_add`に構成されます。下記の標準イベントセクションを参照してください。

## 拡張機能の使用

始める前に、[拡張機能の動作方法]()について理解しておいてください。

拡張機能が追加されると、実装のニーズに応じてイベント条件をカスタマイズできます。イベントのリストは変更できませんが、イベント条件は変更できます。イベント条件をカスタマイズするには：

1. イベントをクリックし、**編集**をクリックします。
1. 必要に応じて条件ロジックを調整します。
1. **適用**をクリックします。

### 条件の削除

イベントが構成されないようにするには、条件を削除し、**適用**をクリックします。これにより、イベントは`構成`から`未構成`に変更され、構成では評価されなくなります。

この例では、メール登録イベントの条件が削除され、イベントが`未構成`になっています。

![](/images/iq-tag-management/remove-event-conditon.png)

![](/images/iq-tag-management/after-removing-condition.png)

## 標準イベント

以下は、拡張機能内の標準イベントとデフォルト条件の表です。イベントはアルファベット順にリストされ、順番に評価されます。デフォルト条件は[標準データレイヤーの推奨事項]()に一致しますが、あなたの具体的な実装に一致するようにカスタマイズ可能です。

|イベント| `tealium_event`| デフォルト条件|
|---| ---| ---|
|カートに追加| `cart_add`| `event_name=&#34;cart_add&#34;`|
|カテゴリーページ表示| `category_view`| `page_type=&#34;category&#34;`|
|チェックアウト| `checkout`| `page_type=&#34;checkout&#34;`|
|メール登録| `email_signup`| `event_name=&#34;email_signup&#34;`|
|カートを空にする| `cart_empty`| `event_name=&#34;cart_empty&#34;`|
|ページ表示| `page_view`| `page_type=&#34;generic&#34;`|
|商品詳細ページ表示| `product_view`| `page_type=&#34;product&#34;`|
|購入完了| `purchase`| `page_type=&#34;purchase&#34;`|
|カートから削除| `cart_remove`| `event_name=&#34;cart_remove&#34;`|
|検索ページ表示| `search`| `page_type=&#34;search&#34; `|
|ショッピングカート表示| `cart_view`| `page_type=&#34;cart&#34; `|
|ソーシャルシェア| `social_share`| `event_name=&#34;social_share&#34;`|
|ユーザーログイン| `user_login`| `event_name=&#34;user_login&#34;`|
|ユーザーログアウト| `user_logout`| `event_name=&#34;user_logout&#34;`|
|ユーザー登録| `user_register`| `event_name=&#34;user_register&#34;`|

`tealium_event`の値は、最後に`true`と評価された条件に常に構成されます。もし複数のイベント条件が`true`と評価された場合、リストの下のイベントが構成されます。

## カスタムイベント

Tealiumイベント拡張機能は、事前定義されたイベントのリストを提供します。カスタムイベントは、あなたが定義した値を使用し、変数`tealium_event`に割り当てます。これらのカスタムイベントを直接データレイヤーで定義するか、[Set Data Values拡張機能]()を使用して定義します。

拡張機能で定義されたカスタムイベントは、Tealiumイベント拡張機能の後に配置します。

拡張機能を使用してカスタムイベントを定義するには：

1. Set Data Values拡張機能を追加します。
1. 新しい拡張機能を既存のTealiumイベント拡張機能の下にドラッグして、それが後に実行されるようにします。
1. **Set**ドロップダウンリストで`tealium_event`を選択します。
1. テキストフィールドにカスタムイベントの名前を入力します。
1. カスタムイベントを識別する条件を追加します。

Set Data Values拡張機能を使用したカスタムイベントの例：

![](/images/iq-tag-management/tealium-event-extension-custom-event.png)

## 例

拡張機能の目的は、構成で使用される`tealium_event`変数にイベント名の値を標準化することです。以下は、この変数の使用例です：

#### タグ内のイベントマッピング

単一の変数、`tealium_event`を使用して、ページとイベントマッピングをサポートするタグ構成を簡素化します。

#### ロードルール

ロードルールは、その条件を簡素化するために`tealium_event`を使用します。

#### Customer Data Hub

[Tealium Collectタグ]()を持っている場合、データレイヤーのすべての変数がTealium EventStreamに渡され、`tealium_event`を含みます。この変数は、エンリッチメント、ルール、フィードで使用するための[インポートされたイベント属性]()として利用可能になります。

