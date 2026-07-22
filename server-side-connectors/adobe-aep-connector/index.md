---
title: Adobe Experience Platform Connector Setup Guide
description: This article describes how to set up the Adobe Experience Platform connector.
url: https://docs.tealium.com/server-side-connectors/adobe-aep-connector/
---
The Adobe Experience Platform Edge Network provides an optimized way for customers to interact with any Adobe Experience Cloud or Adobe Experience Platform Edge services.

Because the API does not rely on any libraries to load, it provides a lightning-fast way to interact with the Adobe Experience Platform Edge Network and supported solutions, like Adobe Analytics, Adobe Audience Manager, and Adobe Target.

## How it works

The Adobe Experience Platform connector provides an optimized way to interact with any Adobe Experience Platform service. This connector sends event data through the Adobe Experience Platform to Adobe Experience Cloud services, such as Adobe Analytics, Adobe Audience Manager, Adobe Target, and Adobe CDP. 

### Data types

The Adobe Experience Platform connector supports all Tealium data types, but arrays and maps are transformed within the connector before data is sent to Adobe.

#### Mapping arrays of objects

To map an array of objects with dynamic lengths, the connector accepts an array per object attribute. The connector then merges these properties into a well-formed JSON array of objects.

For example, if you want to send an Adobe Analytics list, you can use this connector to send the data as an array of objects. The connector will map the list in the following ways:

* `_experience.analytics.customDimensions.lists.list1.list.key` to `['productCategories','productCategories','productCategories']`
* `_experience.analytics.customDimensions.lists.list1.list.value` to `['clothing','shoes','accessories']`

The connector will merge these arrays into the following JSON format:

```json
"xdm": {
    "_experience": {
        "analytics": {
            "customDimensions": {
                "lists": {
                    "list1": {
                        "list": [
                            {
                                "key": "productCategories",
                                "value": "clothing"
                            },
                            {
                                "key": "productCategories",
                                "value": "shoes"
                            },
                            {
                                "key": "productCategories",
                                "value": "accessories"
                            }
                        ]
                    }
                }
            }
        }
    }
}
```

If you pass an empty optional array value to the connector, then the connector passes an empty value in the corresponding object's attribute. For example, if you mapped `experience.analytics.customDimensions.lists.list1.list.key` to `['clothing','','accessories']`, the attribute key will not be present for the second object in the list array.

If the schema requires an attribute and it is not included in the array, the entire object will not be included in the array sent to Adobe.

#### Sending map attributes

Your connector configuration may require map attributes with identity namespaces. To send this data to Adobe, use strings, numbers, and array of strings attributes. We recommend using strings or arrays of strings for numerical values because arrays of numbers cannot include null or empty values.

For example, if you want to send the following `segmentMembership` values to Adobe:

```json
"segmentMembership":{
   "Email":{
      "a@example.com":{
        "version": 1,
      },
      "b@example.com":{
        "status": "exited"
      },
      "c@example.com":{
        "version": 3,
        "status": "in"
      },
   }
}
```
You will need to map the following arrays in the connector:

* `segmentMembership.Email`: `["a@example.com","b@example.com","c@example.com"]`
* `segmentMembership.Email.version`: `["1", "", "3"]` (An array of strings that includes an empty value for the second email.)
* `segmentMembership.Email.status`: `['', 'exited', 'in']` (Includes an empty value for the first email.)
* `segmentMembership.Email.validUntil`: `null`

## API information

This connector uses the following vendor API:

* API Name: Adobe Experience Platform API
* API Version: v2.0
* API Endpoint: `https://server.adobedc.net/ee/v2/interact`
* Documentation: [Adobe Experience Platform API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=en)

## Configuration

Before you can configure the Adobe Experience Platform connector in Tealium, you need to complete the following steps to generate your credentials in the Adobe Developer Console.

