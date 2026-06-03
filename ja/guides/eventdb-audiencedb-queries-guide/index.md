---
title: EventDBおよびAudienceDBクエリとレポート
description: このガイドでは、訪問の行動、セッション活動、デバイス使用、およびオムニチャネルの帰属に関するレポートを作成するためのEventDBおよびAudienceDBのサンプルSQLクエリを提供します。
url: https://docs.tealium.com/ja/guides/eventdb-audiencedb-queries-guide/
---
各セクションには、スキーマに合わせて調整できるサンプルクエリが含まれています。このガイドで取り上げるシナリオには以下が含まれます：

* バウンスセッションとセッション行動
* 時間経過による訪問と訪問数
* トップページとエントランス
* 既知の訪問とアイデンティティのスティッチング
* デバイス間の使用
* チャネル帰属とオフライン購入活動

## 要件

これらのクエリを実行するには、以下が必要です：

* Tealium AudienceStream
* アカウントとプロファイルに対して有効にされたEventDBおよびAudienceDB。[AudienceDBとEventDBの構成]()を参照してください。
* 以下の表にリストされている属性をAudienceStreamで構成する必要があります。デフォルト属性はすべてのアカウントで利用可能です。カスタム属性の構成については、アカウントマネージャーにお問い合わせください。

各クエリで、`ACCOUNT__PROFILE`をデータベース名に置き換えてください。この値は、例えば`mycompany__main`のように、Tealiumアカウントとプロファイルをダブルアンダースコアで結合したものです。


これらのクエリの列名は、属性タイトルに基づいてAudienceDBおよびEventDBビューの命名規則に従います。アカウントで属性を定義する方法によって、実際の列名が異なる場合があります。クエリを実行する前に、スキーマに対して列名を確認してください。


### 必要なAudienceDB属性

| テーブル | 属性 | タイプ |
|---|---|---|
| `visitor_replaces_view` | `visitor - id` | デフォルト |
| `visitor_replaces_view` | `visitor - replaces id` | デフォルト |
| `visits_view` | `visit - property - active device (46)` | デフォルト |
| `visits_view` | `visit - visitor id` | デフォルト |
| `visitor_tallies_view_normalized` | `visitor tally - lifetime devices used - key` | デフォルト |
| `visitor_tallies_view_normalized` | `visitor - id` | デフォルト |
| `visitors_view_normalized` | `visitor - id` | デフォルト |
| `visitors_view_normalized` | `visitor - metric - average visit duration in minutes` | デフォルト |

### 必要なEventDB属性

| テーブル | 属性 | タイプ |
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

EventDBはページビュー、セッション、タイムスタンプなどのイベントレベルデータを保存します。これらのクエリを使用して、トラフィックパターンとセッション行動を分析します。

EventDBテーブルとスキーマについての詳細は、[EventDBデータガイド]()を参照してください。

### バウンスセッション

バウンスは単一ページビューのセッションです。`utag_main__pn`クッキーはセッション内のページ番号を追跡します。値が`1`の場合、訪問は最初のページを超えて進まなかったことを示します。

```sql
SELECT
  COUNT(DISTINCT &#34;event - first party cookies - utag_main_ses_id&#34;)
    AS total_sessions,
  COUNT(DISTINCT CASE
    WHEN &#34;event - first party cookies - utag_main__pn&#34; = 1
    THEN &#34;event - first party cookies - utag_main_ses_id&#34;
  END)
    AS bounced_sessions
FROM ACCOUNT__PROFILE.events_view__all_events__all_events;
```

### 時間ごとの訪問と訪問数

このクエリは、時間ごとのユニークな訪問とセッション数をカウントします。

```sql
SELECT
  DATE_TRUNC(&#39;hour&#39;, &#34;event - time&#34;)                               AS hour,
  COUNT(DISTINCT &#34;event - visitor id&#34;)                             AS visitors,
  COUNT(DISTINCT &#34;event - first party cookies - utag_main_ses_id&#34;) AS visits
FROM ACCOUNT__PROFILE.events_view__all_events__all_events
GROUP BY hour
ORDER BY hour;
```

