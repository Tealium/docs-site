---
title: Connecting SQL Workbench/J
description: This guide describes how to download and install SQL Workbench/J and connect to the database associated with your DataAccess account.
url: https://docs.tealium.com/server-side/data-storage/data-viz-tools/connecting-sql-workbench/
---
SQL Workbench/J is a free query tool that is simple to use and can connect to many database management systems (DBMS), such as PostgreSQL or MySQL. Use SQL Workbench/J as a quick and easy way to connect to your database, view your database schema, and analyze your data.

## Install and setup

### Download and install

The following steps describe how to download SQL Workbench and the Amazon Redshift JDBC driver:

1. Download and install [SQL Workbench](http://www.sql-workbench.net/getting-started.html).
1. Download and install the [Amazon Redshift JDBC driver](https://docs.aws.amazon.com/redshift/latest/mgmt/jdbc20-install-driver.html).
1. Save the `.jar` file to a safe location on your computer.
Deleting this file will cause connections to break.

### Build the driver

The driver for Amazon Redshift JDBC must be installed in SQL Workbench before you can connect to the database.
The following steps describe how to install the Amazon Redshift JDBC driver:

1.  Open **SQL Workbench/J**.
2.  Click **Manage Drivers** in the lower left of the screen.
3.  Click the **Create a new entry** icon.  
![](/images/server-side/sql-workbench-create-driver.jpg)
4.  In the **Name** field, enter `Redshift`.
5.  Click the **folder** icon to the right of the Library text area.  
![](/images/server-side/sql-workbench-folder.jpg)
6.  Navigate to the location of the driver, click to select it, and then click **Open**.  
The **Classname** field is now set to `com.amazon.redshift.jdbc_41_.Driver` where `41` indicates the driver version.
7.  Click **OK** to exit.  
Your Redshift database is now configured.

### Create a Connection Profile

The following steps describe how to create a connection profile by providing SQL Workbench with the connection credentials to your Tealium database:

1.  In the **SQL Workbench/J** interface, click the **Create a new connection profile** icon.  
![](/images/server-side/sql-workbench-connection-profile.jpg)
2.  Enter a name your new profile. For example, a name that combines your Tealium account and profile, such as `mycompany-main`.
3.  In the **Driver** drop-down list, select `Amazon Redshift JDBC Driver (com.amazon.redshift.jdbc41.Driver)`.  
  ![](/images/server-side/sql-workbench-connection-profile.jpg)
4.  In your Tealium account, navigate to **Store &gt; EventDB** or **Store &gt; AudienceDB**.
5.  Click **Get DB Connection Details**.  
  The **DB Connection Detail** dialog displays. Keep this window open as you proceed. In the following example, credentials are removed for confidentiality.  
    ![](/images/server-side/sql-workbench-connection-details.jpg)
6.  Return to SQL Workbench and enter a URL based on the following example, where `HOST`, `PORT`, and `DATABASE` are replaced with the connection values from DataAccess: `jdbc:redshift://HOST:PORT/DATABASE?ssl=true`.  
    ![](/images/server-side/sql-workbench-connection-url.jpg)
7.  Use your credentials to enter your **Username** and **Password**.
8.  Check the **Autocommit** checkbox.  
      ![](/images/server-side/sql-workbench-connection-autocommit.jpg)
9.  Click the **Save Profile List** icon to save.  
        ![](/images/server-side/sql-workbench-connection-save.jpg)
10.  Click **OK** to attempt to connect.  

If successful, the **Statement** page displays. From here, you can begin writing scripts to query the data.  

If you have recently enabled EventDB or AudienceDB, it may take up to an hour for data to become available.

### Troubleshooting

The following sections provide information about common errors and troubleshooting tips.

#### Common Errors
*   **Deleting the Redshift JAR file**  
  If the Redshift JAR file is deleted, connections will break. Be sure to save it to a safe location such as your home folder.
*   **Mixing the username and database name**
    *   The username contains your `account_profile`.
    *   The database is your Tealium account name.
*   **Not checking the Autocommit checkbox**  
  If you do not check the **Autocommit** checkbox prior to saving, only one query can be made per connection instance.

#### Tips
*   **Show password**  
  If you need to view your password, click **Show password** next to the Password input field in SQLWorkbench/J.  
  ![](/images/server-side/sql-workbench-show-password.jpg)
*   **Enable an event feed for EventDB**  
  For EventDB, you must enable an event feed to be sent to EventDB. For additional information, see [event feeds]().
*   **Enable attributes for AudienceDB**  
  For AudienceDB, you must enable attributes to be sent to AudienceDB. For additional information, see [Adding Attributes to AudienceDB]().
    *   If you do not complete the above steps, you will see many `visit_` and `visitor_` tables and views that contain only basic visitor-level data and Audiences. No attribute data will be included.
    *   There is a soft limit of 250 attributes in AudienceDB. After this number is reached, you may experience performance degradation.


## Using SQL Workbench

After you create your connection profile for SQL Workbench/J, you are ready to start querying data. Follow this document to get started. First, learn your data column names and what your tables and list schema represent.

For additional questions regarding connection and data schema support, contact your Tealium account manager. If you need additional help regarding query support, data export, or integration into Business Intelligence (BI) tools, reach out to a member of your team, such as a data scientist or database administrator.

The following sections provide general information about the most commonly used screens in the SQL Workbench/J interface.

### Statements

From the SQL Workbench/J interface, click the **Statements** tab to write SQL statements and view results or error messages.

![](/images/server-side/whiteui-dataaccess-running-queries-on-audiencedb-event-db-using-sql-workbench:j-statement-editor.jpg)

### Database explorer

From the SQL Workbench/J interface, go to **Database Explorer** to review your available data.

![](/images/server-side/whiteui-dataaccess-running-queries-on-audiencedb-eventdb-using-sql-workbenchj.jpg)

The left panel displays the tables and views that are accessible within your Redshift instance. Each table or view contains different pieces of data. To build your query correctly, you must know the column names that are available to be queried, such as `udo_job_role`. The right pane helps you navigate the data column names and build your queries.

* **Table**  
A table is a standard method of storing data in a database. The number of tables depends on the number of filtered streams enabled for EventDB and AudienceDB.
* **View**  
For each table, there is a corresponding view. A view provides a more human-readable version of the table columns.
* **Examples**
    * A table displays `tags_main_1_executed` whereas a view displays `event - tags - tealium collect (main 1) - executed`.
    * A table displays `udo_job_role` whereas a view displays `event - udo - job_role`.
* **Using with EventDB**
    * The `events__all_events` table holds all events by default.
    * Each filtered stream then has a table, such as `events__f84fc357_4ded_413d_d28a_de70624ff2d5`.
* **Using with AudienceDB**
    * `visit_lists` contains the current visit-scoped list attributes for querying.
    * `visit_tallies` contains the current visit-scoped tally attributes for querying.
    * `visitor_lists` contains the visitor-scoped list attributes for querying.
    * `visitor_tallies` contains the visitor-scoped tally attributes for querying.
    * `visitor_replaces` contains visitor profiles that have been stitched.
    * `visitors` is the most commonly-used table and contains the latest visitor-scoped data for each visitor and any audiences that they belong to.
    * `visits` contains the latest current visitor-scoped data for each visitor.
* **Limitations**
    * [Funnel]() and [timeline]() attributes are not supported.

### View column names

Click the **Objects** tab to view the column names for each table or view. You can use the available filters in the interface to fine-tune your results. By default, `COLUMN_NAME` is not in alphabetical order. Click the header row to sort the names alphabetically.

![](/images/server-side/whiteui-dataaccess-running-queries-on-audencedb-eventdb-using-sql-workbenchj-search-tables-objects-tab.jpg)

### View random sample data

Click the **Search table data** tab to view random samples of data. You can use the available filters in the interface to fine-tune your results.

![](/images/server-side/whiteui-dataaccess-running-queries-on-audencedb-eventdb-using-sql-workbenchj-search-table-data.jpg)

### Common errors to avoid

The following items are noted as common errors to avoid:

* Not declaring UDO variables within `utag_data` in your iQ Tag Management (TiQ) data layer. If the variables are not declared, they will not display in EventDB.
* Not enabling an AudienceStream attribute to be sent to AudienceDB. Each attribute must be manually selected. There is a soft limit of 250 attributes. If more columns are needed, contact your Tealium account manager.
