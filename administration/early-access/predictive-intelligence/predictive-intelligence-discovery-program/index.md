---
title: Predictive Intelligence Discovery Program
description: Learn how Tealium uses your DataAccess data to build and evaluate machine learning models through the Predictive Intelligence Discovery Program.
url: https://docs.tealium.com/administration/early-access/predictive-intelligence/predictive-intelligence-discovery-program/
---

<blockquote>
The Predictive Intelligence Discovery Program is in Early Access and is only available to select customers. Contact your Customer Success Manager to learn more.
</blockquote>


The Predictive Intelligence Discovery Program is a data science engagement where Tealium builds and evaluates machine learning models using your first-party data stored in [Tealium DataAccess](https://docs.tealium.com/about-dataaccess/). Each study validates whether a specific predictive capability is feasible before any roadmap commitment is made.

Your team does not need to provide data science resources or model infrastructure. Each study operates on data already stored in Tealium DataAccess and does not generate new inbound events or affect your usage level.

## Requirements

This feature requires the following:

* An active Tealium DataAccess subscription.
* Historical data stored in Tealium DataAccess covering the agreed lookback window, typically one month or more.
* An attribute in your data that indicates the target outcome. For example, an attribute that indicates a purchase.
* A point of contact from your team who can confirm data definitions and participate in the findings review.

Tealium may define additional requirements during the scoping phase, which may vary by study type.

## How it works

Each study follows a defined five-step process:

1. **Scoping**: Tealium and your team agree on the prediction problem, success criteria, and data requirements. For example, predicting propensity to buy based on early session behavior using 30 days of historical data.
1. **Data preparation**: Tealium works directly with your historical data stored in Tealium DataAccess. You do not need to export data or take any action. Tealium handles all preprocessing, feature engineering, and labeling.
1. **Model development**: Tealium builds, trains, and tunes a model within Tealium's production environment. Tealium does not replicate your data to a development or test environment.
1. **Evaluation**: Tealium validates the model against agreed success criteria, such as accuracy, precision, and recall.
1. **Findings report**: Tealium delivers a report covering model performance, recommended thresholds, limitations, and implications for a potential production offering.

## What's included

Participation in the program includes:

* A predictive model built and evaluated by Tealium using data stored in Tealium DataAccess.
* An out-of-time validation report (validation using a later time period) with quantitative performance results.
* A collaborative review session to walk through the findings.

## Limitations

Models built during this program are for evaluation purposes only and cannot be activated or deployed for live use cases. Any production capability based on study findings requires a separate product investment.

## Join the program

To join the Predictive Intelligence Discovery Program, contact your Customer Success Manager. For more information about the Early Access program, see [About Early Access](https://docs.tealium.com/about-early-access/).