### ビューとエントランスでトップのページ

エントランスは、URLがセッションの最初のページである場合に発生し、`utag_main__pn = 1`によって識別されます。

```sql
SELECT
  &#34;event - page url - full_url&#34;  AS page,
  COUNT(*)                       AS pageviews,
  COUNT(DISTINCT CASE
    WHEN &#34;event - first party cookies - utag_main__pn&#34; = 1
    THEN &#34;event - first party cookies - utag_main_ses_id&#34;
  END)                           AS entrances
FROM ACCOUNT__PROFILE.events_view__all_events__all_events
GROUP BY page
ORDER BY pageviews DESC
LIMIT 10;
```

### トップページのバウンスセッション

このクエリは、ページビュー数とバウンスセッション数を組み合わせて、高トラフィックページでの高バウンス率を特定します。

```sql
SELECT
  &#34;event - page url - full_url&#34;  AS page,
  COUNT(DISTINCT &#34;event - first party cookies - utag_main_ses_id&#34;)
    AS sessions,
  COUNT(DISTINCT CASE
    WHEN &#34;event - first party cookies - utag_main__pn&#34; = 1
    THEN &#34;event - first party cookies - utag_main_ses_id&#34;
  END)
    AS bounce_sessions
FROM ACCOUNT__PROFILE.events_view__all_events__all_events
GROUP BY page
ORDER BY sessions DESC
LIMIT 10;
```



### チャネルサマリー

このクエリは、日付とチャネルごとにイベントをグループ化して、チャネルごとの日別訪問数を表示します。

```sql
SELECT
  DATE(e.&#34;event - time&#34;)                                       AS start_date,
  e.&#34;event - first party cookies - channel_name_cookie&#34;        AS channel,
  COUNT(DISTINCT &#34;event - visitor id&#34;)                         AS visitors
FROM ACCOUNT__PROFILE.events_view__all_events__all_events e
GROUP BY
  DATE(e.&#34;event - time&#34;),
  e.&#34;event - first party cookies - channel_name_cookie&#34;;
```

## AudienceDBクエリ

AudienceDBは訪問レベルのデータを保存し、アイデンティティのスティッチング結果、デバイスの集計、および長期的な指標を含みます。これらのクエリを使用して、既知の訪問の人口とエンゲージメントの傾向を分析します。

AudienceDBテーブルとスキーマについての詳細は、[AudienceDBデータガイド]()を参照してください。

### 既知の訪問の割合

AudienceStreamは`visitor_replaces_view`でステッチされた訪問のアイデンティティを記録します。これらの2つのクエリを別々に実行し、その後で式を適用します。詳細については、[訪問のスティッチング]()を参照してください。

```sql
-- 既知の訪問
SELECT COUNT(DISTINCT &#34;visitor - id&#34;) AS known_visitors
FROM ACCOUNT__PROFILE.visitor_replaces_view;

-- 合計訪問
SELECT COUNT(DISTINCT &#34;visitor - id&#34;) AS total_visitors
FROM ACCOUNT__PROFILE.visitors_view_normalized;
```

```
% known visitors = known_visitors / total_visitors
```

### ステッチされたアイデンティティを持つ合計訪問

このクエリは、`visitor_replaces_view`に少なくとも1つのステッチされたアイデンティティを持つ訪問をカウントします。

```sql
SELECT
  COUNT(DISTINCT &#34;ID&#34;)
FROM
(
  SELECT
    v.&#34;visitor - id&#34;  AS &#34;ID&#34;,
    COUNT(vr.&#34;visitor - id&#34;) AS &#34;Total Replaces&#34;
  FROM ACCOUNT__PROFILE.visitors_view_normalized v
  INNER JOIN ACCOUNT__PROFILE.visitor_replaces_view vr
    ON vr.&#34;visitor - id&#34; = v.&#34;visitor - id&#34;
  GROUP BY
    v.&#34;visitor - id&#34;
)
WHERE &#34;Total Replaces&#34; &gt;= 1;
```
### 既知の訪問のデバイス分布

