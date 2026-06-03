---
title: マリーゴールドによるチーターデジタルコネクタ構成ガイド
description: この記事では、マリーゴールドによるチーターデジタルコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/cheetah-digital-by-marigold-connector/
---
## コネクタのアクション

| **アクション名** | **AudienceStream** | **EventStream** |
|:------|:-------------------|:----------------|
| サブスクライバーにメールを送信（高度なAPI呼び出し - ebmtrigger1） | ✓                  | ✗               |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIユーザー名**
  * マリーゴールドによるチーターデジタルAPIのユーザー名。
  * 詳細については、[マリーゴールドによるチーターデジタルAPI](https://help.cheetahces.com/hc/en-us/articles/360007860897-API-Category-Authentication-Service)を参照してください。

* **APIパスワード**
  * マリーゴールドによるチーターデジタルAPIのパスワード。
  * 詳細については、[マリーゴールドによるチーターデジタルAPI](https://help.cheetahces.com/hc/en-us/articles/360007860897-API-Category-Authentication-Service)を参照してください。

* **API URL**
  * プライベートIPネットワークをサポートします。例：`https://trig.{client-domain}.com/`。
  * 必要に応じてクライアントドメインを定義します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - サブスクライバーにメールを送信（高度なAPI呼び出し - ebmtrigger1）

#### パラメータ

| **パラメータ** | **説明** |
|:--------------|:----------------|
| `email`| &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;ターゲットのメールアドレス。&lt;/li&gt;&lt;/ul&gt;|
| `eid`| &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;ターゲットのメーリングテンプレートに関連付けられたイベントID。&lt;/li&gt;&lt;/ul&gt;|
| `aid`| &lt;ul&gt;&lt;li&gt;ターゲットメーリングのアフィリエイトID。&lt;/li&gt;&lt;/ul&gt;|
| `from_address`| &lt;ul&gt;&lt;li&gt;送信者/差出人のメールアドレス。&lt;/li&gt;&lt;/ul&gt;|
| `from_text`| &lt;ul&gt;&lt;li&gt;差出人ヘッダーのテキスト部分。&lt;/li&gt;&lt;/ul&gt;|
| `replyto`| &lt;ul&gt;&lt;li&gt;返信先ヘッダー。&lt;/li&gt;&lt;/ul&gt;|
| `b `| &lt;ul&gt;&lt;li&gt;エンゲージグローバル抑制ツール（GST）。&lt;/li&gt;&lt;/ul&gt; |
| `certify`| &lt;ul&gt;&lt;li&gt;第三者の認証スタンプを付けて送信。&lt;/li&gt;&lt;/ul&gt; |
| `mtype`| &lt;ul&gt;&lt;li&gt;認証済みメッセージタイプ。&lt;/li&gt;&lt;/ul&gt; |
| `test `| &lt;ul&gt;&lt;li&gt;デプロイされていないイベントをトリガーするテストフラグ。&lt;/li&gt;&lt;/ul&gt; |
| `part`| &lt;ul&gt;&lt;li&gt;テストに使用するメーリング部分。&lt;/li&gt;&lt;/ul&gt; |
| 優先コンテンツタイプ                                                              | &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;`HTML=Optional` - PARAM値の特殊なインスタンスで、優先コンテンツタイプを示します：&lt;ul&gt;&lt;li&gt;– テキストのみ&lt;/li&gt;&lt;li&gt;`1` – HTML/テキストのマルチパート&lt;/li&gt;&lt;li&gt;`2` – リッチテキスト/テキストのマルチパート&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
| 構成するメールCBデータフィールド                                                         | &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;フィールドごとに1行のアイテムを追加します（提供される行アイテムはパイプで区切られています）。&lt;/li&gt;&lt;li&gt;`cb=Optional` - グローバル抑制ツール（GST）の変更対象となるクライアント定義の抑制ビットインデックスのリストで、1から25までの範囲です。&lt;/li&gt;&lt;li&gt;`cb`パラメータが渡された場合、`b`パラメータも0または1の値で指定する必要があります。&lt;/li&gt;&lt;li&gt;アドレスの抑制を評価する際に、標準的なストップリストを含めるかどうかを示します。&lt;/li&gt;&lt;/ul&gt; |
| 構成するメールREQデータフィールド                                                        | &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;フィールドごとに1行のアイテムを追加します（提供される行アイテムはパイプで区切られています）。&lt;/li&gt;&lt;li&gt;`req=Optional` - 成功のために空でない必要があるパーソナライゼーションフィールドを指定します。&lt;/li&gt;&lt;li&gt;ループするダイナミックコンテンツフィールドは、適切な値（`ITEMS.*`）で`*`を置き換えて明示的に必要とすることができます。&lt;/li&gt;&lt;li&gt;また、`req`を`1`の値に構成すると、存在するすべてのパーソナライゼーションフィールドが空でないことが指定されます。&lt;/li&gt;&lt;/ul&gt; |
| ダイナミックコンテンツタグ/パラメータの構成                                                 | &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;フィールドごとに1行のアイテムを追加します（提供される行アイテムはパイプで区切られています）。&lt;/li&gt;&lt;li&gt;`PARAM=` - 任意の大文字のパラメータの値は、パラメータ名と2つのパーセンテージ記号で構成されるタグの代わりにメールに代入されるためのものです。&lt;ul&gt;&lt;li&gt;例：PARAMの場合、タグは&#34;`%%PARAM%%`&#34;になります。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;大文字のパラメータは`A` - `Z`または`_`で始まり、その後に任意の数の文字`A`- `Z`、- `9`、またはアンダースコア（ `_`）が続きます。&lt;/li&gt;&lt;li&gt;値は代入前にURLデコードされます。&lt;/li&gt;&lt;li&gt;API呼び出しで提供されないパラメータを参照するタグは空の文字列に置き換えられます。&lt;/li&gt;&lt;li&gt;値のサイズ制限はありません（全体の注文テーブルを提供することができます）。&lt;/li&gt;&lt;li&gt;テキスト、html、リッチテキスト/aolの3種類のメールクリエイティブのパラメータにはバージョニングがありません。&lt;/li&gt;&lt;li&gt;変数コンテンツがクリエイティブによって異なる形式でフォーマットされる必要がある場合、API呼び出しは異なるパラメータ名で異なるバージョンを提供する必要があります。&lt;/li&gt;&lt;li&gt;メーリングは、バージョンに適したタグを使用するように構成する必要があります。&lt;/li&gt;&lt;li&gt;パラメータ`T`、`TRACK`、および`EMAIL`は内部使用のために予約されています。&lt;/li&gt;&lt;li&gt;APIはPARAM名に対してエラートレラントです。&lt;/li&gt;&lt;li&gt;テンプレートに存在しないPARAMが提供された場合、それは静かに無視されます。&lt;/li&gt;&lt;li&gt;すべての名前を校正して、スペルミスにより失われないように確認してください。&lt;/li&gt;&lt;/ul&gt; |
| `getuser1` API呼び出しを介したサブスクライバールックアップの有効化 | &lt;ul&gt;&lt;li&gt;このオプションを有効にすると、ターゲットのサブスクライバーが`getuser1` API呼び出しを使用して検索される追加のAPI呼び出しがトリガーされます。&lt;/li&gt;&lt;li&gt;結果は次のセクションで構成されたサブスクライバーリストIDと照合され、一致した場合には`ebmtrigger1` API呼び出しを介してメールが送信されます。&lt;/li&gt;&lt;/ul&gt; このAPI呼び出しから返されるAIDは、&#34;Email General Data Fields to Set&#34;セクションの構成を上書きして使用されます。ただし、&#34;Subscriber Lookupから返されるAIDの使用を除外&#34;がチェックされている場合は除きます。 |
| &#34;Subscriber Lookup&#34;から返されるAIDの使用を除外 | &lt;ul&gt;&lt;li&gt;このオプションは、&#34;Subscriber Lookup&#34;も有効にされている場合にのみ使用されます。&lt;/li&gt;&lt;li&gt;チェックされている場合、&#34;Subscriber Lookup&#34; API呼び出しで返されたAIDは、次の`ebmtrigger1` API呼び出しには含まれません。それ以外の場合、&#34;Subscriber Lookup&#34;からのAIDが含まれ、&#34;Email General Data Fields to Set&#34;セクションの構成を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| サブスクライバールックアップ（`getuser1` API呼び出し）と照合するターゲットサブスクライバーリストID | &lt;ul&gt;&lt;li&gt;このオプションは、&#34;Subscriber Lookup&#34;も有効にされている場合にのみ使用されます。&lt;/li&gt;&lt;li&gt;email&lt;/li&gt;&lt;li&gt;このテーブルの&#34;Email General Data Fields to Set&#34;行を参照してください。&lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;&#34;Email General Data Fields to Set&#34;セクションで提供されたメールアドレスがサブスクライバーの検索に使用されます。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;ターゲットサブスクライバーリストID  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;`getuser1` API呼び出しの応答と照合するために使用されるサブスクライバーリストID。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |

