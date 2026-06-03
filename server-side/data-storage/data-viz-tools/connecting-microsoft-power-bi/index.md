---
title: Connecting Microsoft Power BI
description: This article describes how to connect Microsoft Power BI to Tealium DataAccess
url: https://docs.tealium.com/server-side/data-storage/data-viz-tools/connecting-microsoft-power-bi/
---### Create ODBC data source

To connect Power BI to DataAccess, an ODBC Data Source connection is required.

To create an ODBC data source in Power BI:

1. [Install the Amazon Redshift Driver for Windows](http://docs.aws.amazon.com/redshift/latest/mgmt/install-odbc-driver-windows.html#odbc-driver-windows-how-to-install)
1. [Create a system DSN entry for an ODBC connection](http://docs.aws.amazon.com/redshift/latest/mgmt/install-odbc-driver-windows.html#create-dsn-odbc-windows)
    * Be sure to use `System DSN`
1. Your configurations should resemble the following:  
      ![](/images/server-side/example-odbc-setup.png)
1. After the ODBC Data Source has been configured, click **Test**. If the client computer can connect to the Amazon Redshift database, you will see the following message: **Connection successful**.
1. Close the ODBC configurations.

### Connect Microsoft Power BI to Tealium DataAccess

1. Within Power BI, select the **Home** tab then **Get Data** (click the icon, not the drop-down)
1. Select **Other**, then **ODBC**, then click **Connect**.  
      ![](/images/server-side/get-data.png)
1. Select your Data source name from the drop-down.  
      ![](/images/server-side/from-odbc.png)
1. If you retrieve the entire database, you may not be able to successfully run queries after you are connected. We recommend that you click **Advanced options** and enter a limiting statement in the SQL statement (Optional) field so that you retrieve only the data you need. It should resemble the following:  
      ![](/images/server-side/power-bi-limiting-query.png)
1. Click **OK**. A data Navigator will appear.
1. Expand the directory structure and select the table you want to query then click **Load**.  
      ![](/images/server-side/data-navigator.png)
1. Power BI will connect to the data, load the data for modeling, and populate the columns with your attributes.  
      ![](/images/server-side/data-fields-aka-attributes.png)

Now you are ready to build reports using Microsoft Power BI on top of Tealium DataAccess.

### Troubleshooting

&#34;Server certificate for &amp;lt;cluster name&amp;gt; does not match host name.&#34;

First, try to use the full cluster name in the connection settings. If that does not resolve the error, try changing the **sslmode** setting to `verify-ca` rather than `verify-full`. Learn more about [Redshift SSL Support](https://docs.aws.amazon.com/redshift/latest/mgmt/connecting-ssl-support.html).