このクエリは、既知の訪問がセッション間で使用するデバイスの組み合わせを示します。各行はユニークなデバイスパターンを表し、例えばiPhoneとMacデスクトップの両方を使用した訪問は、`&#34;iPhone used&#34;` および `&#34;Mac desktop used&#34;` の列に表示されます。

```sql
SELECT
  CASE WHEN patterns.&#34;Android&#34; &gt; 0
    THEN &#39;Android&#39; ELSE &#39; &#39; END               AS &#34;Android used&#34;,
  CASE WHEN patterns.&#34;BlackBerry&#34; &gt; 0
    THEN &#39;BlackBerry&#39; ELSE &#39; &#39; END            AS &#34;BlackBerry used&#34;,
  CASE WHEN patterns.&#34;Chromebook&#34; &gt; 0
    THEN &#39;Chromebook&#39; ELSE &#39; &#39; END            AS &#34;Chromebook used&#34;,
  CASE WHEN patterns.&#34;iPad&#34; &gt; 0
    THEN &#39;iPad&#39; ELSE &#39; &#39; END                  AS &#34;iPad used&#34;,
  CASE WHEN patterns.&#34;iPhone&#34; &gt; 0
    THEN &#39;iPhone&#39; ELSE &#39; &#39; END                AS &#34;iPhone used&#34;,
  CASE WHEN patterns.&#34;Mac desktop&#34; &gt; 0
    THEN &#39;Mac desktop&#39; ELSE &#39; &#39; END           AS &#34;Mac desktop used&#34;,
  CASE WHEN patterns.&#34;other&#34; &gt; 0
    THEN &#39;other&#39; ELSE &#39; &#39; END                 AS &#34;Other used&#34;,
  CASE WHEN patterns.&#34;Windows desktop&#34; &gt; 0
    THEN &#39;Windows desktop&#39; ELSE &#39; &#39; END       AS &#34;Windows desktop used&#34;,
  CASE WHEN patterns.&#34;Windows phone&#34; &gt; 0
    THEN &#39;Windows phone&#39; ELSE &#39; &#39; END         AS &#34;Windows phone used&#34;,
  CASE WHEN patterns.&#34;Windows tablet&#34; &gt; 0
    THEN &#39;Windows tablet&#39; ELSE &#39; &#39; END        AS &#34;Windows tablet used&#34;,
  COUNT(DISTINCT patterns.&#34;visit - visitor id&#34;) AS &#34;Unique visitors&#34;
FROM
(
  SELECT
    vs.&#34;visit - visitor id&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;Android&#39;
      THEN 1 ELSE 0 END)         AS &#34;Android&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;BlackBerry&#39;
      THEN 1 ELSE 0 END)         AS &#34;BlackBerry&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;Chromebook&#39;
      THEN 1 ELSE 0 END)         AS &#34;Chromebook&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;iPad&#39;
      THEN 1 ELSE 0 END)         AS &#34;iPad&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;iPhone&#39;
      THEN 1 ELSE 0 END)         AS &#34;iPhone&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;Mac desktop&#39;
      THEN 1 ELSE 0 END)         AS &#34;Mac desktop&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;other&#39;
      THEN 1 ELSE 0 END)         AS &#34;other&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;Windows desktop&#39;
      THEN 1 ELSE 0 END)         AS &#34;Windows desktop&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;Windows phone&#39;
      THEN 1 ELSE 0 END)         AS &#34;Windows phone&#34;,
    SUM(CASE WHEN vs.&#34;visit - property - active device (46)&#34; = &#39;Windows tablet&#39;
      THEN 1 ELSE 0 END)         AS &#34;Windows tablet&#34;
  FROM ACCOUNT__PROFILE.visits_view vs
  WHERE vs.&#34;visit - visitor id&#34; IN (
    SELECT DISTINCT &#34;visitor - id&#34;
    FROM ACCOUNT__PROFILE.visitor_replaces_view
  )
  GROUP BY vs.&#34;visit - visitor id&#34;
) patterns
GROUP BY
  &#34;Android used&#34;,
  &#34;BlackBerry used&#34;,
  &#34;Chromebook used&#34;,
  &#34;iPad used&#34;,
  &#34;iPhone used&#34;,
  &#34;Mac desktop used&#34;,
  &#34;Other used&#34;,
  &#34;Windows desktop used&#34;,
  &#34;Windows phone used&#34;,
  &#34;Windows tablet used&#34;;
```

