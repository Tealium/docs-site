---
title: EventDBとAudienceDBのクエリおよびレポート
description: このガイドでは、訪問の行動、セッションアクティビティ、デバイスの使用状況、オムニチャネルアトリビューションに関するレポートを作成するための、EventDBとAudienceDBのSQLクエリ例を紹介します。
url: https://docs.tealium.com/ja/guides/eventdb-audiencedb-queries-guide/
---
各セクションには、スキーマに合わせて変更できるクエリ例が含まれています。このガイドでは、次のシナリオについて説明します。

* バウンスセッションとセッションの動作
* 時系列での訪問数と訪問数
* 上位ページと入口ページ
* 既知の訪問とIDスティッチング
* クロスデバイスでの利用
* チャネルアトリビューションとオフライン購入アクティビティ

## 要件

これらのクエリを実行するには、次のものが必要です。

* Tealium AudienceStream
* アカウントおよびプロファイルでEventDBとAudienceDBが有効になっていること。詳細については、[AudienceDBとEventDBの構成](https://docs.tealium.com/enable-audiencedb-eventdb/)を参照してください。
* 以下の表に示す必須属性がAudienceStreamで構成されていること。デフォルト属性はすべてのアカウントで使用できます。カスタム属性の構成については、アカウントマネージャーにお問い合わせください。

各クエリで、`ACCOUNT__PROFILE`をデータベース名に置き換えてください。この値は、Tealiumのアカウント名とプロファイル名を二重アンダースコアで連結したものです（例：`mycompany__main`）。


<blockquote>
Column names in these queries follow AudienceDB and EventDB view naming conventions based on attribute titles. The exact column names in your account depend on how you define attributes in AudienceStream. Verify column names against your schema before running queries.
</blockquote>


### 必須のAudienceDB属性

| テーブル | 属性 | 種類 |
|---|---|---|
| `visitor_replaces_view` | `visitor - id` | デフォルト |
| `visitor_replaces_view` | `visitor - replaces id` | デフォルト |
| `visits_view` | `visit - property - active device (46)` | デフォルト |
| `visits_view` | `visit - visitor id` | デフォルト |
| `visitor_tallies_view_normalized` | `visitor tally - lifetime devices used - key` | デフォルト |
| `visitor_tallies_view_normalized` | `visitor - id` | デフォルト |
| `visitors_view_normalized` | `visitor - id` | デフォルト |
| `visitors_view_normalized` | `visitor - metric - average visit duration in minutes` | デフォルト |

### 必須のEventDB属性

| テーブル | 属性 | 種類 |
|---|---|---|
| `events_view__all_events__all_events` | `event - visitor id` | デフォルト |
| `events_view__all_events__all_events` | `event - first party cookies - utag_main_ses_id` | デフォルト |
| `events_view__all_events__all_events` | `event - first party cookies - utag_main__pn` | デフォルト |
| `events_view__all_events__all_events` | `event - time` | デフォルト |
| `events_view__all_events__all_events` | `event - page url - full_url` | デフォルト |
| `events_view__all_events__all_events` | `event - omnichannel - createddate` | カスタム |
| `events_view__all_events__all_events` | `event - omnichannel - price` | カスタム |
| `events_view__all_events__all_events` | `event - first party cookies - channel_name_cookie` | カスタム |

## EventDBクエリ

EventDBには、ページビュー、セッション、タイムスタンプなどのイベントレベルのデータが保存されます。これらのクエリを使用して、トラフィックパターンとセッションの動作を分析できます。

EventDBのテーブルとスキーマの詳細については、[EventDBデータガイド](https://docs.tealium.com/eventdb-data-guide/)を参照してください。

### バウンスセッション

バウンスとは、ページビューが1回だけのセッションです。`utag_main__pn` Cookieは、セッション内のページ番号を追跡します。値が`1`の場合、訪問が最初のページから先に進まなかったことを示します。

```sql
SELECT
  COUNT(DISTINCT "event - first party cookies - utag_main_ses_id")
    AS total_sessions,
  COUNT(DISTINCT CASE
    WHEN "event - first party cookies - utag_main__pn" = 1
    THEN "event - first party cookies - utag_main_ses_id"
  END)
    AS bounced_sessions
FROM ACCOUNT__PROFILE.events_view__all_events__all_events;
```

### 1時間あたりの訪問数と訪問数

このクエリは、1時間あたりのユニーク訪問数とセッション数をカウントします。

```sql
SELECT
  DATE_TRUNC('hour', "event - time")                               AS hour,
  COUNT(DISTINCT "event - visitor id")                             AS visitors,
  COUNT(DISTINCT "event - first party cookies - utag_main_ses_id") AS visits
FROM ACCOUNT__PROFILE.events_view__all_events__all_events
GROUP BY hour
ORDER BY hour;
```

### ページビュー数と入口数による上位ページ

入口は、URLがセッションの最初のページである場合に発生し、`utag_main__pn = 1`によって識別されます。

```sql
SELECT
  "event - page url - full_url"  AS page,
  COUNT(*)                       AS pageviews,
  COUNT(DISTINCT CASE
    WHEN "event - first party cookies - utag_main__pn" = 1
    THEN "event - first party cookies - utag_main_ses_id"
  END)                           AS entrances
FROM ACCOUNT__PROFILE.events_view__all_events__all_events
GROUP BY page
ORDER BY pageviews DESC
LIMIT 10;
```

### 上位ページのバウンスセッション

このクエリでは、ページビュー数とバウンスセッション数を組み合わせ、トラフィックとバウンス率の両方が高いページを特定します。

```sql
SELECT
  "event - page url - full_url"  AS page,
  COUNT(DISTINCT "event - first party cookies - utag_main_ses_id")
    AS sessions,
  COUNT(DISTINCT CASE
    WHEN "event - first party cookies - utag_main__pn" = 1
    THEN "event - first party cookies - utag_main_ses_id"
  END)
    AS bounce_sessions
FROM ACCOUNT__PROFILE.events_view__all_events__all_events
GROUP BY page
ORDER BY sessions DESC
LIMIT 10;
```



### チャネルサマリー

このクエリは、イベントを日付とチャネル別にグループ化し、チャネルごとの1日あたりの訪問数を表示します。

```sql
SELECT
  DATE(e."event - time")                                       AS start_date,
  e."event - first party cookies - channel_name_cookie"        AS channel,
  COUNT(DISTINCT "event - visitor id")                         AS visitors
FROM ACCOUNT__PROFILE.events_view__all_events__all_events e
GROUP BY
  DATE(e."event - time"),
  e."event - first party cookies - channel_name_cookie";
```

## AudienceDBクエリ

AudienceDBには、IDスティッチングの結果、デバイスの集計、長期的な指標など、訪問レベルのデータが保存されます。これらのクエリを使用して、既知の訪問層とエンゲージメントの傾向を分析できます。

AudienceDBのテーブルとスキーマの詳細については、[AudienceDBデータガイド](https://docs.tealium.com/audiencedb-data-guide/)を参照してください。

### 既知の訪問の割合

AudienceStreamは、スティッチングされた訪問IDを`visitor_replaces_view`に記録します。次の2つのクエリを個別に実行してから、数式を適用します。詳細については、[訪問スティッチング](https://docs.tealium.com/about-visitor-stitching/)を参照してください。

```sql
-- Known visitors
SELECT COUNT(DISTINCT "visitor - id") AS known_visitors
FROM ACCOUNT__PROFILE.visitor_replaces_view;

-- Total visitors
SELECT COUNT(DISTINCT "visitor - id") AS total_visitors
FROM ACCOUNT__PROFILE.visitors_view_normalized;
```

```
% known visitors = known_visitors / total_visitors
```

### スティッチングされたIDを持つ訪問の合計

このクエリは、`visitor_replaces_view`にスティッチングされたIDが少なくとも1つ存在する訪問をカウントします。

```sql
SELECT
  COUNT(DISTINCT "ID")
FROM
(
  SELECT
    v."visitor - id"  AS "ID",
    COUNT(vr."visitor - id") AS "Total Replaces"
  FROM ACCOUNT__PROFILE.visitors_view_normalized v
  INNER JOIN ACCOUNT__PROFILE.visitor_replaces_view vr
    ON vr."visitor - id" = v."visitor - id"
  GROUP BY
    v."visitor - id"
)
WHERE "Total Replaces" >= 1;
```
### 既知の訪問のデバイス分布

このクエリは、既知の訪問が複数のセッションにわたって使用するデバイスの組み合わせを示します。各行は一意のデバイス使用パターンを表します。たとえば、iPhoneとMacデスクトップの両方を使用した訪問は、`"iPhone used"`列と`"Mac desktop used"`列に表示されます。

```sql
SELECT
  CASE WHEN patterns."Android" > 0
    THEN 'Android' ELSE ' ' END               AS "Android used",
  CASE WHEN patterns."BlackBerry" > 0
    THEN 'BlackBerry' ELSE ' ' END            AS "BlackBerry used",
  CASE WHEN patterns."Chromebook" > 0
    THEN 'Chromebook' ELSE ' ' END            AS "Chromebook used",
  CASE WHEN patterns."iPad" > 0
    THEN 'iPad' ELSE ' ' END                  AS "iPad used",
  CASE WHEN patterns."iPhone" > 0
    THEN 'iPhone' ELSE ' ' END                AS "iPhone used",
  CASE WHEN patterns."Mac desktop" > 0
    THEN 'Mac desktop' ELSE ' ' END           AS "Mac desktop used",
  CASE WHEN patterns."other" > 0
    THEN 'other' ELSE ' ' END                 AS "Other used",
  CASE WHEN patterns."Windows desktop" > 0
    THEN 'Windows desktop' ELSE ' ' END       AS "Windows desktop used",
  CASE WHEN patterns."Windows phone" > 0
    THEN 'Windows phone' ELSE ' ' END         AS "Windows phone used",
  CASE WHEN patterns."Windows tablet" > 0
    THEN 'Windows tablet' ELSE ' ' END        AS "Windows tablet used",
  COUNT(DISTINCT patterns."visit - visitor id") AS "Unique visitors"
FROM
(
  SELECT
    vs."visit - visitor id",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'Android'
      THEN 1 ELSE 0 END)         AS "Android",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'BlackBerry'
      THEN 1 ELSE 0 END)         AS "BlackBerry",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'Chromebook'
      THEN 1 ELSE 0 END)         AS "Chromebook",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'iPad'
      THEN 1 ELSE 0 END)         AS "iPad",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'iPhone'
      THEN 1 ELSE 0 END)         AS "iPhone",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'Mac desktop'
      THEN 1 ELSE 0 END)         AS "Mac desktop",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'other'
      THEN 1 ELSE 0 END)         AS "other",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'Windows desktop'
      THEN 1 ELSE 0 END)         AS "Windows desktop",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'Windows phone'
      THEN 1 ELSE 0 END)         AS "Windows phone",
    SUM(CASE WHEN vs."visit - property - active device (46)" = 'Windows tablet'
      THEN 1 ELSE 0 END)         AS "Windows tablet"
  FROM ACCOUNT__PROFILE.visits_view vs
  WHERE vs."visit - visitor id" IN (
    SELECT DISTINCT "visitor - id"
    FROM ACCOUNT__PROFILE.visitor_replaces_view
  )
  GROUP BY vs."visit - visitor id"
) patterns
GROUP BY
  "Android used",
  "BlackBerry used",
  "Chromebook used",
  "iPad used",
  "iPhone used",
  "Mac desktop used",
  "Other used",
  "Windows desktop used",
  "Windows phone used",
  "Windows tablet used";
```

### 訪問あたりのデバイス数

このクエリは、`visitors_view_normalized`と`visitor_tallies_view_normalized`を結合して、各訪問が使用する一意のデバイス数をカウントし、デバイス数ごとに訪問をグループ化します。

```sql
SELECT
  "Unique Devices",
  COUNT("visitor - id") AS "Total Visitors"
FROM
(
  SELECT
    v."visitor - id",
    COUNT(DISTINCT t."visitor tally - lifetime devices used - key")
      AS "Unique Devices"
  FROM ACCOUNT__PROFILE.visitors_view_normalized v
  LEFT JOIN ACCOUNT__PROFILE.visitor_tallies_view_normalized t
    ON t."visitor - id" = v."visitor - id"
    AND t."visitor tally - lifetime devices used - value" != ''
  GROUP BY v."visitor - id"
)
GROUP BY "Unique Devices";
```

### 複数のデバイスを使用する既知の訪問の平均訪問時間

このクエリは、2台以上のデバイスを使用する既知の訪問について、訪問時間の合計と訪問数を計算します。

```sql
SELECT
  SUM("Total Duration"),
  COUNT(DISTINCT "ID")
FROM
(
  SELECT
    v."visitor - id" AS "ID",
    SUM(v."visitor - metric - average visit duration in minutes")
      AS "Total Duration",
    COUNT(DISTINCT t."visitor tally - lifetime devices used - key")
      AS "Unique Devices"
  FROM ACCOUNT__PROFILE.visitors_view_normalized v
  LEFT JOIN ACCOUNT__PROFILE.visitor_tallies_view_normalized t
    ON t."visitor - id" = v."visitor - id"
  WHERE t."visitor tally - lifetime devices used - key" != ''
  GROUP BY v."visitor - id"
)
WHERE "Unique Devices" >= 2;
```



## EventDBとAudienceDBの組み合わせ

EventDBとAudienceDBのデータを組み合わせる際は、訪問のIDを解決するために`visitor_replaces_view`を使用します。


<blockquote>
EventDB events and AudienceDB visits tables don't share a direct join key. To combine event-level and visitor-level data, join through `visitor_replaces_view` as shown below.
</blockquote>


### イベントと訪問プロファイルの結合

このパターンでは、イベントテーブルの訪問IDをAudienceDBの正規訪問IDと照合して解決し、イベントレコードに訪問属性を追加します。

```sql
SELECT
  e.*,
  v.*
FROM ACCOUNT__PROFILE.events_view__all_events__all_events e
LEFT JOIN ACCOUNT__PROFILE.visitor_replaces_view vr
  ON e."event - visitor id" = vr."visitor - replaces id"
LEFT JOIN ACCOUNT__PROFILE.visitors_view_normalized v
  ON vr."visitor - id" = v."visitor - id";
```

### 訪問と訪問プロファイルの結合

このパターンでは、訪問IDを使用して、AudienceDB内の訪問データと訪問データを結合します。

```sql
SELECT
  v.*,
  vs.*
FROM ACCOUNT__PROFILE.visitors_view_normalized v
LEFT JOIN ACCOUNT__PROFILE.visits_view vs
  ON vs."visit - visitor id" = v."visitor - id";
```

## オムニチャネルクエリ

これらのクエリでは、EventDBのカスタム属性を使用して、オンラインでの行動とオフラインでのコンバージョンを関連付けます。
### オンライン訪問から1か月以内のオフライン購入

このクエリは、オンライン訪問から1か月以内に発生したオフライン購入を特定し、チャネルと日付別にグループ化します。`visitor_replaces_view` を介してオンラインイベントデータとオフライン購入レコードを結合し、`ADD_MONTHS` を使用して1か月のアトリビューション期間を定義します。

```sql
SELECT
  LOWER(offline_online_combined_date."event - first party cookies - channel_name_cookie")
    AS channel,
  DATE(offline_online_combined_date."date")                AS date,
  SUM(offline_online_combined_date."Total Purchase Amount") AS total_purchase
FROM
(
  SELECT DISTINCT
    offline_online_combined."visitor - id",
    offline_online_combined."event - first party cookies - channel_name_cookie",
    DATE(offline_online_combined."purchase_date") AS "date",
    offline_online_combined."purchase_amount"     AS "Total Purchase Amount"
  FROM
  (
    SELECT DISTINCT
      DATE(e."event - time")                    AS "start_date",
      DATE(ADD_MONTHS(e."event - time", 1))     AS "end_date",
      vr."visitor - id",
      e."event - first party cookies - channel_name_cookie",
      offline_data."purchase_date",
      offline_data."purchase_id",
      offline_data."purchase_amount"
    FROM ACCOUNT__PROFILE.events_view__all_events__all_events e
    INNER JOIN ACCOUNT__PROFILE.visitor_replaces_view vr
      ON e."event - visitor id" = vr."visitor - replaces id"
    INNER JOIN
    (
      SELECT
        timestamp 'epoch'
          + CAST("event - omnichannel - createddate" AS BIGINT) / 1000
          * interval '1 second' AS "purchase_date",
        "event - visitor id"    AS "purchase_id",
        SUM("event - omnichannel - price") AS "purchase_amount"
      FROM ACCOUNT__PROFILE.events_view__all_events__all_events
      WHERE "event - omnichannel - createddate" IS NOT NULL
      GROUP BY "purchase_date", "event - visitor id"
    ) offline_data
      ON offline_data."purchase_id" = vr."visitor - id"
      AND offline_data."purchase_date" >= DATE(e."event - time")
      AND offline_data."purchase_date" <= DATE(ADD_MONTHS(e."event - time", 1))
    WHERE
      "event - udo - order_grand_total" IS NOT NULL
      AND e."event - first party cookies - channel_name_cookie" != 'Direct Traffic'
  ) offline_online_combined
) offline_online_combined_date
GROUP BY
  offline_online_combined_date."event - first party cookies - channel_name_cookie",
  DATE(offline_online_combined_date."date");
```

## 次のステップ

* EventDBとAudienceDBを構成します。[AudienceDBとEventDBの構成](https://docs.tealium.com/enable-audiencedb-eventdb/)を参照してください。
* クエリ結果をTableauやLookerなどのBIツールにエクスポートして、ダッシュボードを作成します。
* 訪問IDがどのように統合されるかを確認します。[訪問のスティッチング](https://docs.tealium.com/about-visitor-stitching/)を参照してください。
* [EventDBデータガイド](https://docs.tealium.com/eventdb-data-guide/)および[AudienceDBデータガイド](https://docs.tealium.com/audiencedb-data-guide/)で、利用可能なテーブルとフィールドを確認します。