1. Create a new Adobe Developer Console project or use an existing project. See [Projects Overview](https://developer.adobe.com/developer-console/docs/guides/projects/).
1. Add the services to the project that you want associated with the project credentials. See [Services Overview](https://developer.adobe.com/developer-console/docs/guides/services/). 
The following Adobe services are required to integrate with this connector:
    * Experience Platform API
    * I/O Events
1. After you add the services to the project, you can access your project credentials. See [Credentials](https://developer.adobe.com/developer-console/docs/guides/credentials/). Navigate to your project overview and select **OAuth Server-to-Server** in the **Credentials** section. 
The following credentials are required for this connector:
    * Client ID (API Key)
    * Client secret 
    * Organization ID
1. Note your credentials and return to Tealium to complete the connector configuration.
1. In Tealium, navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).
1. After adding the connector, configure the following settings using the credentials that you generated in the previous steps:
    * **Client ID**  
    (Required) The Client ID.
    * **Client Secret**  
    (Required) The Client Secret.
    * **Organization ID**  
    (Required) The Organization ID.
    * **Sandbox**  
    (Optional) If you want the API calls to refer to a different environment than the default one (prod), specify it in this field.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✓ | ✓ |
| Send Event (Batched) | ✓ | ✓ |
| Stream Record Data | ✓ | ✓ |
| Stream Record Data (Batched) | ✓ | ✓ |

### Send Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Datastream ID | The Adobe server-side Datastream configuration you want to use for this action. |
| XDM Schema | The Experience Data Model (XDM) schema that will be used to send data through the datastream. Ensure the XDM schema is associated with the datastream you want to use. For more information about associating an XDM schema with a datastream, see [Generate a Datastream identifier](https://developer.adobe.com/client-sdks/resources/user-guides/getting-started-with-platform/overview/#generate-a-datastream-identifier). |
| Identity Namespaces | Indicates what the identity relates to, such as email addresses or numeric CRM IDs. When matching record data across profile fragments, Adobe Experience Platform uses the identity value and the namespace to merge profile data. <br> If the **XDM Schema** you select contains any kind of map attribute, use this parameter to select the identity namespaces you want to use in the mapping. |
| XDM Schema Parameters | Parameters associated with the XDM schema. Required attributes appear next to a lock icon and are read only. You will need to provide a valid mapping in the drop-down list to the left-hand side.<br> Note: The `identityMap` attribute requires that at least one of its namespaces has the property `primary` set to `true`. If the parameter does not contain any identity namespaces, enter a dash (`-`). |
| XDM Schema Template | Provide a JSON template for the XDM schema. The template should match the structure of your XDM schema, and you can use template variables within the JSON structure. If a value is provided in this field, the XDM Schema Parameters above are ignored.<br>For more information, see [Adobe Developer: Interact Endpoint](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/). |
| Data | Use this field to map a preexisting JSON data layer object to an XDM schema. The sub-properties of the data object can be constructed in a way that maps to the data layer properties that you want to capture. The attribute is fully customizable. |
| Template Variables | Provide template variables as data input for Templates. Name nested template variables with the dot notation. For example, `items.name`. Nested template variables are typically built from data layer list attributes. <br> For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|
| Templates | Provide templates to be referenced in Data section. Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.<br>For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|
| Referer | Identifies the full URL of the page or resource from which the event originated. Used by AEP to associate the interaction with the correct referring context. The default value is the browser's Referer header, if available, or the corresponding data layer property. |
| X-Forwarded-For | Contains the originating IP address of the client connecting through Tealium or another proxy. Used by AEP for geolocation and attribution. The default value is taken from the IP address provided in the incoming request or the Tealium system variable representing the visitor's IP address. |
| X-Forwarded-Proto | Specifies the protocol (HTTP or HTTPS) that the client used to connect. Helps AEP interpret the original request scheme when routed through a proxy. The default value is `HTTPS`. |
| X-Forwarded-Host | Identifies the original host requested by the client, such as `www.clientsite.com`. Required by AEP to maintain accurate host attribution. |
| User-Agent | Provides the full user agent string identifying the client’s browser, operating system, and rendering engine. Used by AEP for device and browser detection. |
| Sec-CH-UA | (Required) Low-entropy Client Hint header listing the browser brands and versions. |
| Sec-CH-UA-Mobile | (Required) Indicates whether the client is on a mobile device. Required by AEP for mobile classification. |
| Sec-CH-UA-Platform | Identifies the platform on which the browser is running (for example, `Windows`, `macOS`, `Android`). |
| Sec-CH-UA-Platform-Version | Provides the version of the operating system platform. Used for advanced device and compatibility attribution. |
| Sec-CH-UA-Arch | Specifies the CPU architecture of the client device (for example, `x86`, `arm`). |
| Sec-CH-UA-Model | Identifies the device model. Primarily used for mobile devices. |
| Sec-CH-UA-Bitness | Indicates the bitness of the client architecture (for example, `64`). |
| Sec-CH-UA-WoW64 | Indicates whether the client is running a 32-bit process on a 64-bit Windows system. |
| Custom Header Key CSV | Provide a custom header key to send with the request. |
| Custom Header Value CSV | Provide a custom header value to send with the request. This value will correlate to the sequence of the custom header key. |

### Send Event (Batched)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 6,000
* Max time since oldest request: 15 minutes

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Datastream ID | The Adobe server-side Datastream configuration you want to use for this action. |
| XDM Schema | The Experience Data Model (XDM) schema that will be used to send data through the datastream. Ensure the XDM schema is associated with the datastream you want to use. For more information about associating an XDM schema with a datastream, see [Generate a Datastream identifier](https://developer.adobe.com/client-sdks/resources/user-guides/getting-started-with-platform/overview/#generate-a-datastream-identifier).  |
| Identity Namespaces | Indicates what the identity relates to, such as email addresses or numeric CRM IDs. When matching record data across profile fragments, Adobe Experience Platform uses the identity value and the namespace to merge profile data. <br> If the **XDM Schema** you select contains any kind of map type attribute, use this parameter to select the identity namespaces you want to use in the mapping.<br>If the parameter does not contain any identity namespaces, enter a dash (`-`). |
| XDM Schema Parameters | Parameters associated with the XDM schema. Required attributes appear next to a lock icon and are read only. You will need to provide a valid mapping in the drop-down list to the left-hand side.<br>Note: The `identityMap` attribute requires that at least one of its namespaces has the property `primary` set to `true`. |
| XDM Schema Template | Provide a JSON template for the XDM schema. The template should match the structure of your XDM schema, and you can use template variables within the JSON structure. If a value is provided in this field, the XDM Schema Parameters above are ignored.<br>For more information, see [Adobe Developer: Interact Endpoint](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/). |
| Data | Use this field to map a preexisting JSON data layer object to an XDM schema. The sub-properties of the data object can be constructed in a way that maps to the data layer properties that you want to capture. The attribute is fully customizable. |
| Template Variables | Provide template variables as data input for Templates. Name nested template variables with the dot notation. For example, `items.name`. Nested template variables are typically built from data layer list attributes. <br> For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|
| Templates | Provide templates to be referenced in Data section. Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.<br>For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|
| Referer | Identifies the full URL of the page or resource from which the event originated. Used by AEP to associate the interaction with the correct referring context. The default value is the browser's Referer header, if available, or the corresponding data layer property. |
| X-Forwarded-For | Contains the originating IP address of the client connecting through Tealium or another proxy. Used by AEP for geolocation and attribution. The default value is taken from the IP address provided in the incoming request or the Tealium system variable representing the visitor's IP address. |
| X-Forwarded-Proto | Specifies the protocol (HTTP or HTTPS) that the client used to connect. Helps AEP interpret the original request scheme when routed through a proxy. The default value is `HTTPS`. |
| X-Forwarded-Host | Identifies the original host requested by the client, such as `www.clientsite.com`. Required by AEP to maintain accurate host attribution. |
| User-Agent | Provides the full user agent string identifying the client’s browser, operating system, and rendering engine. Used by AEP for device and browser detection. |
| Sec-CH-UA | (Required) Low-entropy Client Hint header listing the browser brands and versions. |
| Sec-CH-UA-Mobile | (Required) Indicates whether the client is on a mobile device. Required by AEP for mobile classification. |
| Sec-CH-UA-Platform | Identifies the platform on which the browser is running (for example, `Windows`, `macOS`, `Android`). |
| Sec-CH-UA-Platform-Version | Provides the version of the operating system platform. Used for advanced device and compatibility attribution. |
| Sec-CH-UA-Arch | Specifies the CPU architecture of the client device (for example, `x86`, `arm`). |
| Sec-CH-UA-Model | Identifies the device model. Primarily used for mobile devices. |
| Sec-CH-UA-Bitness | Indicates the bitness of the client architecture (for example, `64`). |
| Sec-CH-UA-WoW64 | Indicates whether the client is running a 32-bit process on a 64-bit Windows system. |
| Custom Header Key CSV | Provide a custom header key to send with the request. |
| Custom Header Value CSV | Provide a custom header value to send with the request. This value will correlate to the sequence of the custom header key. |

### Stream Record Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Dataset | Select the source dataset for record data. |
| Connection | The connection ID. <br>For new connection IDs:<ol><li>Click **Create**.</li><li>In the **Create Connection** screen, enter the name for the connection ID and click **Done**.</li><li>Click **Connect** to finish creating the connection to Adobe AEP endpoints.</li></ol>For existing connection IDs:<ol><li>Click **Connect** to create the connection to the Adobe AEP endpoints.</li></ol>A **Connection Done** message will be displayed after your connection is successfully established.  |
| Identity Namespaces | Indicates what the identity relates to, such as email addresses or numeric CRM IDs. When matching record data across profile fragments, Adobe Experience Platform uses the identity value and the namespace to merge profile data. <br> If the **XDM Schema** you select contains any kind of map attribute, use this parameter to select the identity namespaces you want to use in the mapping. If the parameter does not contain any identity namespaces, enter a dash (`-`). |
| Body parameters | Parameters associated with the XDM schema. Required attributes appear next to a lock icon and are read only. Provide a valid mapping in the drop-down list.<br>Note: The `identityMap` attribute requires that at least one of its namespaces has the property `primary` set to `true`. |
| Created At | A timestamp marking the creation of the connection. |
| Source Name | (Optional) A name for your source. If this value is missing, the streaming message automatically adds the source ID from the streaming connection definition. |
| Referer | Identifies the full URL of the page or resource from which the event originated. Used by AEP to associate the interaction with the correct referring context. The default value is the browser's Referer header, if available, or the corresponding data layer property. |
| X-Forwarded-For | Contains the originating IP address of the client connecting through Tealium or another proxy. Used by AEP for geolocation and attribution. The default value is taken from the IP address provided in the incoming request or the Tealium system variable representing the visitor's IP address. |
| X-Forwarded-Proto | Specifies the protocol (HTTP or HTTPS) that the client used to connect. Helps AEP interpret the original request scheme when routed through a proxy. The default value is `HTTPS`. |
| X-Forwarded-Host | Identifies the original host requested by the client, such as `www.clientsite.com`. Required by AEP to maintain accurate host attribution. |
| User-Agent | Provides the full user agent string identifying the client’s browser, operating system, and rendering engine. Used by AEP for device and browser detection. |
| Sec-CH-UA | (Required) Low-entropy Client Hint header listing the browser brands and versions. |
| Sec-CH-UA-Mobile | (Required) Indicates whether the client is on a mobile device. Required by AEP for mobile classification. |
| Sec-CH-UA-Platform | Identifies the platform on which the browser is running (for example, `Windows`, `macOS`, `Android`). |
| Sec-CH-UA-Platform-Version | Provides the version of the operating system platform. Used for advanced device and compatibility attribution. |
| Sec-CH-UA-Arch | Specifies the CPU architecture of the client device (for example, `x86`, `arm`). |
| Sec-CH-UA-Model | Identifies the device model. Primarily used for mobile devices. |
| Sec-CH-UA-Bitness | Indicates the bitness of the client architecture (for example, `64`). |
| Sec-CH-UA-WoW64 | Indicates whether the client is running a 32-bit process on a 64-bit Windows system. |
| Custom Header Key CSV | Provide a custom header key to send with the request. |
| Custom Header Value CSV | Provide a custom header value to send with the request. This value will correlate to the sequence of the custom header key. |
| Template Variables | Provide template variables as data input for Templates. Name nested template variables with the dot notation. For example, `items.name`. Nested template variables are typically built from data layer list attributes. <br> For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|
| Templates | Provide templates to be referenced in the Body parameters section. Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.<br>For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|

### Stream Record Data (Batched)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 6,000
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Dataset | Select the dataset to ingest record data. |
| Connection | The connection ID. <br>For new connection IDs:<ol><li>Click **Create**.</li><li>In the **Create Connection** screen, enter the name for the connection ID and click **Done**.</li><li>Click **Connect** to finish creating the connection to Adobe AEP endpoints.</li></ol>For existing connection IDs:<ol><li>Click **Connect** to create the connection to the Adobe AEP endpoints.</li></ol>A **Connection Done** message will be displayed after your connection is successfully established.  |
| Identity Namespaces | This parameter indicates the context to which an identity relates, distinguishing different types of identity values, such as email addresses or numeric CRM IDs. When matching record data across profile fragments, Adobe Experience Platform uses the identity value and the namespace to merge profile data. Select the namespaces that you want to map.<br>If the parameter does not contain any identity namespaces, enter a dash (`-`). |
| Body parameters | Parameters associated with the XDM schema. Required attributes appear next to a lock icon and are read only. Provide a valid mapping in the drop-down list.<br>Note: The `identityMap` attribute requires that at least one of its namespaces has the property `primary` set to `true`. |
| Created At | A timestamp marking the creation of the connection. |
| Source Name | (Optional) A name for your source. If this value is missing, the streaming message automatically adds the source ID from the streaming connection definition. |
| Referer | Identifies the full URL of the page or resource from which the event originated. Used by AEP to associate the interaction with the correct referring context. The default value is the browser's Referer header, if available, or the corresponding data layer property. |
| X-Forwarded-For | Contains the originating IP address of the client connecting through Tealium or another proxy. Used by AEP for geolocation and attribution. The default value is taken from the IP address provided in the incoming request or the Tealium system variable representing the visitor's IP address. |
| X-Forwarded-Proto | Specifies the protocol (HTTP or HTTPS) that the client used to connect. Helps AEP interpret the original request scheme when routed through a proxy. The default value is `HTTPS`. |
| X-Forwarded-Host | Identifies the original host requested by the client, such as `www.clientsite.com`. Required by AEP to maintain accurate host attribution. |
| User-Agent | Provides the full user agent string identifying the client’s browser, operating system, and rendering engine. Used by AEP for device and browser detection. |
| Sec-CH-UA | (Required) Low-entropy Client Hint header listing the browser brands and versions. |
| Sec-CH-UA-Mobile | (Required) Indicates whether the client is on a mobile device. Required by AEP for mobile classification. |
| Sec-CH-UA-Platform | Identifies the platform on which the browser is running (for example, `Windows`, `macOS`, `Android`). |
| Sec-CH-UA-Platform-Version | Provides the version of the operating system platform. Used for advanced device and compatibility attribution. |
| Sec-CH-UA-Arch | Specifies the CPU architecture of the client device (for example, `x86`, `arm`). |
| Sec-CH-UA-Model | Identifies the device model. Primarily used for mobile devices. |
| Sec-CH-UA-Bitness | Indicates the bitness of the client architecture (for example, `64`). |
| Sec-CH-UA-WoW64 | Indicates whether the client is running a 32-bit process on a 64-bit Windows system. |
| Custom Header Key CSV | Provide a custom header key to send with the request. |
| Custom Header Value CSV | Provide a custom header value to send with the request. This value will correlate to the sequence of the custom header key. |
| Template Variables | Provide template variables as data input for Templates. Name nested template variables with the dot notation. For example, `items.name`. Nested template variables are typically built from data layer list attributes. <br> For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|
| Templates | Provide templates to be referenced in the Body parameters section. Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.<br>For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|

## Use cases

### Send analytics data to Adobe Analytics

To use the Adobe Experience Platform connector to send analytics data to Adobe Analytics, you first need to configure XDM schema, datastream, and services in Adobe Experience Platform. After you complete the Adobe configuration, you can then configure the connector in Tealium.

#### XDM schemas

When sending data to Adobe Experience Edge, you need to ensure it adheres to the Adobe XDM schemas. After Adobe Analytics receives the events, they are converted into more structured data, such as page views or link events, that can be easily managed. For more information about XDM data and Adobe Analytics, see [Implement Adobe Analytics with Adobe Experience Platform Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/overview.html?lang=en).

To ensure that page views and link events are handled properly, Adobe applies specific logic to the data before it's sent to the Adobe Experience Edge network. This logic ensures that the data is properly formatted, that any necessary transformations or aggregations are applied, and that the data conforms to the XDM schema. From there, it's forwarded to Adobe Analytics for processing and analysis.

The following table lists examples of data in an XDM payload and how Adobe Analytics will interpret the data based on the schema:

| **XDM payload data** | **Adobe Analytics interpretation** |
| --- | --- |
| `web.webPageDetails.name` or<br> `web.webPageDetails.URL` and no <br>`web.webInteraction.type` | Payload is considered a page view.|
|`web.webInteraction.type` and <br>(`web.webInteraction.name` or `web.webInteraction.url`) | Payload is considered a link event.|
|`web.webInteraction.type` and<br> (`web.webPageDetails.name` or `web.webPageDetails.url`)| Payload is considered a link event. `web.webPageDetails.name` and `web.webPageDetails.URL` are set to `null`.|
|no `web.webInteraction.type` and <br>(no `webPageDetails.name` and no `web.webPageDetails.URL`) | Payload is dropped and data is ignored.|

For a complete list of different variables that you can use to send data to Adobe Analytics, see [Analytics variable mapping in Adobe Experience Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en).

The following example shows how data for the variable `web.webPageDetails.name` and `experience` data is formatted when sent to Adobe Analytics:

```json
"xdm": {
  "web": {
    "webPageDetails": {
      "name": "Home Page"
    }
  },
  "_experience": {
    "analytics": {
      "customDimensions": {
        "props": {
          "prop1": "value1"
        },
        "eVars": {
          "eVar1": "value2"
        }
      }
    }
  }
}
```

#### Configure Adobe Experience Platform

1. In Adobe Experience Platform, go to **Data Management > Schemas** and click **Create Schema**.
1. In the **Schema Details** section, select the **Experience Event** option and then click **Next**.
1. Enter a name for the schema and click **Finish**.
1. In **Data Management > Schemas** select the schema that you just created.
1. In the schema details screen, go to the **Field groups** section and click **Add**. Select the **Adobe Analytics ExperienceEvent Template** and click **Save**.![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-schemas.png)
1. Go to **Data Collection > Datastreams** and select the datastream you want to use for data streaming and click the **Edit** button on the right side of the screen. If you do not already have a datastream configured, you can create a new one.
1. In your Datastream **Configure** screen, select the **Event Schema** you just created and click **Save**. ![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-datastreams.png)
1. In the **Datastreams** screen, click **Add Service** and select the **Adobe Analytics** option from the drop-down list and then click **Add Report Suite**. 
1. Enter the **Report Suite ID** from Adobe Analytics and click **Save**. You can find the report suite ID by navigating to **Adobe Analytics > Admin > Report Suites**. 

For more information about configuring Adobe Experience Platform Datastream, services, and schemas, see the following articles in the Adobe documentation:

* [Configure a Datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [Create and edit schemas in the UI](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Analytics settings](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#analytics)
* [Analytics field mappings](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html?lang=en)

#### Configure the Adobe Experience Platform connector in Tealium

1. Complete the configuration steps for the Adobe Experience Platform connector in the [Configure Settings](#configure-settings) section.
1. In the **Action** step, select the action you want to use.
1. Configure the actions with the following parameters:
    * **Datastream ID**: Select the datastream ID that you created previously.
    * **XDM Schema**: Select the XDM schema for the corresponding datastream. In Adobe Experience Platform, the datastream should already be linked to a single XDM schema. You should be able to see this schema in the drop-down list.
    * **Identity Namespaces**: Select the namespaces you want to map. When matching record data across profile fragments, Adobe Experience Platform uses the identity value and the namespace to merge profile data. If your XDM schema contains a map object, such as `identityMap`, you must select a namespace.
    * **XDM Schema Parameters**: Select attributes to associated with XDM schema parameters.
        * `_id`: A random unique ID that identifies an event. If you do not already have an specific attribute to map to this ID, use `tealium_random`.
        * `timestamp`: The UTC timestamp that represents the moment when the event took place. The expected format is `YYYY-MM-DDTHH:MM:SSZ`.
        * Add any additional attributes that need to be mapped. For a complete list of different variables that you can use to send data to Adobe Analytics, see [Analytics variable mapping in Adobe Experience Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en).
1. Click **Finish**.

The following image shows example mappings in Tealium:

![](https://docs.tealium.com/images/server-side-connectors/adobe-analytics-tealium-setup.png)

### Send audience data to Adobe Audience Manager

To use the Adobe Experience Platform connector to send audience data to Adobe Audience Manager, you first need to configure the XDM schema details in Adobe Experience Platform. After you complete the Adobe configuration, you can then configure the connector in Tealium.

For a full list of Adobe Audience Manager and XDM field mappings, see [Audience Manager field mappings](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/audience-manager.html?lang=en) in the Adobe documentation.

The following example shows how audience data is mapped to XDM schema when sent to Adobe Audience Manager.

```json
  "xdm": {
      "identityMap": {
        "ECID": {
          "_id": "12345"
        },
        "CORE": {
          "_id": "67890"
        }
      },
      "segmentMemberships": {
        "AAMTraits": ["trait1", "trait2"],
        "AAMSegments": ["segment1", "segment2"]
      },
      "profileStitch": [],
      "device": {
        "type": "desktop"
      },
      "placeContext": {
        "geo": {
          "countryCode": "US"
        }
      },
      "environment": {
        "browserDetails": {
          "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3"
        }
      }
  }
```
#### Configure Adobe Experience Platform

Adobe Audience Manager accepts two types of data: real-time and profile data, using Experience Event and Individual Profile schemas. The following example shows how to configure Adobe Experience Platform for an Experience Event use case. To use Individual Profile, complete the following steps but select the Individual Profile option in the step 2.

1. In Adobe Experience Platform, go to **Data Management > Schemas** and click **Create Schema**.
1. In the **Schema Details** section, select the **Experience Event** option for real-time data setup and then click **Next**.
1. Enter a name for the schema and click **Finish**.
1. In **Data Management > Schemas** select the schema that you just created.
1. In the schema details screen, go to the **Field groups** section, select the **Adobe Audience Manager Template**, and click **Save**.![](https://docs.tealium.com/images/server-side-connectors/adobe-audience-manager-schema.png)
1. Go to **Data Collection > Datastreams** and select the datastream you want to use for data streaming and click the **Edit** button on the right side of the screen. If you do not already have a datastream configured, you can create a new one.
1. In your Datastream **Configure** screen, select the **Event Schema** you just created and click **Save**. 
1. In the **Datastreams** screen, click **Add Service** and select the **Adobe Audience Manager** option from the drop-down list and click **Save**. 

For more information about configuring Adobe Experience Platform Datastream, services, and schemas, see the following articles in the Adobe documentation:

* [Configure a Datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [Create and edit schemas in the UI](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Audience Manager](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en)
* [Adobe Audience Manager field mappings](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/audience-manager.html?lang=en)

#### Configure the Adobe Experience Platform connector in Tealium 

To configure the connector to send data to Adobe Audience Manager, complete the steps in the [Configure the Adobe Experience Platform connector in Tealium](#configure-the-adobe-experience-platform-connector-in-tealium) section.

For more information about available data mappings in Adobe Audience Manager and their corresponding XDM fields, see [Audience Manager field mappings](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/audience-manager.html?lang=en) in the Adobe documentation.

### Send data to Adobe Target

To use the Adobe Experience Platform connector to send audience data to Adobe Target, you first need to configure the XDM schema details in Adobe Experience Platform. After you complete the Adobe configuration, you can then configure the connector in Tealium.

For a full list of Adobe Target and XDM field mappings, see [Audience Target field mappings](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/target.html?lang=en) in the Adobe documentation.

The following example shows how data is mapped to XDM schema when sent to Adobe Target.

```json
"xdm": {
        "channel": {
            "_id": "web"
        },
        "environment": {
            "browserDetails": {
                "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3"
            }
        },
        "_experience": {
            "target": {
                "clientCode": "adobetarget",
                "mboxName": "mbox1",
                "activities": [
                    {
                        "activityID": "12345"
                    }
                ]
            }
        },
        "device": {
            "type": "desktop"
        },
        "placeContext": {
            "geo": {
                "countryCode": "US"
            }
        },
        "commerce": {
            "order": {
                "priceTotal": 100.0
            }
        },
        "web": {
            "webReferrer": {
                "url": "https://www.example.com"
            }
        }
    }
}
```
#### Configure Adobe Experience Platform

1. In Adobe Experience Platform, go to **Data Management > Schemas** and click **Create Schema**.
1. In the **Schema Details** section, select the **Experience Event** option and then click **Next**.
1. Enter a name for the schema and click **Finish**.
1. In **Data Management > Schemas** select the schema that you just created.
1. In the schema details screen, go to the **Field groups** section and click **Add**. Select the **Adobe Target ExperienceEvent Template** and click **Save**.![](https://docs.tealium.com/images/server-side-connectors/adobe-target-schema.png)
1. Go to **Data Collection > Datastreams** and select the datastream you want to use for data streaming and click the **Edit** button on the right side of the screen. If you do not already have a datastream configured, you can create a new one.
1. In your Datastream **Configure** screen, select the **Event Schema** you just created and click **Save**. 
1. In the **Datastreams** screen, click **Add Service** and select the **Adobe Target** option from the drop-down list and click **Save**. 

For more information about configuring Adobe Experience Platform datastream, services, and schemas, see the following articles in the Adobe documentation:

* [Configure a Datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [Create and edit schemas in the UI](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Target](https://experienceleague.adobe.com/docs/target.html?lang=en)
* [Adobe Target field mappings](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/target.html?lang=en)

#### Configure the Adobe Experience Platform connector in Tealium 

To configure the connector to send data to Adobe Target, complete the steps in the [Configure the Adobe Experience Platform connector in Tealium](##configure-the-adobe-experience-platform-connector-in-tealium) section.

The following image shows example mappings in Tealium:

![](https://docs.tealium.com/images/server-side-connectors/adobe-target-tealium-setup.png)


### Send profiling data to Adobe Identity Service

To use the Adobe Experience Platform connector to send profiling data to Adobe Identity Service, you first need to configure the XDM schema details in Adobe Experience Platform. After you complete the Adobe configuration, you can then configure the connector in Tealium.

The following concepts can help you get started using the Identity Service within 
Adobe Experience Platform:

* **Identity**: Data that is unique to an entity, typically an individual person, such as a log-in ID, ECID, or loyalty ID.
* **Identity namespaces**: Distinguish the context or type of an identity. For example, an identity distinguishes `name@email.com` as an email address or `443522` as a numeric CRM ID. Identity namespaces are used to look up individual identities and provide the context for identity values. This lets you determine that two Profile fragments that contain different primary IDs, but share the same value for the email identity namespace, are the same individual.
* **Identity Graph**: A map of relationships between different identities, allowing you to visualize and better understand which customer identities are stitched together, and how. The graph is created automatically by the Identity Service and maps different identity namespaces, providing you with a visual representation of how your customers interact with your brand across different channels.
* **Experience Cloud ID (ECID)**: A shared identity namespace used across Adobe Experience Platform and Adobe Experience Cloud applications. ECID provides the foundation for customer identity and is used as the primary ID for devices and as a base node for identity graphs.

#### Merge policies

Adobe Experience Platform enables you to bring data fragments together from multiple sources and combine them to see a complete view of each of your individual customers. Merge policies are a set of rules that dictate how Adobe Experience Platform prioritizes data and determines which data to combine to create a unified view of a customer. 

Each profile fragment contains information for just one identity out of the total number of identities that could exist for an individual. When merging that data together to form a customer profile, there is the potential for that information to conflict and a priority must be specified.

Selecting a merge method lets you specify which dataset attributes to prioritize if a merge conflict occurs between datasets. There are two merge methods: Dataset Precedence and Timestamp Ordered. Dataset Precedence prioritizes fragments based on their dataset, while Timestamp Ordered prioritizes the most recent fragment.

Identity stitching is the process of identifying data fragments and combining them together to form a complete profile record. There are two methods to merge profiles for identity stitching: None and Private Graph. If you select **None**, a single customer may have multiple profiles that qualify for different audiences, resulting in several marketing messages. Selecting **Private Graph** stitches multiple identities related to the same individual together, resulting in a single profile and one marketing message. 

The following example shows how identity data is mapped to XDM schema when sent to Adobe Identity Service. The Adobe Identity Service will search for the profiles with the email address `myemail@example.com`. When it finds a matching profile, it will add the `myNEWemail@example.com` email address and `77828292900000` phone number. If the Identity Service cannot find a match, it will create a new profile with both email addresses and the phone number. 

```json
{
    "_id": "gjsadfghdfkyweiu2ydudyieds3wuyi2kadsjlksddrdesdhslksdwqe",
    "timestamp": "2023-11-17T02:59:57Z",
    "identityMap": {
        "Email": [
          {
            "id": "myemail@example.com",
            "primary": true
          }
        ]
      },
      "personalEmail": {
        "address": "myNEWemail@example.com"
      },
      "mobilePhone": {
        "number": "77828292900000"
      }
    }
}
```

For more information about configuring the Identity Service in Adobe Experience Platform, see the following articles in the Adobe documentation:

* [Identity Service Overview](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en)
* [Identity Namespace Overview](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
* [Merge Policies Overview](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html?lang=en) 
* [Adobe Data Collection](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/data-collection.html?lang=en)

#### Configure Adobe Experience Platform


<blockquote>
Updating customer data in Adobe Experience Platform may require stitching data from across Adobe products. For example, a profile may be created for an email campaign running in Adobe Journey Optimizer and then updated with different events sent through the Interactive Data Collection endpoint.
</blockquote>


1. In Adobe Experience Platform, go to **Data Management > Schemas** and select the schema you want to use or click **Create Schema** to create a new one.
    * New schema
        1. In the **Schema Details** section, select the **Experience Event** or **Individual Profile** option and then click **Next**.
        1. Enter a name for the schema and click **Finish**.
    * Existing schema
        1. In the schema details screen, go to the **Field groups** section and select **Personal Contact Details** and click **Save**.
        1. Add the profile attributes you want updated when you use this schema. For example, to add email address and phone number:
            * Expand the **personalEmail** property, click on **address**, and click the **Identity** checkbox in the **Field Properties** section on the right side of the schema screen.
            * Expand the **mobilePhone** property, click on **number**, and click the **Identity** checkbox in the **Field Properties** section on the right side of the schema screen.
1. Click **Save**.![](https://docs.tealium.com/images/server-side-connectors/adobe-identity-schema.png)
1. Go to **Data Management > Datasets**, and click **Create Dataset**.
1. Click **Create Dataset from Schema**, select your schema from the list, and click **Next**.
1. Enter a name for the dataset and click **Finish**.
1. Go to **Customer > Profiles**, select the **Merge Policies** tab, and click **Create merge policy**.
1. Enter a schema name. Leave the schema class as **XDM Individual Profile** and ID stitching as **Private Graph**. Click **Save**.
1. Go to **Connection > Sources**, search for **Adobe Data Collection**, and click **Set Up**. 

For more information, see [Adobe Data Collection](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/data-collection.html?lang=en).

#### Configure the Adobe Experience Platform connector in Tealium 

To configure the connector to send data to Adobe Identity Service, complete the steps in the [Configure the Adobe Experience Platform connector in Tealium](#configure-the-adobe-experience-platform-connector-in-tealium) section.

If you are using an Event Experience schema, create a **Send Event** action. If you are using an Individual Profile schema, you will need to create a **Stream Record Data** action.

The following image shows example mappings in Tealium:

![](https://docs.tealium.com/images/server-side-connectors/adobe-identity-service-tealium-setup.png)

#### Verify profile update in Adobe Experience Platform

To see an updated profile in Adobe Experience Platform, go to **Customer > Profiles**. To view all profile attributes, click the **Attributes** tab. 

## Debug an event call in Adobe Experience Platform

To debug an event call, go to **Connection > Sources** and click the **Dataflows** tab. 

Click the dataflow automatically created for your datastream and verify if records have failed. You may not see the dataflow yet if the event has not been processed.

If you find an error, click the **Dataflow Run Start** value to view the error details.
![](https://docs.tealium.com/images/server-side-connectors/adobe-dataflows-tab.png)

In this example, the event has not been processed because the timestamp is not in the correct format.
![](https://docs.tealium.com/images/server-side-connectors/adobe-dataflow-run-error.png)