### 訪問ごとのデバイス数

このクエリは、`visitors_view_normalized` と `visitor_tallies_view_normalized` を結合して、各訪問が使用するユニークなデバイスの数をカウントし、デバイス数ごとに訪問をグループ化します。

```sql
SELECT
  &#34;Unique Devices&#34;,
  COUNT(&#34;visitor - id&#34;) AS &#34;Total Visitors&#34;
FROM
(
  SELECT
    v.&#34;visitor - id&#34;,
    COUNT(DISTINCT t.&#34;visitor tally - lifetime devices used - key&#34;)
      AS &#34;Unique Devices&#34;
  FROM ACCOUNT__PROFILE.visitors_view_normalized v
  LEFT JOIN ACCOUNT__PROFILE.visitor_tallies_view_normalized t
    ON t.&#34;visitor - id&#34; = v.&#34;visitor - id&#34;
    AND t.&#34;visitor tally - lifetime devices used - value&#34; != &#39;&#39;
  GROUP BY v.&#34;visitor - id&#34;
)
GROUP BY &#34;Unique Devices&#34;;
```

### 複数のデバイスを使用する既知の訪問の平均訪問時間

このクエリは、2台以上のデバイスを使用する既知の訪問の合計訪問時間と訪問数を計算します。

```sql
SELECT
  SUM(&#34;Total Duration&#34;),
  COUNT(DISTINCT &#34;ID&#34;)
FROM
(
  SELECT
    v.&#34;visitor - id&#34; AS &#34;ID&#34;,
    SUM(v.&#34;visitor - metric - average visit duration in minutes&#34;)
      AS &#34;Total Duration&#34;,
    COUNT(DISTINCT t.&#34;visitor tally - lifetime devices used - key&#34;)
      AS &#34;Unique Devices&#34;
  FROM ACCOUNT__PROFILE.visitors_view_normalized v
  LEFT JOIN ACCOUNT__PROFILE.visitor_tallies_view_normalized t
    ON t.&#34;visitor - id&#34; = v.&#34;visitor - id&#34;
  WHERE t.&#34;visitor tally - lifetime devices used - key&#34; != &#39;&#39;
  GROUP BY v.&#34;visitor - id&#34;
)
WHERE &#34;Unique Devices&#34; &gt;= 2;
```



## EventDBとAudienceDBの組み合わせ

`visitor_replaces_view` を使用して、EventDBとAudienceDBのデータを組み合わせる際に訪問のIDを解決します。


EventDBのイベントとAudienceDBの訪問テーブルは直接的な結合キーを共有していません。イベントレベルと訪問レベルのデータを組み合わせるには、以下に示すように `visitor_replaces_view` を通じて結合します。


### イベントを訪問プロファイルに結合

このパターンは、イベントテーブルの訪問IDをAudienceDBの正規訪問IDに対して解決し、イベントレコードに訪問属性をエンリッチメントします。

```sql
SELECT
  e.*,
  v.*
FROM ACCOUNT__PROFILE.events_view__all_events__all_events e
LEFT JOIN ACCOUNT__PROFILE.visitor_replaces_view vr
  ON e.&#34;event - visitor id&#34; = vr.&#34;visitor - replaces id&#34;
LEFT JOIN ACCOUNT__PROFILE.visitors_view_normalized v
  ON vr.&#34;visitor - id&#34; = v.&#34;visitor - id&#34;;
```

### 訪問を訪問プロファイルに結合

このパターンは、訪問IDを使用してAudienceDB内の訪問を訪問に結合します。

```sql
SELECT
  v.*,
  vs.*
FROM ACCOUNT__PROFILE.visitors_view_normalized v
LEFT JOIN ACCOUNT__PROFILE.visits_view vs
  ON vs.&#34;visit - visitor id&#34; = v.&#34;visitor - id&#34;;
```

