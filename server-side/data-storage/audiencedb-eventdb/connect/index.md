---
title: Connect to EventDB and AudienceDB
description: This article describes provides information on connecting to Redshift, getting database credentials, and writing SQL queries.
url: https://docs.tealium.com/server-side/data-storage/audiencedb-eventdb/connect/
---
## Connect to Redshift

To access to your EventDB and AudienceDB data, a third-party tool with the ability to connect to a PostgreSQL-style database is required.

* **First Time Users**
After EventDB and AudienceDB are enabled for your account, Redshift Spectrum is automatically enabled.
* **Existing Customers** 
Before enabling Spectrum for existing customers that have been using DataAccess, a data migration is needed to ensure all existing and new data are written to the correct location. Coordinate with your team in advance to proceed.  

## Get database credentials

Third-party tools with PostgreSQL support require authentication credentials to connect. Authentication credentials are provided in the DataAccess Console.

Database Credentials are now generated for each user. Previously, all users shared the credentials generated for an account and profile. If someone regenerated global credentials, all user connections were terminated, and all users had to reconnect.

For user-specific credentials, the generated credentials are based on the account, profile, and the user&#39;s email address. Users can regenerate their own credentials without terminating other connections. You can remove access for a specific user without terminating other connections. To deactivate a specific user&#39;s credentials, contact Tealium Support.

Previously-generated global credentials can still be used, but cannot be regenerated.

Use the following steps to get database authentication credentials:

1. Navigate to **Store &gt; EventDB** or **Store &gt; AudienceDB**.
1. Click **Get DB Connection Details**.
1. Click **Regenerate DB Credentials**.  
You need to regenerate credentials even if this is your first time getting credentials.  
      ![](/images/server-side/connection-details.png)
1. Click **Yes** to confirm that you want to delete your existing credentials and generate new ones.  
The **DB Connection Details** screen displays the following fields:
    * **Username**  
    The username for the database connection, which is a combination of your account, profile names, and your email address. For example, `account__profile__email`.
    * **Password**  
    The password for the database connection.
    * **Database**  
    The name of the database, usually the name of your account.
    * **Host**  
    The host name of the database server, specific to your data storage region.
    * **Port**  
    The port number for the connection.
1. Save the connection details for future use, then click **Close**.

### Browse the Redshift database

After you have your database authentication credentials, you can connect to the database using a third-party tool. The following example uses SQL Workbench/J, which is a freeware application (see [Connecting to EventDB with SQL Workbench]()). The schema naming convention is `account__profile`.

The example below shows a view that joins all the related tables and columns.

![](/images/server-side/sql-workbench-db-explorer.jpg)

This example shows a raw data table view. The column names are in the same positions in each table, regardless of the view. The main difference between these two views is the readability of the entry.

![](/images/server-side/sql-workbench-columns.jpg)

## Writing SQL queries

The following articles provide best practices and examples of useful queries:

* [Connecting to EventDB and AudienceDB with SQL Workbench/J]()
* [Best Practices for Writing Queries for EventDB and AudienceDB](https://support.tealiumiq.com/en/support/solutions/articles/36000363364-best-practices-for-writing-queries-for-eventdb-and-audiencedb/preview)
* [Helpful SQL Queries for EventDB and AudienceDB](https://support.tealiumiq.com/en/support/solutions/articles/36000363427-helpful-sql-queries-for-eventdb-and-audiencedb)

