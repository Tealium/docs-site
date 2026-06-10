---
title: About log streaming
description: This article explains how to use log streaming to route Tealium system logs to external observability, storage, and alerting platforms.
url: https://docs.tealium.com/administration/early-access/log-streaming/about/
---
Log streaming is in Early Access and is only available to select customers. If you are interested in trying this feature, contact your Tealium Support representative.

## Overview

Log streaming routes Tealium logs to your existing observability, storage, and alerting platforms so you can monitor system behavior in the tools you already use.

In this Early Access release, log streaming supports connector error logs.

Use log streaming to:

* Monitor connector reliability in a central location.
* Investigate failures with detailed log records.
* Build dashboards and alerts in your destination platform.
* Store logs in your own systems for retention or compliance needs.

## How it works

Log streaming uses two main components:

### Destinations

Destinations define where log entries are sent. Each destination is backed by a connector and uses a dedicated log streaming action to deliver log data to an external system.

Log streaming destinations are configured in the Log Streaming UI and are separate from connectors configured in the standard connectors screen.

Examples include observability platforms such as Datadog or New Relic, storage systems such as Amazon S3, and streaming platforms such as Confluent Kafka. For more examples, see .

### Log sources

Log sources define which logs are collected and how they are grouped before delivery. Each log source specifies a log type and controls which connectors or actions are monitored. A log source instance is tied to a single destination. To send the same logs to multiple destinations, create separate log source instances.

When a log source generates a log entry, the following process occurs:

1. The log source captures the event.
1. The log source assembles a structured record containing fields such as the connector type, HTTP response status, error code, and execution time.
1. The record is forwarded to the associated destination.
1. The destination connector delivers the log entry to the external platform.
1. The external platform ingests the logs for monitoring, analysis, alerting, or long-term retention.

For example, you might monitor connector errors for a high-priority campaign and send those logs to Datadog so your team can review failures and trigger alerts when error counts rise.

Log streaming delivers logs through connectors and does not store or analyze logs within Tealium.

## Benefits

* **External visibility into connector errors**  
Connector error information is only available inside the Tealium UI by default. Log streaming routes those errors to your observability stack so your team can monitor them without logging into Tealium.
* **Structured data for programmatic analysis**  
Each log record includes fields such as HTTP status codes, error types, and execution times. Use these fields to classify errors, filter noise, and build targeted alerts in your destination platform.
* **Correlated monitoring**  
Send connector errors to the same platform where you monitor the rest of your infrastructure, so you can correlate Tealium failures with broader system events.
* **Long-term error history**  
Tealium does not retain historical error data. Storing logs in your own systems gives you a persistent record for auditing, compliance, or trend analysis.
* **Selective field delivery**  
Use the Send Log Event action to control which fields reach your destination, so you only forward what is relevant to your use case.

## Available destination connectors

Use the following connectors to send log entries:

| Connector | Send Log Event | Send Entire Log Event |
|---| :---: | :---: |
| [Amazon Redshift]() | ✓ | ✓ |
| [Amazon S3]() | ✓ | ✓ |
| [AWS Firehose]() | ✓ | ✗ |
| [AWS Firehose (Tealium Provided Credentials)]() | ✓ | ✗ |
| [Confluent Kafka Connect]() | ✓ | ✓ |
| [Datadog]() | ✓ | ✗ |
| [File Transfer Protocol (SFTP, FTPS)]() | ✓ | ✓ |
| [Google BigQuery]() | ✓ | ✓ |
| [Google Cloud Pub/Sub]() | ✓ | ✗ |
| [Google Cloud Storage]() | ✓ | ✓ |
| [Microsoft Fabric Eventhouse]() | ✓ | ✓ |
| [New Relic]() | ✓ | ✓ |
| [Splunk]() | ✓ | ✓ |
| [Webhook JDBC]() | ✓ | ✓ |

Each destination uses one of two log streaming actions:

* **Send Entire Log Event**  
Sends all available log attributes to the destination in a single payload. Use this action during initial setup to see the complete data structure and identify which fields matter for your use case.
* **Send Log Event**  
Sends only the attributes you explicitly map in the connector action configuration. Only mapped attributes are included in the payload. Use this action in production to control which fields reach your destination. For more information, see [Map event attributes to vendor parameters]().

## Available log sources

The following log source type is supported:

* [Connector Errors]()  
Error logs generated by connector actions. These logs include details such as error codes, execution status, timestamps, and identifiers used for troubleshooting.

## Workflow

Before you begin, decide which connectors and actions to monitor and which external platform receives the logs.

Log streaming counts toward your outbound event connector calls. Monitor only the connectors and actions necessary for your use case.

1. [Create a destination]() for each external system that receives logs.
1. [Create a log source]() to define which connectors and actions to monitor.
1. [Map event attributes to vendor parameters]() by creating enrichments to extract log field values, then mapping those attributes to destination-specific parameters.
1. Verify that log records arrive in your destination system with correctly mapped fields.
1. [Monitor log streaming activity]() using the **Manage Log Streaming** page. Delivery metrics reflect the health of the log delivery pipeline, not the connector operations being monitored.

For troubleshooting connector errors captured in the logs, see [Connector error logging]().

## Next steps

* [Manage log streaming]()
* [Connector error logging]()