## オムニチャネルクエリ

これらのクエリは、カスタムEventDB属性を使用してオンライン行動とオフラインのコンバージョンを接続します。
### オンライン訪問から1か月以内のオフライン購入

このクエリは、オンライン訪問から1か月以内に発生したオフライン購入を、チャネルと日付ごとにグループ化して特定します。`visitor_replaces_view`を使用してオンラインイベントデータとオフライン購入記録を結合し、`ADD_MONTHS`を使用して1か月の帰属ウィンドウを定義します。

```sql
SELECT
  LOWER(offline_online_combined_date.&#34;event - first party cookies - channel_name_cookie&#34;)
    AS channel,
  DATE(offline_online_combined_date.&#34;date&#34;)                AS date,
  SUM(offline_online_combined_date.&#34;Total Purchase Amount&#34;) AS total_purchase
FROM
(
  SELECT DISTINCT
    offline_online_combined.&#34;visitor - id&#34;,
    offline_online_combined.&#34;event - first party cookies - channel_name_cookie&#34;,
    DATE(offline_online_combined.&#34;purchase_date&#34;) AS &#34;date&#34;,
    offline_online_combined.&#34;purchase_amount&#34;     AS &#34;Total Purchase Amount&#34;
  FROM
  (
    SELECT DISTINCT
      DATE(e.&#34;event - time&#34;)                    AS &#34;start_date&#34;,
      DATE(ADD_MONTHS(e.&#34;event - time&#34;, 1))     AS &#34;end_date&#34;,
      vr.&#34;visitor - id&#34;,
      e.&#34;event - first party cookies - channel_name_cookie&#34;,
      offline_data.&#34;purchase_date&#34;,
      offline_data.&#34;purchase_id&#34;,
      offline_data.&#34;purchase_amount&#34;
    FROM ACCOUNT__PROFILE.events_view__all_events__all_events e
    INNER JOIN ACCOUNT__PROFILE.visitor_replaces_view vr
      ON e.&#34;event - visitor id&#34; = vr.&#34;visitor - replaces id&#34;
    INNER JOIN
    (
      SELECT
        timestamp &#39;epoch&#39;
          &#43; CAST(&#34;event - omnichannel - createddate&#34; AS BIGINT) / 1000
          * interval &#39;1 second&#39; AS &#34;purchase_date&#34;,
        &#34;event - visitor id&#34;    AS &#34;purchase_id&#34;,
        SUM(&#34;event - omnichannel - price&#34;) AS &#34;purchase_amount&#34;
      FROM ACCOUNT__PROFILE.events_view__all_events__all_events
      WHERE &#34;event - omnichannel - createddate&#34; IS NOT NULL
      GROUP BY &#34;purchase_date&#34;, &#34;event - visitor id&#34;
    ) offline_data
      ON offline_data.&#34;purchase_id&#34; = vr.&#34;visitor - id&#34;
      AND offline_data.&#34;purchase_date&#34; &gt;= DATE(e.&#34;event - time&#34;)
      AND offline_data.&#34;purchase_date&#34; &lt;= DATE(ADD_MONTHS(e.&#34;event - time&#34;, 1))
    WHERE
      &#34;event - udo - order_grand_total&#34; IS NOT NULL
      AND e.&#34;event - first party cookies - channel_name_cookie&#34; != &#39;Direct Traffic&#39;
  ) offline_online_combined
) offline_online_combined_date
GROUP BY
  offline_online_combined_date.&#34;event - first party cookies - channel_name_cookie&#34;,
  DATE(offline_online_combined_date.&#34;date&#34;);
```

## 次のステップ

* EventDBとAudienceDBを構成します。[AudienceDBとEventDBの構成]()を参照してください。
* クエリ結果をBIツール（例：TableauやLooker）にエクスポートしてダッシュボードを構築します。
* 訪問のアイデンティティの解決方法を学びます。[訪問のスティッチングについて]()を参照してください。
* [EventDBデータガイド]()および[AudienceDBデータガイド]()で利用可能なテーブルとフィールドを確認してください。