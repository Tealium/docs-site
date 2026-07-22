---
title: Tealium IP addresses to allow
description: This article provides a list of IP addresses to include in your allowlist to enable the Tealium platform to communicate with external systems.
url: https://docs.tealium.com/administration/security-access/ip-allow-list/
---
## How it works

The Tealium platform communicates with external systems during the following operations:

* Sending data with connector actions.
* Making requests to external services in [functions](https://docs.tealium.com/about-functions/).
* Processing [file import data sources]() (other than AWS S3).

If an external system restricts access to only an approved list of IP addresses, then you must add all of the following IP addresses to your allowlist:


<blockquote>
For OAuth calls, test connections initiated from the server-side interface, the Snowflake Streaming connector, SFTP connections, and file import data source test connections (excluding AWS S3), data is transmitted from IP addresses in the `us-west-1` region. To enable these features, ensure that the IP addresses for the `us-west-1` region are included in your allowlist.<br><br>Additionally, include the IP addresses for the region associated with your specific server-side profile, which can be found under **Server-Side Settings** > **Region**.<br><br>Note that only login information is transmitted during OAuth calls and test connections. No customer data is sent during these operations.
</blockquote>


| IP Address | Region  | Location |
| -------------- | -------------| ----------- |
| 50.18.192.141<br>52.52.159.89<br>54.153.15.248<br>54.176.233.190<br>54.183.127.212<br>54.193.243.80 | `us-west-1`  | San Jose, California |
| 34.208.6.185<br>35.83.9.139<br>35.155.164.60<br>35.155.225.25<br>35.163.73.149<br>44.228.182.113<br>44.231.202.70<br>44.238.18.189<br>52.32.22.16 | `us-west-2` | Oregon |
| 3.210.6.72<br>3.210.238.60<br>3.214.63.89<br>23.23.136.136<br>34.224.220.100<br>44.220.225.247<br>54.82.200.66<br>54.164.73.126<br>107.23.142.239 |  `us-east-1` | Ashburn, Virginia |
| 34.251.234.107<br>52.30.45.164<br>52.31.156.52<br>52.48.83.213<br>52.209.154.50<br>54.76.122.246<br>54.195.193.79<br>54.229.215.104<br>108.128.75.88 | `eu-west-1`      | Dublin, Ireland |
| 3.72.173.191<br>3.79.77.159<br>3.125.211.165<br>18.193.100.101<br>18.195.141.132<br>18.198.88.136<br>18.199.16.199<br>52.29.52.87<br>52.29.185.253<br>54.93.104.232  | `eu-central-1`   | Frankfurt, Germany |
| 16.163.133.41<br>16.163.255.152<br>18.163.149.136<br>18.166.4.167<br>18.167.208.249<br>18.167.237.249<br>43.198.29.150<br>43.198.173.159<br>43.199.6.88   | `ap-east-1`      | Hong Kong |
| 13.112.219.50<br>35.72.125.147<br>35.74.186.82<br>35.76.187.92<br>52.68.25.59<br>52.69.49.172<br>52.196.255.145<br>54.64.29.101<br>54.64.71.25  | `ap-northeast-1` | Tokyo, Japan |
| 3.1.110.78<br>13.213.156.181<br>13.213.213.34<br>13.229.167.61<br>52.77.131.77<br>52.221.89.137<br>54.151.174.143<br>54.251.195.112<br>54.254.212.72| `ap-southeast-1` | Singapore|
| 3.25.4.61<br>13.54.68.127<br>13.54.118.13<br>13.237.193.244<br>13.237.225.69<br>52.62.159.75<br>52.64.214.94<br>52.64.154.49<br>54.253.220.122 | `ap-southeast-2` | Sydney, Australia |
| 3.28.34.78<br>3.29.103.105<br>3.29.118.210<br>40.172.248.172<br>40.172.249.33<br>51.112.137.196<br>51.112.152.225<br>51.112.35.98<br>51.112.64.17 | `me-central-1` | Dubai, United Arab Emirates |

## Private cloud environments

If you're using a private cloud environment, contact your support team to get the IP address specific to your account and add it to your allowlist.

If you're using the `PC-HMT` environment, also add 52.36.206.227 to your allowlist.

## AWS S3

Tealium [File Import](https://docs.tealium.com/about-file-import/) can retrieve files from either the included Tealium S3 bucket or your S3 bucket. If you want to retrieve files from your company's own S3 bucket (not the included Tealium S3 bucket), the AWS bucket policy allowlist must include the VPCe IDs (VPC endpoint IDs) below and the above IP addresses.

For more information about AWS bucket policies, see the following articles in the AWS documentation:

* [Adding a bucket policy by using the Amazon S3 console](https://docs.aws.amazon.com/AmazonS3/latest/userguide/add-bucket-policy.html)
* [Controlling access from VPC endpoints with bucket policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies-vpc-endpoint.html)

| VPC Endpoint ID | Region |
| ---|---|
|vpce-0a90f919e7498cdde|ap-east-1 (Hong Kong)|
|vpce-0a4bf8ead3aea5037|ap-northeast-1 (Tokyo)|
|vpce-0703e4f94cb9fdf27|ap-southeast-1 (Singapore)|
|vpce-0c7d746d995509e11|ap-southeast-2 (Sydney)|
|vpce-0846ac0c8e0640982|eu-central-1 (Germany)|
|vpce-0e9f722cf43431023|eu-west-1 (Ireland)|
|vpce-05d7e73f9198f3805|me-central-1 (Dubai)|
|vpce-0a993429061ac314f|us-east-1 (Virginia)|
|vpce-0ce7ea5d3270c6ebf|us-west-2 (Oregon)|
|vpce-00e07d2d5e4b55215|us-west-1 (California)|