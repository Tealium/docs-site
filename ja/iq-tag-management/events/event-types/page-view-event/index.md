---
title: ページビューイベント
description: ページビューイベントは、訪問がページを閲覧するときにトラッキングデータを送信します。
url: https://docs.tealium.com/ja/iq-tag-management/events/event-types/page-view-event/
---

<blockquote>
ページビューイベントリスナーは現在非推奨です。現在のイベントリスナーについては、[ページロードイベントリスナー](https://docs.tealium.com/page-load-event/)を参照してください。
</blockquote>


## 要件

* utag v4.38以降。`utag.js`テンプレートの更新についての詳細は、当社のナレッジベース記事[utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)を参照してください。

## 動作方法

ページビューイベントは、訪問がページを閲覧するときにトラッキングします。訪問がアクションを実行すると、イベントリスナーはそのデータを既存のトラッキング呼び出しに追加します。


<blockquote>
この動作は、ページビューのペイロードを定義し、指定されたページまたはページが閲覧されたときにタグを発火するロードルールを持つ[データ値構成](https://docs.tealium.com/set-data-values-extension/)拡張機能に似ています。
</blockquote>


イベントリスナーの追加方法についての詳細は、[イベントの管理](https://docs.tealium.com/manage-events/)を参照してください。

### ユースケース


<blockquote>
このイベントリスナーは、すでに他のイベントリスナーに登録しているタグと一緒に使用します。
</blockquote>


訪問がページを閲覧すると、ページビューイベントがタグを発火し、ページビューイベントの変数をタグのペイロードに含めるように、他のイベントとのOR関係にページビューイベントを追加します。

## イベントのトラッキング

ページビューイベントは、このページビューイベントを別のイベントとマージするための`utag.ut.merge()`関数を実行します。詳細については、[ユーティリティ関数](https://docs.tealium.com/ja/platforms/javascript/api/utility-functions/#utagutmerge)を参照してください。

## イベントトリガー

イベントトリガーは、イベントリスナーがトラッキングする特定のアクションです。

イベントのデフォルトはページビューイベントトリガーです。

## イベントトリガー変数

イベントトリガー変数は、イベントリスナーがトラッキング呼び出しと一緒に送信する値です。ページビューイベントには、以下のデフォルトのイベントトリガー変数があります：

### ページビュー

|識別子| 説明|
|---| ---|
|`tealium_event="page_view"`| 訪問が指定されたページを閲覧しました。|
|`iq_event_id` | イベントを送信したイベントリスナーのUIDです。|

**例**

```json
{
   "tealium_event"  : "page_view",
   "iq_event_id:" : "page_view_events_1"
}

```