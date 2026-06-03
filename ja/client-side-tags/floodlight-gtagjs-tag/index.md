---
title: Floodlight (gtag.js) タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Floodlight を構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/floodlight-gtagjs-tag/
---
## タグのヒント

* 変換 API を開始する前にアクティブにしてください。詳細については、[Google: 新しい Floodlight 変換アクションの Google タグを作成する](https://support.google.com/ds/answer/7562806)を参照してください。
* Eコマース拡張機能をサポートしています:
  * 注文 ID (`_corder`)
  * 注文合計 (`_ctotal`)
  * 製品 ID のリスト (`_cprod`)
  * 数量のリスト (`_cquan`)
  * 価格のリスト (`_cprice`)
* マッピングを使用して:
  * イベントトリガーを構成する
  * 標準構成値を動的に上書きする
  * Eコマース拡張値を動的に上書きする
* カスタムイベントパラメータを &#34;DoubleClick Custom Parameters&#34; にマッピングして、`myvar` をカスタム変数名に置き換えて渡します。
* リストを使用する際にセッション ID が不要な場合は、SessionID を空白または空の文字列に構成します。
* 追加情報については、[Google: Floodlight ドキュメント](https://support.google.com/dcm/partner/answer/7568534)を参照してください。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法については、[タグ概要]()の記事を読んでください。

タグを追加する際には、以下の構成を構成します:

* **広告主 ID**
  * 単一またはカンマ区切りの広告主識別子のリストで、Floodlight アクティビティのソースです。例: `DC-123456789`。
* **グループタグ文字列**
  * 単一またはカンマ区切りのグループタグ文字列のリスト。
  * 広告主 ID の数と一致する必要があります。
* **アクティビティタグ文字列**
  * 単一またはカンマ区切りのアクティビティタグ文字列のリスト。
  * 広告主 ID の数と一致する必要があります。
* **カウント方法**
  * 単一またはカンマ区切りのカウント方法のリスト。
  * 広告主 ID の数と一致する必要があります。
* **自動購入イベント発火**
  * 注文 ID が存在する場合に購入イベントを発火します。
  * カウント方法が構成されていない場合、トランザクションに構成されます。
* **カスタムスクリプトを許可**
  * ウェブサイトのアクティビティを追跡するためにサードパーティツールを統合するダイナミックタグを有効にします。
* **グローバルオブジェクト**
  * この値はイベントキューに使用されるグローバルオブジェクトの名前です。
  * 指定されていない場合、`gtag`が使用されます。
  * ほとんどの実装では必要ありません。
* **データレイヤー名**
  * デフォルトでは、グローバルサイトタグによって初期化および参照されるデータレイヤーは `dataLayer` という名前です。
  * プロジェクトが別の名前を必要とする場合のみ、データレイヤーの名前を変更します。
* **クロストラッキングドメイン**
  * クロスドメイントラッキング (`setAllowLinker`) に使用するドメインのカンマ区切りリスト。
  * この値はトップレベルドメインである必要があります。例: `tealiumiq.com`。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング]()を参照してください。

利用可能なカテゴリは以下の通りです:

### 標準

|構成| 説明|
|---| ---|
| 広告主 ID `advertiser_id` |  &lt;ul&gt;&lt;li&gt;(必須) 文字列/配列&lt;/li&gt;&lt;li&gt;カンマで区切られた1つ以上の広告主 ID。&lt;/li&gt;&lt;li&gt;例: `DC-12345678`&lt;/li&gt;&lt;li&gt;すべての ID にデータが送信されます。&lt;/li&gt;&lt;li&gt;大文字と小文字を区別します&lt;/li&gt;&lt;/ul&gt; |
| グループタグ文字列 `activity_group` |  &lt;ul&gt;&lt;li&gt;(必須) 文字列/配列&lt;/li&gt;&lt;li&gt;カンマで区切られた1つ以上のグループタグ文字列。&lt;/li&gt;&lt;li&gt;広告主 ID の長さと一致する必要があります。&lt;/li&gt;&lt;li&gt;大文字と小文字を区別します&lt;/li&gt;&lt;/ul&gt; |
| アクティビティタグ文字列 `activity` |  &lt;ul&gt;&lt;li&gt;(必須) 文字列/配列&lt;/li&gt;&lt;li&gt;カンマで区切られた1つ以上のアクティビティタグ文字列。&lt;/li&gt;&lt;li&gt;広告主 ID の長さと一致する必要があります。&lt;/li&gt;&lt;li&gt;大文字と小文字を区別します&lt;/li&gt;&lt;/ul&gt; |
| カウント方法 `counting_method` |  &lt;ul&gt;&lt;li&gt;(必須) 文字列/配列&lt;/li&gt;&lt;li&gt;カンマで区切られた1つ以上のカウント方法名。&lt;/li&gt;&lt;li&gt;広告主 ID の長さと一致する必要があります。&lt;/li&gt;&lt;li&gt;小文字に変換されます。&lt;/li&gt;&lt;/ul&gt; |
| セッション ID `session_id` |  &lt;ul&gt;&lt;li&gt;文字列/配列&lt;/li&gt;&lt;li&gt;広告主 ID の長さに一致する値のないもの、1つ、または一連の値をマップします。&lt;/li&gt;&lt;li&gt;必要ない場所には空白を入れます。&lt;/li&gt;&lt;/ul&gt; |
| イベント名 `event_name` |  &lt;ul&gt;&lt;li&gt;現在のイベントの名前。&lt;/li&gt;&lt;/ul&gt; |
| 自動購入イベント発火 `fire_purchase` |  &lt;ul&gt;&lt;li&gt;値は `True` または `False`。&lt;/li&gt;&lt;li&gt;注文 ID が存在する場合に購入イベントを発火します。&lt;/li&gt;&lt;li&gt;カウント方法が構成されていない場合、トランザクションに構成されます。&lt;/li&gt;&lt;/ul&gt; |
| カスタムスクリプトを許可 `custom_scripts` |  &lt;ul&gt;&lt;li&gt;値は `True` または `False`。&lt;/li&gt;&lt;li&gt;デフォルト値は `True` です。&lt;/li&gt;&lt;li&gt;ウェブサイトのアクティビティを追跡するためにサードパーティツールを統合するダイナミックタグを有効にします。&lt;/li&gt;&lt;li&gt;構成値を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| クロストラッキングドメイン `cross_track_domains` | &lt;ul&gt;&lt;li&gt;クロスドメイントラッキングに使用するドメインのカンマ区切りリスト。&lt;/li&gt;&lt;/ul&gt; |
| マッチ ID `dc_custom_params.match_id` | &lt;ul&gt;&lt;li&gt;広告主が作成した一意の識別子（Floodlight 経由で渡される）で、Google と同期してオフライン変換を帰属させることができます。&lt;/li&gt;&lt;li&gt;この値は大文字と小文字を区別し、100文字に制限され、文字 (`a-z` または `A-Z`)、数字 (`0-9`)、アンダースコア (`_`)、ハイフン (`-`)、ピリオド (`.`) のみを含みます。&lt;/li&gt;&lt;/ul&gt; |
| 順序 `dc_custom_params.ord` | &lt;ul&gt;&lt;li&gt;キャッシュバスターとして機能する一意のランダム数値で、ブラウザが広告画像やクリックスルー URL をキャッシュから読み込むのを防ぎます。&lt;/li&gt;&lt;li&gt;Floodlight タグと連携して [SA360 Enhanced Conversion コネクタ]() を使用する場合、購入以外の変換に `tealium_random` をマップすることをお勧めします。&lt;/li&gt;&lt;/ul&gt;  |

### イベント

特定のイベントをページ上でトリガーするためにこれらの宛先にマップします。

イベントをトリガーするための手順は以下の通りです:

1. `tealium_event` 変数を選択します。
1. **&#43; Add Mapping** をクリックします。
1. 左サイドバーで **Event** をクリックします。
1. **Trigger** フィールドにマッピングされる変数の値を入力します。
1. ドロップダウンリストから **Conversion** または **Purchase** を選択します。
1. **&#43; Add** をクリックします。
    * 追加の変数をマップするには、手順 4、5、6 を繰り返します。
1. **Done** をクリックします。

データレイヤーに指定された値が見つかるとイベントがトリガーされます。

|**宛先名**| **説明**|
|---| ---|
| 変換 `conversion` |  &lt;ul&gt;&lt;li&gt;変換タイプのイベントを送信するためにマップします。&lt;/li&gt;&lt;li&gt;変換イベントはデフォルトでは送信されません。&lt;/li&gt;&lt;li&gt;このイベントには `standard`, `unique` または `per_session` のカウント方法を使用します。&lt;/li&gt;&lt;/ul&gt; |
| 購入 `purchase` |  &lt;ul&gt;&lt;li&gt;購入タイプのイベントを送信するためにマップします。&lt;/li&gt;&lt;li&gt;注文 ID が存在する場合、購入イベントは自動的に送信されます。&lt;/li&gt;&lt;li&gt;このイベントには `transactions` または `items_sold` のカウント方法を使用します。&lt;/li&gt;&lt;/ul&gt; |

### Eコマース

Floodlight (`gtag.js`) タグは Eコマース対応であり、デフォルトの Eコマース拡張マッピングを自動的に使用します。拡張マッピングを上書きするか、拡張機能で提供されていない Eコマース変数を使用したい場合を除き、このカテゴリでの手動マッピングは通常必要ありません。

|**宛先名**| **説明**|
|---| ---|
| 注文 ID `order_id` |  &lt;ul&gt;&lt;li&gt;`_corder` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| 注文合計 `order_total` |  &lt;ul&gt;&lt;li&gt;`_ctotal` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| ID のリスト `product_id` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;`_cprod` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| 数量のリスト `product_quantity` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;`_cquan` を上書きします。&lt;/li&gt;&lt;li&gt;単一の数値の上書きまたは値の配列を受け入れます。&lt;/li&gt;&lt;/ul&gt; |
| 価格のリスト `product_unit_price` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;`_cprice` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
### カスタム

|**宛先名**| **説明**|
|---| ---|
| DoubleClick カスタムパラメータ `dc_custom_params.myvar` |  &lt;ul&gt;&lt;li&gt;`dc_custom_params` オブジェクトの一部としてカスタムパラメータを送信するために使用します。&lt;/li&gt;&lt;li&gt;`myvar` をパラメータの名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 1 `custom.u1` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u1` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 2 `custom.u2` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u2` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 3 `custom.u3` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u3` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 4 `custom.u4` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u4` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 5 `custom.u5` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u5` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 6 `custom.u6` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u6` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 7 `custom.u7` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u7` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 8 `custom.u8` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u8` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 9 `custom.u9` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u9` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 10 `custom.u10` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u10` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 11 `custom.u11` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u11` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 12 `custom.u12` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u12` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 13 `custom.u13` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u13` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 14 `custom.u14` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u14` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 15 `custom.u15` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u15` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 16 `custom.u16` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u16` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 17 `custom.u17` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u17` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 18 `custom.u18` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u18` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 19 `custom.u19` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u19` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 20 `custom.u20` |  &lt;ul&gt;&lt;li&gt;カスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u20` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで提供されていない場合、デフォルトでディメンションまたはメトリック名になります。&lt;/li&gt;&lt;/ul&gt; |
| カスタム変数 21&#43; `custom.u#` |  &lt;ul&gt;&lt;li&gt;20を超えるカスタムメトリクスとディメンションを追加するためにこのカスタムパラメータを使用します（Floodlight Searchではサポートされていません）。&lt;/li&gt;&lt;li&gt;カスタム Floodlight 変数 `u#` と関連付けます。&lt;/li&gt;&lt;li&gt;マッピングで `#` 記号を希望する番号に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |

#### IAB 透明性と同意フレームワーク v2

|変数| 説明|
|---| ---|
| TCF サポートを有効にする `tag_enable_tcf_support` |  &lt;ul&gt;&lt;li&gt;値は `true` または `false` です。&lt;/li&gt;&lt;/ul&gt; |

### エンハンスドコンバージョン

| 変数  | タイプ | 説明 |
|:---------|:------------|:------------|
|  `user_data.email` | 文字列 |メールアドレス  |
|  `user_data.phone_number` | 文字列 |電話番号  |
|  `user_data.address.first_name` | 文字列 |名  |
|  `user_data.address.last_name` |文字列 |姓  |
| `user_data.address.street` | 文字列 |住所  | 
|  `user_data.address.city` |文字列 |市  |
|  `user_data.address.region` | 文字列 |地域  |
| `user_data.address.postal_code` | 文字列 |郵便番号  | 
|  `user_data.address.country` | 文字列 |国  |


## 追加文書

* [複数の Floodlight タグの構成](/ja/client-side-tags/configuring-multiple-floodlight-tags/)
* [Google: グローバルサイトタグの使用](https://support.google.com/dcm/partner/answer/7568534)

