---
title: Use the Amazon Command Line Interface to upload and manage files
description: This article describes how to use the AWS Command Line Interface to upload and manage files.
url: https://docs.tealium.com/server-side/data-sources/file-import/file-transfer-service/aws-cli/
---
To install the AWS Command Line Interface (CLI), see [Installing, updating, and uninstalling the AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) in the Amazon documentation. For information on configuring AWS CLI, see [Configuration Basics](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html).

When you call the `aws configure` command, you are prompted for your Access Key and Access Key ID. You can leave Region Name and Output Format blank.

After you configure the CLI, make queries using the `s3api` method, as shown in the following CLI examples:

## List all objects in the root folder

```bash
aws s3 ls s3://collect-{REGION}.tealium.com/bulk-downloader/{ACCOUNT-PROFILE}/
```

## Copy a file into a folder

```bash
aws s3 cp local_file.csv s3://collect-{REGION}.tealium.com/bulk-downloader/{ACCOUNT-PROFILE}/
```

## Remove a file from a folder

```bash
aws s3 rm s3://collect-{REGION}.tealium.com/bulk-downloader/{ACCOUNT-PROFILE}/local_file.csv
```

