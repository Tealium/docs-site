---
title: Roku JavaScript Pixel タグ構成ガイド
description: この記事では、Roku JavaScript Pixel タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/roku-javascript-pixel-tag/
---
## タグのヒント

* 標準パラメータを上書きするためにマッピングを使用します。
* サポートされているEコマース拡張パラメータ。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **Ad Account ID**: あなたのRoku広告アカウントID。
* **Generate Event ID**: RokuトラッキングイベントごとにイベントIDを自動生成します。Roku Events APIコネクタを実装する際の重複排除に使用されます。デフォルト値は`true`です。詳細については、[Roku Events APIコネクタ](https://docs.tealium.com/roku-events-api-connector/)を参照してください。
* **Auto PageView Tracking**: ページビューを自動的に追跡します。デフォルト値は`true`です。
* **Auto Purchase Tracking**: `order_id`または`_corder`が存在する場合、自動的に購入イベントをトリガーします。デフォルト値は`true`です。

### Roku Events API


<blockquote>
この機能にはアクティブな[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)が必要です。
</blockquote>


Roku Events APIをサポートするために、**Generate Event ID**を`true`に構成します。**Generate Event ID**が有効になっている場合、このタグは追跡された各イベントに対して一意のイベントIDを生成し、それをTealium EventStreamの属性として送信し、Roku Events APIコネクタで使用し、`event_id`パラメータでRoku JavaScript Pixelに渡します。このイベントID属性は、コネクタでマッピングされ、ウェブベースのタグとサーバーサイドの統合を同期させることができます。

タグは以下の命名規則を使用してイベントIDを送信します：

```nohl
roku_event_id_{EVENT_NAME}_{TAG_UID}
```

例えば、タグ＃32からの購入イベントは以下の属性と値を送信します：

```json
{
  "roku_event_id_purchase_32": "028b2ade7478..."
}
```

同じタグからのページビューイベントは以下の属性と値を送信します：

```json
{
  "roku_event_id_page_view_32": "084b1cda7461..."
}
```

#### 重複排除

適切なイベントの重複排除を保証するために、Roku Events APIコネクタのPixelタグからのイベントIDをTealium Collectタグによって送信されるペイロードに含める必要があります。これを行うには、以下の手順を使用します：

* **Tag Timing**ドロップダウンから**Prioritized**を選択します。
* **Bundle Flag**トグルを`On`に構成します。
* **Load Order Manager**を使用して、Roku JavaScript PixelタグをTealium Collectタグの前に発火させます。Tealium Collectタグは最後に発火させることをお勧めします。詳細については、[Load Order Manager](https://docs.tealium.com/load-order-manager/)を参照してください。

これらのイベントID属性の使用に関する情報については、[Roku: Events APIコネクタ](https://docs.tealium.com/roku-events-api-connector/)および[Roku: Conversions API](https://help.ads.roku.com/en/articles/8880744-conversions-api)を参照してください。