---
title: The Trade Desk Universal Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでThe Trade Desk Universal Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/the-trade-desk-universal-pixel-tag/
---
## タグの構成

まず、タグマーケットプレイスに移動し、The Trade Desk Universal Pixelタグをプロファイルに追加します（[タグの追加](https://docs.tealium.com/manage-tags/#add-a-tag)を参照）。

タグを追加する際は、次の構成を構成します。

1. **広告主ID**：Trade Deskから提供された広告主IDを入力します。このIDはUniversal Pixelタグに含まれています。
1. **ピクセルID**：Trade Deskから提供されたピクセルIDを入力します。このIDはUniversal Pixelタグに含まれています。


<blockquote>
タグ構成を動的に構成する場合は、データマッピングを使用してください。
</blockquote>


## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

推奨ロードルール：**すべてのページで読み込む**。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

The Trade Desk Universal Pixelタグの宛先変数は、タグの「データマッピング」タブに組み込まれています。

使用可能なカテゴリは次のとおりです。

### 標準

|**宛先名**| **説明**|
|---| ---|
|広告主ID|Trade Deskから提供された広告主の一意の識別子|
|ピクセルID|Trade Deskから提供されたピクセルの一意の識別子|
| `td1`| カスタマーパラメータ#1 |
| `td2`| カスタマーパラメータ#2 |
| `td3`| カスタマーパラメータ#3 |
| `td4`| カスタマーパラメータ#4 |
| `td5`| カスタマーパラメータ#5 |
| `td6`| カスタマーパラメータ#6 |
| `td7`| カスタマーパラメータ#7 |
| `td8`| カスタマーパラメータ#8 |
| `td9`| カスタマーパラメータ#9 |
| `td10`| カスタマーパラメータ#10 |

### 同意（GDPR）

同意パラメータは、URLベースのサービスに関するIAB仕様に準拠しています。

参照：[URLベースのサービスにおけるIAB GDPR同意情報の受け渡し](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/URL-based%20Consent%20Passing_%20Framework%20Guidance.md)


<blockquote>
URLの作成者は、これらのパラメータが一度だけ追加され、それらを想定し適切に処理できるサービスに渡されるようにする必要があります。
</blockquote>


|宛先名| **値**| **説明**|
|---| ---| ---|
|`gdpr`| `0` / `1`| ユーザーにGDPRを適用するかどうかを決定します。値が`1`の場合は「はい」を意味し、デフォルト値の`0`は「いいえ」を意味します。|
|`gdpr_consent`| URLセーフなBase64でエンコードされたGDPR同意文字列| このパラメータは、`gdpr`の値が`1`であり、`gdpr_consent`が空文字列でない場合にのみ渡す必要があります。|
|`gdpr_pd`| `0` / `1`| このパラメータは任意であり、個人データが含まれるかどうかを決定します。値が`1`の場合は「はい」を意味し、デフォルト値の`0`は「いいえ」を意味します。|


<blockquote>
IPアドレスやトラッキングピクセルCookieなど、その他の個人データがリクエストの一部として渡される場合があります。呼び出し先は、識別子Cookieまたはその他の個人データを構成または使用できるかどうかを判断するために、`gdpr`および`gdpr_consent`パラメータを使用する必要があります。
</blockquote>
