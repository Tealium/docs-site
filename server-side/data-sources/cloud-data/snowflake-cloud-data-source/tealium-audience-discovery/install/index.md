---
title: Install Tealium Audience Discovery for Snowflake
description: Install Tealium Audience Discovery for Snowflake from the Snowflake Marketplace and configure the required roles and permissions.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/snowflake-cloud-data-source/tealium-audience-discovery/install/
---
This guide explains how to install Tealium Audience Discovery for Snowflake from the Snowflake Marketplace and configure the roles and permissions required to use it.

## Requirements

* A Snowflake account owner or administrator role.
* Access to the Snowflake databases and schemas you want to use for audience creation.

## Install the app

Install Tealium Audience Discovery for Snowflake from the Snowflake Marketplace. After installation, run the SQL in the following section to set up and launch the app.

## Set up the service

Run the following SQL after installation to configure and start the app. Replace `<SOURCE_DATABASE>` with the database containing your data. If you chose a different application name during installation, replace `TEALIUM_AUDIENCE_DISCOVERY_APP` accordingly.

1. Create an exclusive compute pool for the app.

   `CPU_X64_XS` (2 vCPU, 8 GB) is suitable for most workloads. Use `CPU_X64_S` (4 vCPU, 16 GB) for large audiences or heavy concurrent use.

   ```sql
   CREATE COMPUTE POOL IF NOT EXISTS TEALIUM_AUDIENCE_DISCOVERY_POOL
     FOR APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP
     MIN_NODES = 1
     MAX_NODES = 1
     INSTANCE_FAMILY = CPU_X64_XS;
   ```

1. Create a warehouse, or use an existing one.

   ```sql
   CREATE WAREHOUSE IF NOT EXISTS TEALIUM_AUDIENCE_DISCOVERY_WH
     WAREHOUSE_SIZE = 'X-SMALL';
   ```

1. Grant the app access to the compute pool and warehouse.

   ```sql
   GRANT USAGE ON COMPUTE POOL TEALIUM_AUDIENCE_DISCOVERY_POOL TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT USAGE ON WAREHOUSE TEALIUM_AUDIENCE_DISCOVERY_WH TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. Grant the app read access to your source data.

   ```sql
   GRANT USAGE ON DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT USAGE ON ALL SCHEMAS IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON ALL TABLES IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON ALL VIEWS IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. Start the service.

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.create_app_service(
       'TEALIUM_AUDIENCE_DISCOVERY_POOL',
       'TEALIUM_AUDIENCE_DISCOVERY_WH'
   );
   ```

1. Check the service status. Wait until the status returns `READY` before continuing.

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.check_service_status();
   ```

