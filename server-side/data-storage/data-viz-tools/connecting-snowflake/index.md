---
title: Connecting Snowflake
description: This article describes how to load Tealium data into Snowflake using the Snowflake web interface.
url: https://docs.tealium.com/server-side/data-storage/data-viz-tools/connecting-snowflake/
---
This article focuses on the Snowflake web interface and Data Load wizard and provides an overview of Snowflake command line tools. For more detailed information about using Snowflake, see the [Snowflake Documentation](https://docs.snowflake.net/manuals/index.html).

## How it works

Tealium DataAccess customers can use the Snowflake web interface to connect their data to an external solution for advanced querying and data analysis. The web interface provides an intuitive wizard that you can use to load limited amounts of data into a table from a small set of flat files. To do this, the wizard uses the PUT and COPY commands to load data and then simplifies the data loading process by combining the staging files and loading data phases into one single operation.

The web interface is intended for loading small numbers of files (up to 50 MB). This limitation ensures optimal performance due to the fact that browser performance can vary between hardware, browser types, and browser versions.

## Prerequisites

The following items are required to connect your DataAccess data from the Tealium-issued Amazon S3 bucket:

* Tealium DataAccess with AudienceStore and EventStore enabled  
You must configure the AudienceStore connector within AudienceStream in order for data to be delivered to your DataAccess bucket. For additional information about AudienceStream configuration, see the Tealium [AudienceStore Setup Guide]().
* Valid Tealium DataAccess credentials for either EventStore and/or AudienceStore.

## Getting started

The following sections guide you through the steps required use the Snowflake Data Load web interface to select source files and load Tealium data into Snowflake.

We recommend loading DataAccess data to a table with a variant data type, which accommodates the semi-structured nature of JSON files without enforcing schema requirements. See the Best Practices section in this document for additional information and tips on parsing the data after it has loaded.

### Open the data load wizard

Use the following steps to open the Snowflake Data Load wizard:

1. Log in to your Snowflake account.
1. Click **Databases &gt; Tables**.
1. Do one of the following:  
      * Click a table row to select it and then click the **Load Data** button.
      * Click a table name to open the table details page, and then click the **Load Table** button.

1. The Load Data wizard displays.
1. Proceed to the next section to select your source files from DataAccess, which will enable you to begin loading data into the table you selected.

### Select source files from DataAccess

When prompted to select source files, you will create a new stage for your Tealium DataAccess data that resides in AWS S3.

Use the following steps to select source files from Tealium DataAccess:

1. Select **Existing Amazon S3 Location**.
1. Click **Next**.  
      ![](/images/server-side/snowflake-create-stage.jpg)
1. Proceed to the next section to enter your DataAccess credentials.

### Enter your DataAccess credentials

Use the following steps to enter your DataAccess credentials:

1. Retrieve your DataAccess credentials for EventStore or AudienceStore if you have not done so already.  
The credentials are the same for both EventStore and AudienceStore.  
      If your credentials have already been generated, your Secret Access Key does not display. Work with your colleagues to retrieve the existing key or to determine if a new one should be regenerated.

1. Once you have your valid credentials, enter them into the following fields:  
    * **Access Key**  
    Enter the Access Key ID provided by Tealium, for example: `AKIA****************`
    * **Secret Key**  
    Enter the Secret Access Key provided by Tealium.
    * **Bucket**  
    Enter only the first value from the path field in Tealium, for example:  
    If your Tealium Path is: `/dataaccess-us-east-1.tealiumiq.com/myaccount/main`  
    Enter : `dataaccess-us-east-1.tealiumiq.com` (without slashes).
    * **Prefix**  
    Enter the remaining part of the path field from Tealium, starting with the account name and ending with a trailing slash (/).  
    Example: `myaccount/main/`
    * **Region**  
    Select the region indicated by your bucket name, for example **us-east-1**.

1. Proceed to the next section to create a file format.

### Create a file format

Use the following steps to create a file format:

1. Click the plus (**&#43;**) symbol next to the drop-down list.  
The Create File Format dialog displays.  
      ![](/images/server-side/snowflake-create-file-format.jpg)
1. Enter the following information:
    * In the Name field, enter a name for the file format you will use for your DataAccess data, for example: `TEALIUM_JSON`.  
    This is a required field.
    * Select a Schema Name type from the drop-down list, for example: **Public**.
    * Select a Format Type from the drop-down list, for example: **JSON**.
    * Select a Compression Method ;from the drop-down list, for example: **Gzip**.
    * Select one or more of the following checkboxes:
        * Enable Octal
        * Allow Duplicate
        * Strip Outer Array
        * Strip Null Values
        * Ignore UTF-8 Errors
    * In the Comment field, enter descriptive comments about this file format.  
    Example: Tealium stores JSON data in Gzip compressed files.

1. Click **Finish**.
1. Proceed to the next section to load your data.

### Load data

Use the following steps to continue manually loading data using the web interface, continue reading the steps below. You can optionally load data from the command line. If you select this method, skip to the Load Using Command Line section.

1. Select your previously named file format from the drop-down list.  
      ![](/images/server-side/snowflake-manually-load-data-via-web-interface.jpg)
1. Click **Load** to immediately load data or click **Next** to configure additional load options.  
If the warehouse is not currently running, resuming the warehouse could take up to 5 minutes, in addition to the time required for loading.

### Load using command line (Optional)

Use the following steps to load your data from the command line:

1. **Install SnowSQL**  
Before you can load data from command line, you must install SnowSQL on your machine. Learn more about [installing SnowSQL](https://docs.snowflake.com/en/user-guide/snowsql-install-config.html).
1. **Configure Snow SQL**  
After completing the SnowSQL installation, you must edit your configuration file with your credentials to be able to connect to your Snowflake instance.
    1. Open your configuration file located in the following directory:  
        * For Linux/Mac OS:`~/.snowsql/`
        * For Windows: `%USERPROFILE%\.snowsql\`
    1. Edit the file by modifying the connections section to input your credentials.  
    Example:  
          ```bash
          [connections.tealium_example]
          #Can be used in SnowSql as connect tealium_example
          accountname = MY_ACCOUNT_NAME
          username = MYUSER
          password = ********************
          ```
    1. Modify the options or variables sections as you prefer. Learn more: [Configuring SnowSQL](https://docs.snowflake.com/en/user-guide/snowsql-config.html).

1. **Connect through SnowSQL**  
Once your connection details are saved in your configuration file, connect to SnowSQL using a shell command. Replace `tealium_example` with your connection name:  
`$ snowsql -c tealium_example`  
Learn more: [Connecting Through SnowSQL](https://docs.snowflake.com/en/user-guide/snowsql-start.html).
1. **Load Data Using the COPY INTO Command**  
Once you are connected, execute a `COPY INTO &lt;table&gt;` command to load your data into the target table. The following example loads data from files in the named stage `my_dataaccess_stage` which was created in the previous steps.  
Using appended pathing, the statement only loads files located in the events subdirectory:
      ```
      COPY INTO mytable
      FROM ‘@my_dataaccess_stage/events/’
      FILE_FORMAT ‘TEALIUM_JSON’;
      ```

## Best practices

This section provides helpful information about best practices for parsing data after the data is loaded.

### Parse EventStore data

EventStore is formatted in a flattened JSON file. If you followed the data loading steps described in this document, your EventStore data should now be structured in your variant type column. To format the data into a more usable structure for querying, you must parse the JSON.

The following sample query defines all default EventStore attributes columns into dedicated columns of a database view:

```sql
CREATE OR REPLACE VIEW TEALIUM_STD_EVENTS AS
  SELECT
      JSON:&#34;visitorid&#34;::string                              as visitorid
  ,   JSON:&#34;eventid&#34;::string                                as eventid
  ,   JSON:&#34;useragent&#34;::string                              as useragent
  ,   JSON:&#34;device_type&#34;::string                            as device_type
  ,   JSON:&#34;eventtime&#34;::number                              as eventtime

  ,   JSON:&#34;dom_domain&#34;::string                             as dom_domain
  ,   JSON:&#34;dom_pathname&#34;::string                           as dom_pathname
  ,   JSON:&#34;dom_query_string&#34;::string                       as dom_query_string
  ,   JSON:&#34;dom_title&#34;::string                              as dom_title
  ,   JSON:&#34;dom_url&#34;::string                                as dom_url
  ,   JSON:&#34;dom_viewport_height&#34;::number                    as dom_viewport_height
  ,   JSON:&#34;dom_viewport_width&#34;::number                     as dom_viewport_width

  ,   JSON:&#34;pageurl_domain&#34;::string                         as pageurl_domain
  ,   JSON:&#34;pageurl_full_url&#34;::string                       as pageurl_full_url
  ,   JSON:&#34;pageurl_path&#34;::string                           as pageurl_path
  ,   JSON:&#34;pageurl_querystring&#34;::string                    as pageurl_querystring
  ,   JSON:&#34;pageurl_scheme&#34;::string                         as pageurl_scheme

  ,   JSON:&#34;referrerurl_domain&#34;::string                     as referrerurl_domain
  ,   JSON:&#34;referrerurl_full_url&#34;::string                   as referrerurl_full_url
  ,   JSON:&#34;referrerurl_path&#34;::string                       as referrerurl_path
  ,   JSON:&#34;referrerurl_querystring&#34;::string                as referrerurl_querystring
  ,   JSON:&#34;referrerurl_scheme&#34;::string                     as referrerurl_scheme

  ,   JSON:&#34;udo_ut_account&#34;::string                         as udo_ut_account
  ,   JSON:&#34;udo_ut_domain&#34;::string                          as udo_ut_domain
  ,   JSON:&#34;udo_ut_env&#34;::string                             as udo_ut_env
  ,   JSON:&#34;udo_ut_event&#34;::string                           as udo_ut_event
  ,   JSON:&#34;udo_ut_profile&#34;::string                         as udo_ut_profile
  ,   JSON:&#34;udo_ut_version&#34;::string                         as udo_ut_version

  ,   JSON:&#34;firstpartycookies_utag_main__pn&#34;::number        as cookie_utag_main__page_number
  ,   JSON:&#34;firstpartycookies_utag_main__sn&#34;::number        as cookie_utag_main__session_number
  ,   JSON:&#34;firstpartycookies_utag_main__ss&#34;::number        as cookie_utag_main__session_start_flag
  ,   JSON:&#34;firstpartycookies_utag_main__st&#34;::number        as cookie_utag_main__sessoin_timeout
  ,   JSON:&#34;firstpartycookies_utag_main_ses_id&#34;::number     as cookie_utag_main__session_id

  ,   JSON:&#34;udo_timing_pathname&#34;::string                    as timing_pathname
  ,   JSON:&#34;udo_timing_dns&#34;::number                         as timing_dns
  ,   JSON:&#34;udo_timing_load&#34;::number                        as timing_load
  ,   JSON:&#34;udo_timing_connect&#34;::number                     as timing_connect
  ,   JSON:&#34;udo_timing_response&#34;::number                    as timing_response
  ,   JSON:&#34;udo_timing_dom_interactive_to_complete&#34;::number as timing_dom_interactive_to_complete
  ,   JSON:&#34;udo_timing_front_end&#34;::number                   as timing_front_end
  ,   JSON:&#34;udo_timing_dom_loading_to_interactive&#34;::number  as timing_dom_loading_to_interactive
  ,   JSON:&#34;udo_timing_query_string&#34;::string                as timing_query_string
  ,   JSON:&#34;udo_timing_domain&#34;::string                      as timing_domain
  ,   JSON:&#34;udo_timing_fetch_to_interactive&#34;::              as timing_fetch_to_interactive
  ,   JSON:&#34;udo_timing_timestamp&#34;::number                   as timing_timestamp
  ,   JSON:&#34;udo_timing_fetch_to_complete&#34;::number           as timing_fetch_to_complete
  ,   JSON:&#34;udo_timing_fetch_to_response&#34;::number           as timing_fetch_to_response
  ,   JSON:&#34;udo_timing_time_to_first_byte&#34;::number          as timing_time_to_first_byte

  FROM EVENTSTORE_SAMPLE;
```

For detailed information about these fields, see the [EventStore Data Guide]().

### Parse AudienceStore data

AudienceStore data can have several variations, each depending on the configuration of the connector actions. In the previous setup steps, you defined your file format for the Snowflake stage as JSON.

You can use the following sample query to create a view containing all default visitor badges, dates, strings, numbers and Booleans.

```sql
CREATE OR REPLACE VIEW TEALIUM_STD_VISITORS AS
SELECT

JSON:_id::string as &#34;visitor_id&#34;
, JSON:metrics.&#34;Average visit duration in minutes&#34;::number as &#34;avg_visit_duration&#34;
, JSON:metrics.&#34;Average visits per week&#34;::number as &#34;avg_visits_per_week&#34;
, JSON:metrics.&#34;Lifetime event count&#34;::number as &#34;ltm_event_count&#34;
, JSON:metrics.&#34;Lifetime visit count&#34;::number as &#34;ltm_visit_count&#34;
, JSON:metrics.&#34;Total direct visits&#34;::number as &#34;total_direct_visits&#34;
, JSON:metrics.&#34;Total referred visits&#34;::number as &#34;total_referred_visits&#34;
, JSON:metrics.&#34;Total time spent on site in minutes&#34;::number as &#34;total_time_onsite&#34;
, JSON:metrics.&#34;Weeks since first visit&#34;::number as &#34;weeks_since_first_visit&#34;
, JSON:dates.&#34;First visit&#34;::number as &#34;first_visit_date&#34;
, JSON:dates.&#34;Last visit&#34;::number as &#34;last_visit_date&#34;
, JSON:properties.&#34;Last event url&#34;::string as &#34;last_event_url&#34;
, JSON:properties.&#34;Lifetime browser types used (favorite)&#34;::string as &#34;ltm_browser_types_used_fav&#34;
, JSON:properties.&#34;Lifetime browser versions used (favorite)&#34;::string as &#34;ltm_browser_versions_used_fav&#34;
, JSON:properties.&#34;Lifetime devices used (favorite)&#34;::string as &#34;ltm_devices_used_fav&#34;
, JSON:properties.&#34;Lifetime operating systems used (favorite)&#34;::string as &#34;ltm_os_used_fav&#34;
, JSON:properties.&#34;Lifetime platforms used (favorite)&#34;::string as &#34;ltm_platforms_used_fav&#34;
, JSON:badges.&#34;Fan&#34;::boolean as &#34;fan_badge&#34;
, JSON:badges.&#34;Frequent visitor&#34;::boolean as &#34;frequent_visitor_badge&#34;
, JSON:badges.&#34;Unbadged&#34;::boolean as &#34;unbadged&#34;
, .&#34;Returning visitor&#34;::boolean as &#34;returning_visitor_flag&#34;

FROM AUDIENCESTORE_SAMPLE;

```

For more advanced parsing of the visitor profile object, see the [Snowflake Semi-structured Data](https://docs.snowflake.com/en/user-guide/semistructured-concepts.html) documentation.

## Related topics

See the following resources for additional information:

* [Working with AudienceStore and EventStore - Tealium ]()
* [EventStore Data Guide - Tealium]()
* [Preparing to Load Data - Snowflake](https://docs.snowflake.com/en/user-guide/data-load-prepare.html)
* [Data Loading Considerations - Snowflake](https://docs.snowflake.com/en/user-guide/data-load-considerations.html)
