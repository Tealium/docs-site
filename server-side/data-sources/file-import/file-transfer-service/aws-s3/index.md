---
title: AWS S3
description: This article describes how to use the AWS S3 bucket to upload and manage files.
url: https://docs.tealium.com/server-side/data-sources/file-import/file-transfer-service/aws-s3/
---
  
<blockquote>
Storing large numbers of files in your S3 bucket may slow read times. We recommend regularly removing processed files from your S3 bucket to maintain efficient read times.
</blockquote>
 

## Credentials

You will need the following AWS credentials to configure the file service in the File Import configuration:

* Access Key
* Secret Key
* Bucket

Additionally, you can add a bucket prefix and region. For more information, see [AWS: Manage access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

## Region

The Amazon S3 bucket and Tealium profile must be assigned to the same region to successfully import files.

## Amazon S3 access configuration

If you use your company's own Amazon S3 bucket for your file service (not the included Tealium S3 bucket), you need to allow Tealium access to the Amazon S3 bucket before processing any files. 

## Amazon bucket policies

Use the AWS Policy Generator and the Amazon S3 console to add a new bucket policy. The Amazon S3 bucket policies control access to buckets from specific virtual private cloud (VPC) endpoints.

For more information about AWS bucket policies, see the following articles in the AWS documentation:
* [Adding a bucket policy by using the Amazon S3 console](https://docs.aws.amazon.com/AmazonS3/latest/userguide/add-bucket-policy.html)
* [Controlling access from VPC endpoints with bucket policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies-vpc-endpoint.html)

Use the following configuration details to allow Tealium access to the Amazon S3 bucket used in your file import data source.

```json
{
    "Version": "2012-10-17", //The specific AWS bucket policy version. Use this value.
    "Id": "VPCe and SourceIP",
    "Statement": [
        {
            "Sid": "VPCe and SourceIP",
            "Effect": "Deny",
            "Principal": "*",
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::name", //Replace "name" with the name of your bucket
                "arn:aws:s3:::name/*" //Replace "name" with the name of your bucket
            ],
            "Condition": {
                "NotIpAddress": {
                    "aws:SourceIp": [
                        "18.158.6.183", //An example of a Tealium Office VPN.  Add this IP if you want to allow Tealium staff to browse the bucket from their office. Get the value for your Tealium office from your CSM.
                        "50.18.192.141", //This and the following IP addresses are for the us-west-1 Tealium region. They must always be included for the CDH show the files present in the bucket.
                        "52.52.159.89",
                        "54.153.15.248",
                        "54.176.233.190",
                        "54.183.127.212",
                        "54.193.243.80",
                        "3.72.173.191", //This and the following IP addresses are for your specific CDH region. In this example, it is the eu-central-1 region. Find the correct list for YOUR CDH region from the "Tealium IP addresses to allow" listed below.
                        "3.79.77.159",
                        "3.125.211.165",
                        "18.193.100.101",
                        "18.195.141.132",
                        "18.198.88.136",
                        "18.199.16.199",
                        "52.29.52.87",
                        "52.29.185.253",
                        "54.93.104.232"
                    ]
                },
                "StringNotEquals": {
                    "aws:sourceVpce": "vpce-0846ac0c8e0640982" //The VPC Endpoint ID for your specific CDH region. In this example, it is the eu-central-1 region. Find the correct value for YOUR CDH region from the "Tealium IP addresses to allow" page listed below.
                }
            }
        }
    ]
}
```

## Addresses to allow

Ensure that you allow both the VPCe (VPC endpoint ID) for `us-west-1` and the VPCe for your profile region. 

To find your profile region, navigate to the server-side admin menu and select **Server-Side Settings > Region**. After you locate your region, select the corresponding VPCe from [Tealium IP addresses to allow](https://docs.tealium.com/ip-allow-list/).

## Use Amazon CLI to upload files to an empty S3 Bucket

When an S3 bucket is first created, it's empty. If you try to access an empty S3 bucket, the following message may be displayed:

`Failure to read attributes of ACCOUNT-PROFILE`

Before uploading any CSV files, use the following `aws s3api` command to upload a file into the empty bucket:

```bash
aws s3api put-object --bucket <bucket> --key <key> --body <body>
```

* The `bucket` value is the region domain in the format `collect-REGION.tealium.com`.
* The `key` value specifies the filename you want to assign to the file, including the file prefix.
* The `body` value specifies the file location on the local system.

For example:

```bash
aws s3api put-object --bucket collect-us-east-1.tealium.com \
  --key bulk-downloader/ACCOUNT-PROFILE/test_fileimp_01.csv \
  --body ./test_fileimp_01.csv
```

For more information, see [AWS Command Line Interface (CLI): How to Connect to Your S3 Bucket and Other Common Commands](https://support.tealiumiq.com/en/support/solutions/articles/36000363516-aws-command-line-interface-cli-how-to-connect-to-your-s3-bucket-and-other-common-commands).