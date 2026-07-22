---
title: Tealium + ObservePoint Integration Guide
description: This article describes how to get the most out of Tealium and ObservePoint by setting up the ObservePoint tag in your Tealium iQ Tag Management account and configuring it to send Tealium audiences and badges to ObservePoint.
url: https://docs.tealium.com/partners-and-industries/tech-partners/tealium-observepoint-integration-guide/
---
The Tealium + ObservePoint integration ensures cross-team alignment and data integrity across all of your digital assets — including analytic platforms, personalization tools, and more. This integration allows joint customers to activate automatic ObservePoint scans when updates are made to identify and resolve tracking errors before publishing. With this integration, you can expect to save time, increase agility, and ensure that the data you are using for analysis and personalization is both compliant and consistent.

## Requirements

Integrating ObservePoint with Tealium requires the following:

* Tealium iQ Tag Management
* ObservePoint WebAssurance
* ObservePoint AppAssurance

## How it works

The Tealium Customer Data Hub (CDH) helps organizations manage the full lifecycle of customer data from collection, to enrichment, and then to activation.

* Beginning with data collection, Tealium iQ Tag Management enables you to manage your ObservePoint deployment and associated data alongside other integrated systems using a standardized, vendor-agnostic data layer.
* The Tealium Customer Data Platform (CDP) uses this data collection infrastructure as a data source to create comprehensive customer profiles.
* These customer profiles are configured with business rules to trigger actions with an integrated vendor.

ObservePoint’s WebAssurance and AppAssurance products enable you to test and validate their data collection technologies at scale to ensure accurate data.

* Web Audits and Web Journeys use proprietary technology to scan your analytics implementation to check for inaccuracies and alert you of errors that could threaten your data collection.
* These automated scans allow you to more efficiently monitor and scale your analytics QA testing, leading to greater trust in your data.
* With the acquisition of Strala technologies — Touchpoints, JourneyStream, and Prism — ObservePoint additionally helps you standardize your data upfront, gather and unify online and offline customer touchpoints, and generate accurate and actionable insights that drive growth and increased ROI.

For more information, see [Tealium + ObservePoint Partnership Overview](https://tealium.com/technology-partner/observepoint/%20).

## Integration configuration

The following sections contain additional information about specific Tealium + ObservePoint configuration steps to follow for a successful implementation.

### Use remote file mapping to test Tealium

ObservePoint Remote File Mapping lets you easily perform large scale testing. Using Remote File Mapping allows you see how your data quality will be affected if you publish your tag management changes to your production environment. This can be useful when making changes to your Tealium (or other tag manager) implementation and are apprehensive about publishing to Production.

See [ObservePoint: Using Remote File Substitutions to Test Tealium](https://help.observepoint.com/en/articles/9113442-using-file-substitutions-to-test-tealium) to learn more.

### Check Tealium data objects

Integration with Tealium allows mutual customers to check the data objects (or b objects) within your utag.link and utag.click functions. For example, if you want to test to ensure that you are sending the 'size' option correctly on an e-commerce Add to Basket interaction.

* To learn about setting up your Tealium ObservePoint tag, see the [ObservePoint Data Layer Validator Tag Setup Guide](https://docs.tealium.com/observepoint-data-layer-validator-tag/).
* To learn more about finding your results in ObservePoint, see [ObservePoint: Checking Tealium Data Objects](https://help.observepoint.com/en/articles/9113411-checking-tealium-data-objects).

## Tealium ObservePoint trigger

Using the Tealium ObservePoint trigger allows a group of ObservePoint Audits and Web Journeys to run automatically when you publish to any Tealium profile. This feature is available to any organization that is a mutual customer of both ObservePoint and Tealium.

The primary use of this trigger is to test changes quickly and at scale and then verify that your analytics are functioning properly after you release updates. For example, when you want to test the data quality on 1,000 pages, your e-commerce funnel, and your customer registration funnel automatically each time you publish a change to your Tealium QA profile.

To learn more, see [ObservePoint: Tealium ObservePoint Trigger](https://help.observepoint.com/en/articles/9113192-tealium-observepoint-trigger).