1. Get the application URL.

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.get_app_url();
   ```

## Open the app

1. Open the URL returned in step 7, or go to **Snowsight > Data Products > Apps > TEALIUM_AUDIENCE_DISCOVERY_APP > Endpoints**.
1. Click **audience-discovery-endpoint** to open the web interface.
1. Use the **Data Explorer** to browse available tables.

## Additional setup

### Grant access to additional databases

The app needs read access to every database you want to build audiences from. Repeat the following for each additional database.

```sql
GRANT USAGE ON DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
GRANT USAGE ON ALL SCHEMAS IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
GRANT SELECT ON ALL TABLES IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
GRANT SELECT ON ALL VIEWS IN DATABASE <SOURCE_DATABASE> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
```


<blockquote>
The app can only read source data. It never modifies your tables.
</blockquote>


### Enable Cortex AI (optional)

The app includes a Cortex mode that lets users describe audience segmentation rules in natural language. Cortex Analyst generates the SQL query automatically using your Snowflake semantic views.


<blockquote>
This feature requires a semantic view assigned to the application.
</blockquote>


1. Grant the Cortex AI database role.

   ```sql
   GRANT DATABASE ROLE SNOWFLAKE.CORTEX_USER TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. Grant access to your semantic views.

   ```sql
   GRANT USAGE ON DATABASE <SEMANTIC_VIEW_DB> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT USAGE ON SCHEMA <SEMANTIC_VIEW_DB>.<SEMANTIC_VIEW_SCHEMA> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON ALL VIEWS IN SCHEMA <SEMANTIC_VIEW_DB>.<SEMANTIC_VIEW_SCHEMA> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   GRANT SELECT ON SEMANTIC VIEW <SEMANTIC_VIEW_NAME> TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. (Optional) Configure available large language models (LLMs). Grant `app_admin` to your role to manage the model list.

   ```sql
   GRANT APPLICATION ROLE TEALIUM_AUDIENCE_DISCOVERY_APP.app_admin TO ROLE <ADMIN_ROLE>;
   ```

   View the default models seeded during installation.

   ```sql
   SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUDIENCE_DISCOVERY_SCHEMA.AVAILABLE_LLMS;
   ```

   Replace the list with your own models.

   ```sql
   DELETE FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUDIENCE_DISCOVERY_SCHEMA.AVAILABLE_LLMS;
   INSERT INTO TEALIUM_AUDIENCE_DISCOVERY_APP.AUDIENCE_DISCOVERY_SCHEMA.AVAILABLE_LLMS (MODEL_NAME)
   VALUES
       ('mistral-large2'),
       ('llama3.1-70b'),
       ('llama3.1-405b'),
       ('snowflake-arctic'),
       ('claude-3-5-sonnet');
   ```

   
<blockquote>
Only list models enabled in your Snowflake region. To test a model, run `SELECT AI_COMPLETE(model => '<model_name>', prompt => 'Hello');`
</blockquote>


### Enable webhook delivery (optional)

The app can send audience data to external HTTP endpoints. The app disables this feature by default and requires administrator setup.


<blockquote>
This feature requires a configured network rule and external access integration.
</blockquote>


1. Create a network rule for your webhook host.

   ```sql
   CREATE OR REPLACE NETWORK RULE webhook_egress_rule
     TYPE = HOST_PORT
     MODE = EGRESS
     VALUE_LIST = ('your-webhook-host.example.com:443');
   ```

1. Create an external access integration.

   ```sql
   CREATE OR REPLACE EXTERNAL ACCESS INTEGRATION webhook_external_access
     ALLOWED_NETWORK_RULES = (webhook_egress_rule)
     ENABLED = TRUE;
   ```

1. Grant the integration to the application.

   ```sql
   GRANT USAGE ON INTEGRATION webhook_external_access TO APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP;
   ```

1. Enable the feature. This automatically attaches the external access integration to the running service.

   ```sql
   -- Uses the default integration name WEBHOOK_EXTERNAL_ACCESS
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.set_webhook_enabled(TRUE);

   -- Or specify a custom integration name
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.set_webhook_enabled(TRUE, 'MY_CUSTOM_INTEGRATION');
   ```

   To disable webhook delivery later:

   ```sql
   CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.set_webhook_enabled(FALSE);
   ```

To send audience data:

1. Open an audience and click the three-dot menu.
1. Select **Send to Webhook**.
1. Enter the HTTPS webhook URL and, optionally, basic authentication credentials.
1. Click **Send**. Data is delivered as JSON in batches of 1,000 rows by default, up to 1,000,000 rows.

All deliveries are logged in `AUDIENCE_DISCOVERY_SCHEMA.WEBHOOK_LOG`.

```sql
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUDIENCE_DISCOVERY_SCHEMA.WEBHOOK_LOG
ORDER BY STARTED_AT DESC;
```

### Set up user access to the Tealium application

Grant Snowflake users access to the app by creating a dedicated role and assigning an application role to it.

1. Create a dedicated role for the application users.

   ```sql
   CREATE ROLE IF NOT EXISTS TEALIUM_APP_USER;
   ```

1. Grant the `app_user` application role to the dedicated role.

   ```sql
   GRANT APPLICATION ROLE TEALIUM_AUDIENCE_DISCOVERY_APP.app_user TO ROLE TEALIUM_APP_USER;
   ```

   Choose the application role that matches the user's needs:

      * `app_user`: access to the app with the ability to create audiences
      * `app_admin`: access to the app, ability to create audiences, change app configuration, and access app objects in Snowsight
      * `app_viewer`: access to the app without the ability to create audiences

1. Grant the dedicated role to the user who needs access to the app.

   ```sql
   GRANT ROLE TEALIUM_APP_USER TO USER <user>;
   ```

### Set up external access for the Tealium connector

Each audience includes a `USERS_EXTERNAL` secure view for external consumers such as the Tealium Snowflake connector. The view automatically returns zero rows when an audience is deactivated and resumes when re-activated.

1. Create a dedicated role for the external service account.

   ```sql
   CREATE ROLE IF NOT EXISTS TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE;
   ```

1. Grant the `app_external` application role. This role provides access to secure views only, not tables.

   ```sql
   GRANT APPLICATION ROLE TEALIUM_AUDIENCE_DISCOVERY_APP.app_external TO ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE;
   ```

1. Grant warehouse usage for query execution.

   ```sql
   GRANT USAGE ON WAREHOUSE TEALIUM_AUDIENCE_DISCOVERY_WH TO ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE;
   ```

1. Grant the role to the Tealium service account user.

   ```sql
   GRANT ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE TO USER <TEALIUM_SERVICE_USER>;
   ```

The Tealium connector queries audiences using:

```sql
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.<AUDIENCE_SCHEMA>.USERS_EXTERNAL;
```

To verify role restrictions, disable secondary roles before testing.

```sql
USE SECONDARY ROLES NONE;
USE ROLE TEALIUM_AUDIENCE_DISCOVERY_EXTERNAL_ROLE;

