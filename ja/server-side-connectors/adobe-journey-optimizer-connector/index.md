---
title: Adobe Journey Optimizer コネクタ構成ガイド
description: この記事では、Adobe Journey Optimizer コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-journey-optimizer-connector/
---
## API 情報

このコネクタは以下のベンダー API を使用します：

* API 名：Adobe Journey Optimizer API
* API エンドポイント：`https://platform.adobe.io`
* ドキュメント：[Adobe Journey Optimizer APIs](https://developer.adobe.com/journey-optimizer-apis/)

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| 単一メッセージ実行（リアルタイム） | ✓ | ✓ |
| 単一メッセージ実行（バッチ処理） | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[About Connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **クライアント ID**  
（必須）クライアント ID（API キー）は、Adobe アカウントの [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) で見つけることができます。
* **クライアント シークレット**  
（必須）クライアント シークレットは、Adobe Developer Console で見つけることができます。
* **組織 ID**  
（必須）組織 ID は、Adobe Developer Console で見つけることができます。
* **サンドボックス**  
API 呼び出しがデフォルトの環境（prod）とは異なる環境を参照するかどうかを指定します。

## アクション

次のセクションでは、各アクションに対応するサポートされるパラメータをリストします。

### 単一メッセージ実行（バッチ処理）

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかのしきい値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：20
* 最古のリクエストからの最大時間：5分
* リクエストの最大サイズ：1 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| キャンペーン ID | （必須）キャンペーン識別子。 |
| リクエスト ID | ユニークなリクエスト識別子。 |
| 名前空間 | AEP プロファイルの名前空間。 |

#### 受信者パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| タイプ | （必須）受信者タイプ。例えば、`aep`。 |
| ユーザー ID | （必須）AEP プロファイル識別子。 |
| コンテキスト | メッセージ内容の動的変数置換に使用されるコンテキストデータ。 |
| メールアドレス | 受信者のメールアドレスであり、外部ユーザー ID でもあります。 |
| 携帯電話番号 | SMS テキストメッセージ用の受信者の携帯電話番号。 |
| プロファイル | メッセージ内容の動的変数置換に使用されるプロファイルデータ。 |
| テンプレート変数 | **テンプレート**用のデータ入力としてテンプレート変数を提供します。詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`。<br>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。|
| テンプレート | 本文パラメータで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>サポートされるフィールドに名前でテンプレートが注入されます。例：`{{SomeTemplateName}}`。|

### 単一メッセージ実行（リアルタイム）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| キャンペーン ID | （必須）キャンペーン識別子。 |
| リクエスト ID | ユニークなリクエスト識別子。 |
| 名前空間 | AEP プロファイルの名前空間。 |

#### 受信者パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| タイプ | （必須）受信者タイプ。例えば、`aep`。 |
| ユーザー ID | （必須）AEP プロファイル識別子。 |
| コンテキスト | メッセージ内容の動的変数置換に使用されるコンテキストデータ。 |
| メールアドレス | 受信者のメールアドレスであり、外部ユーザー ID でもあります。 |
| 携帯電話番号 | SMS テキストメッセージ用の受信者の携帯電話番号。 |
| プロファイル | メッセージ内容の動的変数置換に使用されるプロファイルデータ。 |
| テンプレート変数 | **テンプレート**用のデータ入力としてテンプレート変数を提供します。詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`。<br>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。|
| テンプレート | 本文パラメータで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>サポートされるフィールドに名前でテンプレートが注入されます。例：`{{SomeTemplateName}}`。|