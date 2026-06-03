---
title: LivePerson Connector Setup Guide
description: This article describes how to set up the LivePerson connector.
url: https://docs.tealium.com/server-side-connectors/liveperson-connector/
---
This article describes how to set up the LivePerson connector.

## API Information

This connector uses the following vendor API:

* API Name: LivePerson Proactive Messaging API
* API Version: v1.0
* API Endpoint: `https://proactive-messaging.z1.fs.liveperson.com`
* Documentation: [LivePerson API](https://developers.liveperson.com/proactive-messaging-api.html)


## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().


After adding the connector, configure the following settings:
* **Account ID**: LivePerson site ID
* **Client ID**: Provide your Client ID
* **Client Secret**: Provide your Client Secret
* **API domain**: API domain for authentication (Host)

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send outbound message | ✓ | ✓ |
| Send outbound message batched | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send outbound message

#### Message Parameters
Required parameters:

| **Parameter** | **Description** |
| --- | --- |
| Campaign Name | The name of the campaign. |
| Skill | The skill `ID` of the campaign. |
| Template ID | The template `ID` or Handoff `ID` of the campaign. |
| Consent | In enabling this campaign, company acknowledges and agrees that it is responsible for compliance with all applicable laws and regulations regarding sending messages to consumers. |
| Outbound Number | The number from which message should be sent to consumer. |

#### Consumer Content


| **Parameter** | **Description** |
| --- | --- |
| Consumer Content WA | The WhatsApp phone number of the consumer. |
| Consumer Content SMS | The `SMS` phone number of the consumer. |
| Consumer Content Apple | The Apple `ID` of the consumer. |
| Consumer Content in-app | The in-app identifier of the consumer. |

#### Consumer Variables


| **Parameter** | **Description** |
| --- | --- |
| Variables from 1 to 20 | Variable number to be used in the template for `consumers.variables.1` to `consumers.variables.20`. |

#### Consumer Header Variables


| **Parameter** | **Description** |
| --- | --- |
| Image | The image `URL` for the header. |
| Video | The video `URL` for the header. |
| Document | The document `URL` for the header. |

#### Consumer Info


| **Parameter** | **Description** |
| --- | --- |
| ctype | The customer type. |
| Customer ID | The customer `ID`. |
| Balance | The customer balance. |
| Currency | The customer currency. |
| Social ID | The customer social `ID`. |
| IMEI | The customer `IMEI`. |
| Username | The customer user name. |
| Company Size | The customer company size. |
| Company Branch | The customer company branch. |
| Account Name | The customer account name. |
| Role | The customer role |
| Last Payment Date | The customer last payment date. To send a date in string format, use this pattern: `yyyy-MM-dd`. |
| Registration Date | The customer registration date. To send a date in string format, use this pattern: `yyyy-MM-dd`. |

#### Consumer Personal Info


| **Parameter** | **Description** |
| --- | --- |
| Firstname | The customer first name. |
| Lastname | The customer last name. |
| Age | The customer age. |
| Gender | The customer gender. |
| Language | The customer language. |
| Company | The customer company. |

#### Consumer Contacts


| **Parameter** | **Description** |
| --- | --- |
| Contacts Email | The contact email. |
| Contacts Phone | The contact phone. |
| Contacts Country | The contact country. |
| Contacts Region | The contact region. |

### Send outbound message batched

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

#### Message Parameters
Required parameters:

| **Parameter** | **Description** |
| --- | --- |
| Campaign Name | The name of the campaign. |
| Skill | The skill `ID` of the campaign. |
| Template ID | The template `ID` or Handoff `ID` of the campaign. |
| Consent | In enabling this campaign, company acknowledges and agrees that it is responsible for compliance with all applicable laws and regulations regarding sending messages to consumers. |
| Outbound Number | The number from which message should be sent to consumer. |

#### Consumer Content


| **Parameter** | **Description** |
| --- | --- |
| Consumer Content WA | The WhatsApp phone number of the consumer. |
| Consumer Content SMS | The `SMS` phone number of the consumer. |
| Consumer Content Apple | The Apple `ID` of the consumer. |
| Consumer Content in-app | The in-app identifier of the consumer. |

#### Consumer Variables


| **Parameter** | **Description** |
| --- | --- |
| Variables from 1 to 20 | Variable number to be used in the template for `consumers.variables.1` to `consumers.variables.20`. |

#### Consumer Header Variables


| **Parameter** | **Description** |
| --- | --- |
| Image | The image `URL` for the header. |
| Video | The video `URL` for the header. |
| Document | The document `URL` for the header. |

#### Consumer Info


| **Parameter** | **Description** |
| --- | --- |
| ctype | The customer type. |
| Customer ID | The customer `ID`. |
| Balance | The customer balance. |
| Currency | The customer currency. |
| Social ID | The customer social `ID`. |
| IMEI | The customer `IMEI`. |
| Username | The customer user name. |
| Company Size | The customer company size. |
| Company Branch | The customer company branch. |
| Account Name | The customer account name. |
| Role | The customer role |
| Last Payment Date | The customer last payment date. To send a date in string format, use this pattern: `yyyy-MM-dd`. |
| Registration Date | The customer registration date. To send a date in string format, use this pattern: `yyyy-MM-dd`. |

#### Consumer Personal Info


| **Parameter** | **Description** |
| --- | --- |
| Firstname | The customer first name. |
| Lastname | The customer last name. |
| Age | The customer age. |
| Gender | The customer gender. |
| Language | The customer language. |
| Company | The customer company. |

#### Consumer Contacts


| **Parameter** | **Description** |
| --- | --- |
| Contacts Email | The contact email. |
| Contacts Phone | The contact phone. |
| Contacts Country | The contact country. |
| Contacts Region | The contact region. |

