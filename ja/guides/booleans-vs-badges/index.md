---
title: ブール値とバッジの比較
description: このガイドでは、訪問のブール属性とバッジ属性を包括的に比較します。
url: https://docs.tealium.com/ja/guides/booleans-vs-badges/
---
ブール値とバッジは、さまざまな種類の訪問データを取得して表現するために使用される重要な属性です。ただし、それぞれ目的が異なり、異なるシナリオで使用されます。

## 定義

![](https://docs.tealium.com/images/icons/icon-boolean-flag.png)

### ブール値

ブール値は、顧客固有の状態または現在のステータスを表す、単純なtrue/false属性です。訪問に関する1つの情報を表すアトミック属性として使用されます。明示的に更新されない限り、値は変更されません。

訪問ブール値の例は次のとおりです。

  * `is_verified`：訪問がメールアドレスを認証済みかどうか。
  * `has_valid_payment`：訪問のアカウントに有効な支払い方法が登録されているかどうか。
  * `is_internal_user`：訪問が社内ユーザーかどうか。

![](https://docs.tealium.com/images/icons/icon-badge.png)

### バッジ

バッジは、より複雑な行動パターンを表す訪問専用の属性です。顧客が重要なアクションを実行したり、特定のマイルストーンに到達したりしたときに、付与または削除されます。バッジは、条件や行動の組み合わせを表す複合属性に使用され、指定された条件が満たされた場合にのみ付与されます。

バッジはUIで特別に扱われ、AudienceStreamの**Dashboard**にある**Badge Activity**ウィンドウ、**Visitor Profile**サンプラー、および**Audience Discovery**にカスタムアイコンとともに表示されます。

バッジの例は次のとおりです。

  * `VIP`：VIPは、サイトを繰り返し訪問して商品を購入する、価値の高い顧客です。
  * `Cart Abandoner`：カート放棄者とは、商品をショッピングカートに追加したものの、購入を完了しなかった訪問です。
  * `Frequent Business Traveler`：頻繁に出張するビジネス旅行者とは、一定期間内に所定の回数を超えて出張した顧客です。

その他の例については、[popular-badges](https://docs.tealium.com/popular-badges/)を参照してください。

## エンリッチメントとロジック

ブール値とバッジでは、値を構成するために使用するエンリッチメントが次のように異なります。

### ブール値のエンリッチメント

* **Set Boolean**：このエンリッチメントは、ブール属性を`true`または`false`に構成します。たとえば、訪問がメールアドレスを認証したかどうかを追跡するには、最初に属性を`false`に構成し、`user_login`イベントが発生するたびに`true`に構成します。

ブール値をクリアするエンリッチメントはありません。通常、訪問ブール値はほとんど変更されない永続的な値です。

### バッジのエンリッチメント

* **Assign Badge**：このエンリッチメントは、一連の条件が満たされたときに訪問へバッジを付与します。たとえば、購入せずにサイトを頻繁に閲覧する訪問には、`Window Shopper`バッジが付与されます。
* **Remove Badge**：このエンリッチメントは、訪問が条件を満たさなくなったときにバッジを削除します。たとえば、訪問が購入すると、`Window Shopper`バッジが削除されます。
* **Assign Badge from Another Badge**：このエンリッチメントは、別のバッジが付与されていることを基にバッジを付与します。たとえば、`Sports car fan`バッジの獲得をトリガーとして、`Car fan`などの関連バッジを付与できます。詳細については、を参照してください。

## データ表現

訪問ブール値とバッジは、プラットフォーム上で次のように表現されます。

### ブール値

ブール値は、訪問データレコードの`flags`データオブジェクトに、キーと値のペアとして保存されます。キーには、ブール属性のUIDまたは名前が使用されます。

```json
{
    ...
    "flags": {
        "5052": false
    },
    ...
}
```

AudienceDBでは、列見出しはファイルタイプ（テーブル、ビュー、または正規化形式）によって異なります。

* Visitor Table：`flag_5052`
* Visitor View：`visitor - flag - is_verified (5052)`
* Visitor Normalized：`visitor - flag - is_verified`

列の値は`t`または`f`です。

### バッジ

バッジは訪問スコープでのみ使用できます。

バッジは、バッジUIDの配列またはバッジ名の配列として訪問データレコードに保存されます。

```json
{
    ...
    "badges": ["13","26","52"],
    ...
}
```

AudienceDBでは、列見出しはデータベーステーブルのタイプ（テーブル、ビュー、または正規化形式）によって異なります。

* Table：`badge_13`
* View：`visitor - badge - VIP (13)`
* Normalized：`visitor - badge - VIP`

列の値は、バッジの有無に応じて`t`または`f`になります。

AudienceStreamの**Dashboard**にある**Badge Activity**ウィンドウには、訪問プロファイルに付与された、または訪問プロファイルから削除されたすべてのバッジが表示されます。

![](https://docs.tealium.com/images/server-side/badge-activity-view.png)

また、**Visitor Profile**サンプラーでは、各バッジについて、アクティビティの監視を開始してからそのバッジを獲得した訪問の数と割合が表示されます。

![](https://docs.tealium.com/images/server-side/visitor-profile-sampler-badges-view.jpg)

## 文字列をブール値として使用する

ほとんどのシナリオでは、状態の追跡にブール値またはバッジを使用すれば十分です。ただし、**まれなケース**では、`true`と`false`に加えて、**未割り当て**状態を表す必要がある場合があります。文字列を使用すると、2つではなく3つの異なる状態を追跡できます。  

たとえば、ユーザーの同意を保存する場合は次のようになります。

* `true`：ユーザーが同意している。  
* `false`：ユーザーが同意を拒否している。  
* **未割り当て**：ユーザーがまだ回答していない。  

この方法は、**回答なし**と明示的な`false`を区別する必要がある場合に役立ちます。

## 比較の概要

次の表に、ブール値とバッジの主な違いを示します。

| 機能 | 訪問ブール値 | バッジ |
| --- | --- | ---- |
| 定義 | true/falseの状態または現在のステータス。 | 複雑な行動を表します。 |
| 用途 | 単一の条件。 | 複雑な行動やマイルストーン。 |
| 保存形式 | キーと値のペア（true/false） | バッジ名またはバッジUIDの配列。 |
| 変更方法 | 明示的に更新。 | 条件に基づいて追加または削除。 |
| エンリッチメント | Set Boolean。 | Assign、Remove、およびAssign from Another Badge。 |

## 関連項目

* [badge-attribute](https://docs.tealium.com/badge-attribute/)
* [boolean-attribute](https://docs.tealium.com/boolean-attribute/)
* [vip-badge-guide](https://docs.tealium.com/vip-badge-guide/)