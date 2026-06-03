---
title: View import status
description: This article describes how to view the status of imported files.
url: https://docs.tealium.com/server-side/data-sources/file-import/file-transfer-service/view-import-status/
---
 For more details on file import errors, use the custom [Bulk Download Logs](https://support.tealiumiq.com/en/support/solutions/articles/36000363442-tealium-tools-bulk-download-logs) tool.

##  View import activity

After you set up the file import data source and begin importing files, you can view the import activity in the **Data Sources Dashboard** by expanding the data source and clicking the **Status** tab. This page shows a rolling month report, with details about how many rows were processed, with and without errors, in graphical format. A tabular view appears directly underneath the graph.

![](/images/server-side/data-sources/file-import/file-import-status-chart.png)

File rows are processed at a variable rate based on the regional load in our multi-tenant environment, but most files are processed within 24 hours. 

If an error occurs, hover over the red area of a bar in the graph to display a breakdown of the errors. Tooltips show common errors with a link to a detailed report of all errors hosted in AWS S3. Hover over any bar in the graph to view details about the number of rows processed.

![](/images/server-side/data-sources/file-import/file-import-status-file-list.png)

## View imported events

To see events imported from files, navigate to the **Live Events** screen and select the file import data source from the drop-down list. For more information, see [About Live Events]().