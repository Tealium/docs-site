---
title: File import configuration
description: This article describes how to configure your file import data source.
url: https://docs.tealium.com/server-side/data-sources/file-import/configuration/
---

<blockquote>
Before you begin, create a sample CSV file (less than 1,000 columns) to upload during the setup process. This sample file is used to automatically detect the column mappings.
</blockquote>



<blockquote>
To be successfully imported, the CSV files must be formatted correctly. For information on the file format, see [Prepare a CSV file for import](https://docs.tealium.com/prepare-a-csv-file-for-import/).
</blockquote>


## 1. Add a file import data source

  1. Navigate to **Connect > Data Sources**.
  1. Click **+ Add Data Source**.
  1. Under **Categories**, click **File Import** and select the **File Import** platform.
  1. In the **Name** field, enter a unique name related to the file type.
  1. Click **Continue**.

## 2. Upload a sample file (Optional)

If you are using a sample CSV file in your file import configuration, upload it on the **Upload Sample File** screen. Column names in row 1 of the sample file are automatically detected and used to preconfigure entries in the **Column Mappings** screen. 

To skip this step and manually list the columns in your file, click **Continue** to go directly to the **Map Columns** screen.

Complete following steps to upload a sample file:

1. Click **Upload File** and select the sample CSV file you want to upload.  
The **Sample File** preview screen displays the file contents in table format.
1. Scroll through the sample file to verify that the columns and data look correct. The detected column names are listed in CSV format below the table and are prepopulated on the **Map Columns** screen.
1. If there are problems with the sample file, click **Remove** and correct the errors or try another file.
1. After you are done reviewing the contents of the sample file, click **Continue**.


## 3. Configure column mappings

Use the **Map Columns** table to map preconfigured column labels to event attributes or manually enter your file column labels for mapping. Each row of the CSV file is processed as an event. 

Columns not mapped to an event attribute will be ignored. Mapped columns not present in the CSV file will be skipped.

Complete the following steps to map your file column labels to event attributes:

1. Use the **Event Specification** drop-down list to select the specification that matches the data in the file. To use a custom set of event attributes, select **Custom**.  
This selection determines the value of the `tealium_event` attribute during the import process. If you select **Custom**, `tealium_event` is set to **imported**, otherwise it is set to the corresponding specification name, such as **purchase**.
<blockquote>
Changing the selected specification resets the column mapping table.
</blockquote>

1. If you did not upload a sample file, enter the file column labels into the **Map Columns** table. Each CSV column label must be unique.
1. Select the corresponding event attribute from the drop-down list.  
If the column contains a date/time value, select the corresponding attribute and click **Set Format**. In the **Date/Time Format** slideout, select the appropriate date/time format or enter a custom format and click **Done**.
1. When you are done mapping all corresponding event attributes, click **Continue**.

## 4. Map visitor ID attributes 

To use your file data with AudienceStream, map your data to visitor ID attributes. Select the mapped event attribute that represents a visitor ID and map it to the corresponding visitor ID attribute. 


<blockquote>
Visitor ID Mapping in AudienceStream is enabled by default. Disabling visitor ID mapping may cause errors in visitor stitching. For more information about Visitor ID Mapping in AudienceStream, see [Visitor Identification using Tealium Data Sources](https://docs.tealium.com/visitor-identification-data-sources/).
</blockquote>


## 5. Configure a file transfer service


<blockquote>
If you use your own file transfer service, have the connection details ready before proceeding.
</blockquote>


Choose an existing file service configuration or create a new one.
* If you have already created a file service configuration, see the [Complete an existing file service configuration](#complete-an-existing-file-service-configuration) section.
* To change your file service information, click the edit icon next to your configuration name.
* To add a new configuration, see the [Add a new file service configuration](#add-a-new-file-service-configuration) section.

### Complete an existing file service configuration

To complete or edit your file service configuration, complete the following steps:

1. Select your existing configuration from the **Choose File Service Configuration** drop-down list. 
1. Enter the **File Name Prefix**, such as `customers`. The prefix of the file name is used to identify which file import data source to use when importing the data in the file. In this example, a prefix of `customers` is used to create a CSV file titled `customers_VERSION.csv`. The prefix can contain underscores, but do not include an underscore at the end.
<blockquote>
The file name prefix must be unique between multiple file import data sources. For example, using the prefixes `customers` and `customers-orders` will cause unexpected results because they share the same initial prefix: `customers`.
</blockquote>

1. (Optional) To improve file processing efficiency, compress your files using a GZIP format. If your files are compressed, select **GZIP** for the **Compression** format. 
1. (Optional) To ensure secure processing of your files, encrypt your files with PGP encryption. If your files are encrypted, select **PGP** for the **Encryption** format.  
<blockquote>
If you are processing files that are both compressed and encrypted, the files must be compressed first, then encrypted. New versions of previously mapped files must use the same encryption and compression methods as the original files.  
For more information about compression in File Import, see [Encryption and Compression in File Import Data Sources](https://docs.tealium.com/encryption-and-compression-file-import/).
</blockquote>

1. In the **Enable File Service Processing** section, use the toggle to enable or disable service processing for File Import.
    * When set to **ON**, the file service is checked and files are processed every 10 minutes.
    * Set to **OFF** if you are not ready to start processing files. You can enable the service later.
1. Click **Continue** to go to the **Summary** tab.

### Add a new file service configuration

To add a new file transfer service configuration, complete the following steps:

1. Click the **+** icon to add a new file service configuration.
1. In the **Service Configuration** screen, enter a name for your configuration and select the type of file service you want to use.
1. Enter the credentials necessary to access the selected service.  
    * **Tealium S3 Bucket** - The necessary credentials are generated for you automatically.
    * **My SFTP Connection** - Choose an **Authentication Method**. **Password**, **Upload Private Key File**, and **Generate Key Pair** are supported authentication methods.
      * If you select **Password**, enter the password and click **Test File Source Connection**.
      * If you select **Upload Private Key File**, choose a file from the list and click **Test File Source Connection**.
      * If you select **Generate Key Pair**, click **Generate** and click **Test File Source Connection**.
1. (Optional) Click **Test Connection** to test your file service connection.
1. Click **Save**.


## 6. Summary
In this final step, view the summary, make any needed corrections, and then save and publish your profile.


1. View the **Event Attribute** and **Visitor ID mappings**.
1. To edit your configuration, click **Previous** to return to the step where you want to make changes.
1. Click **Finish** to exit the configuration screen. Your new data source is now listed in the **Data Sources Dashboard.**
1. Click **Save/Publish** to save and publish your changes.


<blockquote>
To check the status of import activity, navigate to the **Data Sources Dashboard** by expanding the data source and clicking the **Status** tab. For more information, see [View import status](https://docs.tealium.com/view-import-status/).
</blockquote>



## Edit a File Import data source configuration

To change a file import data source configuration, navigate to the **Data Sources Dashboard** and click the edit icon next to the configuration you want to change. From the **Data Sources Settings** screen, you can edit column mapping, visitor ID mapping, and file service configuration settings.

