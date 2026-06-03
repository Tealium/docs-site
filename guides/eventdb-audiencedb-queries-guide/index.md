---
title: EventDB and AudienceDB queries and reports
description: This guide provides sample SQL queries for EventDB and AudienceDB to build reports on visitor behavior, session activity, device usage, and omnichannel attribution.
url: https://docs.tealium.com/guides/eventdb-audiencedb-queries-guide/
---
Each section includes sample queries that you can adapt to your schema. Scenarios covered in this guide include:

* Bounce sessions and session behavior
* Visitors and visits over time
* Top pages and entrances
* Known visitors and identity stitching
* Cross-device usage
* Channel attribution and offline purchase activity

## Requirements

To run these queries, you need:

* Tealium AudienceStream
* EventDB and AudienceDB enabled for your account and profile. See [Configure AudienceDB and EventDB]().
* The required attributes configured in AudienceStream as listed in the tables below. Default attributes are available in all accounts. Contact your account manager for custom attribute configuration.

In each query, replace `ACCOUNT__PROFILE` with your database name. This value is your Tealium account and profile joined with a double underscore, for example `mycompany__main`.


Column names in these queries follow AudienceDB and EventDB view naming conventions based on attribute titles. The exact column names in your account depend on how you define attributes in AudienceStream. Verify column names against your schema before running queries.


### Required AudienceDB attributes

| Table | Attribute | Type |
|---|---|---|
| `visitor_replaces_view` | `visitor - id` | Default |
| `visitor_replaces_view` | `visitor - replaces id` | Default |
| `visits_view` | `visit - property - active device (46)` | Default |
| `visits_view` | `visit - visitor id` | Default |
| `visitor_tallies_view_normalized` | `visitor tally - lifetime devices used - key` | Default |
| `visitor_tallies_view_normalized` | `visitor - id` | Default |
| `visitors_view_normalized` | `visitor - id` | Default |
| `visitors_view_normalized` | `visitor - metric - average visit duration in minutes` | Default |

### Required EventDB attributes

| Table | Attribute | Type |
|---|---|---|
| `events_view__all_events__all_events` | `event - visitor id` | Default |
| `events_view__all_events__all_events` | `event - first party cookies - utag_main_ses_id` | Default |
| `events_view__all_events__all_events` | `event - first party cookies - utag_main__pn` | Default |
| `events_view__all_events__all_events` | `event - time` | Default |
| `events_view__all_events__all_events` | `event - page url - full_url` | Default |
| `events_view__all_events__all_events` | `event - omnichannel - createddate` | Custom |
| `events_view__all_events__all_events` | `event - omnichannel - price` | Custom |
| `events_view__all_events__all_events` | `event - first party cookies - channel_name_cookie` | Custom |

## EventDB queries

EventDB stores event-level data such as page views, sessions, and timestamps. Use these queries to analyze traffic patterns and session behavior.

For more information about EventDB tables and schema, see [EventDB data guide]().

### Bounce sessions

A bounce is a session with a single page view. The `utag_main__pn` cookie tracks the page number within a session. A value of `1` indicates the visitor didn&#39;t advance past the first page.

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

### Visitors and visits per hour

This query counts unique visitors and sessions per hour.

```sql
SELECT
  DATE_TRUNC(&#39;hour&#39;, &#34;event - time&#34;)                               AS hour,
  COUNT(DISTINCT &#34;event - visitor id&#34;)                             AS visitors,
  COUNT(DISTINCT &#34;event - first party cookies - utag_main_ses_id&#34;) AS visits
FROM ACCOUNT__PROFILE.events_view__all_events__all_events
GROUP BY hour
ORDER BY hour;
```

### Top pages by views and entrances

An entrance occurs when a URL is the first page of a session, identified by `utag_main__pn = 1`.

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

### Bounce sessions for top pages

This query combines page view counts with bounce session counts to identify high-traffic pages with high bounce rates.

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



### Channel summary

This query groups events by date and channel to show daily visitor counts per channel.

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

## AudienceDB queries

AudienceDB stores visitor-level data, including identity stitching results, device tallies, and long-term metrics. Use these queries to analyze your known visitor population and engagement trends.

For more information about AudienceDB tables and schema, see [AudienceDB data guide]().

### Percentage of known visitors

AudienceStream records stitched visitor identities in `visitor_replaces_view`. Run these two queries separately, then apply the formula. For more information, see [Visitor stitching]().

```sql
-- Known visitors
SELECT COUNT(DISTINCT &#34;visitor - id&#34;) AS known_visitors
FROM ACCOUNT__PROFILE.visitor_replaces_view;

-- Total visitors
SELECT COUNT(DISTINCT &#34;visitor - id&#34;) AS total_visitors
FROM ACCOUNT__PROFILE.visitors_view_normalized;
```

```
% known visitors = known_visitors / total_visitors
```

### Total visitors with stitched identities

This query counts visitors that have at least one stitched identity in `visitor_replaces_view`.

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

### Device distribution for known visitors

This query shows which device combinations known visitors use across sessions. Each row represents a unique device pattern, for example visitors who used both an iPhone and a Mac desktop appear in the `&#34;iPhone used&#34;` and `&#34;Mac desktop used&#34;` columns.

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

### Number of devices per visitor

This query joins `visitors_view_normalized` with `visitor_tallies_view_normalized` to count the number of unique devices each visitor uses, then groups visitors by device count.

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

### Average visit duration for known visitors with multiple devices

This query calculates the total visit duration and visitor count for known visitors who use two or more devices.

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



## Combining EventDB and AudienceDB

Use `visitor_replaces_view` to resolve visitor identities when combining EventDB and AudienceDB data.


EventDB events and AudienceDB visits tables don&#39;t share a direct join key. To combine event-level and visitor-level data, join through `visitor_replaces_view` as shown below.


### Join events to visitor profiles

This pattern resolves visitor IDs from the events table against the canonical visitor ID in AudienceDB, enriching event records with visitor attributes.

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

### Join visits to visitor profiles

This pattern joins visits to visitors within AudienceDB using the visitor ID.

```sql
SELECT
  v.*,
  vs.*
FROM ACCOUNT__PROFILE.visitors_view_normalized v
LEFT JOIN ACCOUNT__PROFILE.visits_view vs
  ON vs.&#34;visit - visitor id&#34; = v.&#34;visitor - id&#34;;
```

## Omnichannel queries

These queries use custom EventDB attributes to connect online behavior to offline conversions.

### Offline purchases within one month of an online visit

This query identifies offline purchases that occurred within one month of an online visit, grouped by channel and date. It joins online event data with offline purchase records through `visitor_replaces_view`, using `ADD_MONTHS` to define the one-month attribution window.

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

## Next steps

* Set up EventDB and AudienceDB. See [Configure AudienceDB and EventDB]().
* Export query results to a BI tool such as Tableau or Looker to build dashboards.
* Learn how visitor identities resolve. See [Visitor stitching]().
* Review available tables and fields in the [EventDB data guide]() and [AudienceDB data guide]().