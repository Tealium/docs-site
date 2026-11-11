---
title: Zanoxタグ構成ガイド
description: この記事では、タグ管理アカウントでZanoxを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/zanox-tag/
---## 要件

* Zanoxアカウント


## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **タイトル**：（必須）タグインスタンスを識別するための分かりやすいタイトルを入力します。
* **タグタイプ**：（必須）ドロップダウンリストから、読み込むタグのタイプを選択します。
  * Master Tag：Zanoxが広告主に提供するMasterTagコードを読み込みます。
  * PPS：Pay-per-Sale（売上報酬型）の略称です。PPSトラッキングピクセルを読み込みます。
  * PPL：Pay-per-Lead（リード報酬型）の略称です。PPLトラッキングピクセルを読み込みます。
* **PPS/PPL ID**：PPS/PPLタグタイプを選択した場合は、このフィールドにタグ識別子を入力します。このIDは、Zanoxが提供するトラッキングピクセルの末尾にあります。MasterTagタイプを選択した場合、このフィールドは空白のままにします。例：このURL（//ad.zanox.com/ppl/?2173D3211067525）の末尾にある英数字の値がPPL IDです。
* **デフォルトのzx\_class**：（任意）MasterTagタイプを選択した場合は、このフィールドにclass属性の値（接頭辞「zx」を除く）を入力します。このフィールドに動的に値を構成する場合は、マッピングツールボックスでdivコンテナのclass IDにマッピングする必要があります（[マッピングの構成](#mappings)を参照）。例：48EFE82D8GE72DE1BBE2


<blockquote>
Zanoxでは、1つのページに読み込むMasterTagインスタンスを1つだけにすることを推奨しています。すべてのパラメータが正しくレンダリングされない限り、iFrameを使用してMasterTagを読み込まないでください。
</blockquote>


## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

**ベストプラクティス**：

* MasterTagの場合は、デフォルトの「すべてのページで読み込む」ルールを選択します。
* PPSタグタイプの場合は、サンクスページや領収書ページなどの注文確認ページでタグを読み込むように、読み込みルールを構成します。
* PPLタグタイプの場合は、登録ページでタグを読み込むように、読み込みルールの条件を構成します。

## データマッピング

[マッピング](https://docs.tealium.com/about-data-mappings/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数へデータを送信する簡単なプロセスです。このタグの宛先変数は、マッピングツールボックスで使用できます。使いやすいように、変数は「Standard」と「MasterTag」の各カテゴリーに分類されています。


<blockquote>
このタグを使用するには、事前に[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を構成する必要があります。適切な注文変数と商品変数（`_corder`、`_ccurrency`、`_cprod`、`_cprice`、`_cquan`）を構成すると、拡張機能によってそれらの値を対応する宛先へ自動的にマッピングできます。
</blockquote>


### Standardタブ

PPSタグまたはPPLタグを使用する場合は、このタブの宛先変数にマッピングします。

| パラメータ | 説明 |
|---|---|
| Category ID | リードまたは売上が属するカテゴリーの識別子。 |
| Customer ID | 顧客の一意の識別子。 |
| Order ID | 注文の識別子。 |
| SubOrder ID | 注文に関する追加情報の識別子。 |
| Currency Symbol | 商品に適用される通貨。例：米ドルの場合はUSD。 |
| Total Price | 注文内の商品の合計金額。 |
| Commission Fix | 注文に適用される固定コミッション。 |
| Commission Percent | 合計金額に基づくコミッションの割合。 |
| Session ID | 取引が発生したセッションの識別子。 |
| Partner ID | Zanoxによって割り当てられたパートナー識別子の値。 |
| Review Note | 注文に関するコメントまたは個別の備考。 |
| Maturity Date | 注文の確定日。 |

### MasterTagタブ

MasterTagを使用する場合は、このタブの宛先変数にマッピングします。

| パラメータ | 説明 |
|---|---|
| zx_class (div container class id) | divコンテナの識別子。 |
| zx_identifier | 商品の識別子。 |
| zx_fn | 商品名。 |
| zx_brand | 商品のブランド名。 |
| zx_category | 商品が属するカテゴリー。 |
| zx_amount | 数値で表した商品価格。例：2.99。 |
| zx_price | 通貨記号を含む商品価格。例：2.99$ |
| zx_currency | 注文に適用される通貨。例：USD |
| zx_description | 商品の説明。 |
| zx_url | 商品ページのURL。 |
| zx_photo | 商品画像のURL。 |
| zx_search_query | 検索語句／テキスト。 |


## ベンダーのドキュメント

* [広告主向けFAQ](http://www.zanox.com/gb/advertisers/faq/)
* [用語集](http://wiki.zanox.com/en/Acronyms_and_Terms)
* [サポートおよびドキュメント（広告主向け）](http://www.zanox.com/gb/advertisers/how-to-start/help/)