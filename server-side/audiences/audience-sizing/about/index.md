---
title: About audience sizing
description: This article provides information about audience sizing, audience segments, and jobs.
url: https://docs.tealium.com/server-side/audiences/audience-sizing/about/
---
Audience sizing lets you discover and take action on visitors based on their behavior. After specifying a date range and selecting rule conditions, your audience data is searched for visitor profiles that match the selected conditions. When complete, the results are displayed in an interactive Venn diagram showing the number of visitors discovered for each condition and for combinations of conditions.

## Daily visitor query cap

Visitors are sampled by capping the daily visitor count, which determines the sample size of visitors used to project results in Audience Sizing and Audience Discovery queries. The actual query runs on the total visitors matched, not just the capped visitors. Likewise, jobs also run on the total number of matched visitors, not just the sampled visitors.

The **Sample Size of Daily Visitors to Process** profile setting can only be modified by Tealium staff. To adjust this setting, contact your account representative.

![](/images/server-side/daily-visitor-query-cap-setting.jpg)

The default cap is 100,000. That means if your total visitor population is 1,000,000, the projections are performed on a random sample of a 100,000 visitors.

## Segments

Overlapping conditions in the Venn diagram are called segments, and they represent combinations of rule conditions. To view the total number of visitors found for a segment in the Venn diagram, hover over the segment.

You can send one or more segments for a one-time use with a connector action. To send an audience segment to a connector, click **Next** to create a job. For more information, see [Jobs]() and [Create a job]().

## Jobs

When you have selected rule conditions and the results have been displayed, you can create a job to send one or more audience segments to a connector. After you create a job, you must link it to a connector to activate it. For more information on creating a job and linking a job to a connector, see [Manage audience sizing]().

An activated job is run only once. You cannot pause or restart an active job, which helps prevent duplication of jobs, especially jobs that send email to visitors.

A completed job cannot be reused. You can view its configuration or remove it from the jobs list. To view a list of existing jobs, go to **Connect &gt; Audience Connectors &gt; Jobs**.