-- Should return data for an active audience
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUD_XXXXXXXXXXXXXXXX.USERS_EXTERNAL;

-- Should fail with insufficient privileges
SELECT * FROM TEALIUM_AUDIENCE_DISCOVERY_APP.AUD_XXXXXXXXXXXXXXXX.USERS;

-- Re-enable secondary roles when done
USE SECONDARY ROLES ALL;
USE ROLE SYSADMIN;
```

## Manage the service

Use the following stored procedures to manage the app service lifecycle. To create the service for the first time, see [Set up the service](#set-up-the-service). To recreate it after dropping, run the same SQL.

### Stop the service

Suspends the service without dropping it. Containers stop but the service definition is preserved.

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.stop_app_service();
```

### Resume the service

Resumes a previously suspended service.

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.resume_app_service();
```

### Refresh the service

Re-applies the service specification to pick up a new container image after an application upgrade.

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.refresh_app_service('TEALIUM_AUDIENCE_DISCOVERY_WH');
```

### Drop the service

Permanently removes the service. Use `create_app_service()` to recreate it.

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.drop_app_service();
```

### Check service status

```sql
CALL TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.check_service_status();
```

### View service logs

```sql
CALL SYSTEM$GET_SERVICE_LOGS('TEALIUM_AUDIENCE_DISCOVERY_APP.main_schema.audience_discovery_service', 0, 'audience-discovery-app', 100);
```

## Troubleshoot

| Issue | Resolution |
|---|---|
| Service not created yet | Run `create_app_service()` with your compute pool and warehouse. |
| Application requires an exclusive compute pool | The pool must be created with `FOR APPLICATION TEALIUM_AUDIENCE_DISCOVERY_APP`. |
| Compute pool does not exist or not authorized | Create the pool with `FOR APPLICATION` and grant `USAGE` to the app. |
| Cannot see source data | Grant `USAGE` and `SELECT` on the source database to the application. |
| Service status stuck on PENDING | Run `DESCRIBE COMPUTE POOL <pool>` and wait for the status to show `ACTIVE`. |
| Endpoint not accessible | Ensure `BIND SERVICE ENDPOINT` is granted and try refreshing Snowsight. |
| Can't access the application's URL | Ensure that your firewall [System Allowlist](https://docs.snowflake.com/en/sql-reference/functions/system_allowlist) does not block the app's ID at the front of the Snowflake URL. |
| Webhook delivery is not enabled | Run `CALL main_schema.set_webhook_enabled(TRUE)`. This also attaches the external access integration to the service. |
| Webhook connection error | Update the network rule `VALUE_LIST` to include the webhook host. |

## Security and data handling

### Data residency

All data remains within your Snowflake account. The app:

* Does not make external network requests by default. The only built-in HTTP call is to the Snowflake Cortex Analyst REST API on the same Snowflake infrastructure.
* Does not include telemetry, analytics, or automatic data egress.
* Does not use cookies.
* Does not store secrets in plain text. Authentication is handled through Snowflake's OAuth token mechanism in Snowpark Container Services (SPCS).
* Uses self-hosted fonts bundled into the container image at build time. No runtime requests are made to external servers.

When an administrator enables the optional webhook delivery feature with a network rule and external access integration, users can send audience data to a specified HTTPS endpoint. No outbound requests occur unless the administrator enables this feature and a user initiates a send.

### Authentication

All access requires Snowflake authentication. The web UI is served through a Snowflake ingress endpoint. There are no public unauthenticated endpoints.

### Objects created

The app creates the following objects in your Snowflake account.

**Schemas:**

* `MAIN_SCHEMA`: infrastructure
* `AUDIENCE_DISCOVERY_SCHEMA`: metadata
* `TEALIUM_EXTERNAL_ACCESS`: secure views for external access
* One `AUD_*` schema per audience

**Tables:**

* `AUDIENCES`: audience metadata
* `AVAILABLE_LLMS`: LLM configuration
* `WEBHOOK_CONFIG`: feature flag
* `WEBHOOK_LOG`: webhook delivery audit log
* One `USERS` table per audience

**Views:**

* One `USERS_EXTERNAL` secure view per audience. Returns zero rows when the audience is deactivated and resumes when re-activated.

**Procedures:** Service management and owner-privilege DDL executors for audience lifecycle.

**Tasks:** One `REFRESH_TASK` per active audience for scheduled refreshes.

**Service:** `audience_discovery_service` running the containerized application.

### Data retention

Audience metadata including name, description, configuration, user counts, and timestamps is stored in the `AUDIENCES` table indefinitely. Each audience version is preserved as a separate row for historical tracking. Deleting an audience removes all associated data, including metadata rows and the audience schema.