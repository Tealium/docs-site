---
title: Tealium IP addresses to allow
description: This article provides a list of IP addresses to include in your allowlist to enable the Tealium platform to communicate with external systems.
url: https://docs.tealium.com/administration/security-access/ip-allow-list/
---
## How it works

The Tealium platform communicates with external systems during the following operations:

* Sending data with connector actions.
* Making requests to external services in [functions]().
* Processing [file import data sources]() (other than AWS S3).

If an external system restricts access to only an approved list of IP addresses, then you must add all of the following IP addresses to your allowlist:

For OAuth calls, test connections initiated from the server-side interface, the Snowflake Streaming connector, SFTP connections, and file import data source test connections (excluding AWS S3), data is transmitted from IP addresses in the `us-west-1` region. To enable these features, ensure that the IP addresses for the `us-west-1` region are included in your allowlist.&lt;br&gt;&lt;br&gt;Additionally, include the IP addresses for the region associated with your specific server-side profile, which can be found under **Server-Side Settings** &gt; **Region**.&lt;br&gt;&lt;br&gt;Note that only login information is transmitted during OAuth calls and test connections. No customer data is sent during these operations.

| IP Address | Region  | Location |
| -------------- | -------------| ----------- |
| 50.18.192.141&lt;br&gt;52.52.159.89&lt;br&gt;54.153.15.248&lt;br&gt;54.176.233.190&lt;br&gt;54.183.127.212&lt;br&gt;54.193.243.80 | `us-west-1`  | San Jose, California |
| 34.208.6.185&lt;br&gt;35.83.9.139&lt;br&gt;35.155.164.60&lt;br&gt;35.155.225.25&lt;br&gt;35.163.73.149&lt;br&gt;44.228.182.113&lt;br&gt;44.231.202.70&lt;br&gt;44.238.18.189&lt;br&gt;52.32.22.16 | `us-west-2` | Oregon |
| 3.210.6.72&lt;br&gt;3.210.238.60&lt;br&gt;3.214.63.89&lt;br&gt;23.23.136.136&lt;br&gt;34.224.220.100&lt;br&gt;44.220.225.247&lt;br&gt;54.82.200.66&lt;br&gt;54.164.73.126&lt;br&gt;107.23.142.239 |  `us-east-1` | Ashburn, Virginia |
| 34.251.234.107&lt;br&gt;52.30.45.164&lt;br&gt;52.31.156.52&lt;br&gt;52.48.83.213&lt;br&gt;52.209.154.50&lt;br&gt;54.76.122.246&lt;br&gt;54.195.193.79&lt;br&gt;54.229.215.104&lt;br&gt;108.128.75.88 | `eu-west-1`      | Dublin, Ireland |
| 3.72.173.191&lt;br&gt;3.79.77.159&lt;br&gt;3.125.211.165&lt;br&gt;18.193.100.101&lt;br&gt;18.195.141.132&lt;br&gt;18.198.88.136&lt;br&gt;18.199.16.199&lt;br&gt;52.29.52.87&lt;br&gt;52.29.185.253&lt;br&gt;54.93.104.232  | `eu-central-1`   | Frankfurt, Germany |
| 16.163.133.41&lt;br&gt;16.163.255.152&lt;br&gt;18.163.149.136&lt;br&gt;18.166.4.167&lt;br&gt;18.167.208.249&lt;br&gt;18.167.237.249&lt;br&gt;43.198.29.150&lt;br&gt;43.198.173.159&lt;br&gt;43.199.6.88   | `ap-east-1`      | Hong Kong |
| 13.112.219.50&lt;br&gt;35.72.125.147&lt;br&gt;35.74.186.82&lt;br&gt;35.76.187.92&lt;br&gt;52.68.25.59&lt;br&gt;52.69.49.172&lt;br&gt;52.196.255.145&lt;br&gt;54.64.29.101&lt;br&gt;54.64.71.25  | `ap-northeast-1` | Tokyo, Japan |
| 3.1.110.78&lt;br&gt;13.213.156.181&lt;br&gt;13.213.213.34&lt;br&gt;13.229.167.61&lt;br&gt;52.77.131.77&lt;br&gt;52.221.89.137&lt;br&gt;54.151.174.143&lt;br&gt;54.251.195.112&lt;br&gt;54.254.212.72| `ap-southeast-1` | Singapore|
| 3.25.4.61&lt;br&gt;13.54.68.127&lt;br&gt;13.54.118.13&lt;br&gt;13.237.193.244&lt;br&gt;13.237.225.69&lt;br&gt;52.62.159.75&lt;br&gt;52.64.214.94&lt;br&gt;52.64.154.49&lt;br&gt;54.253.220.122 | `ap-southeast-2` | Sydney, Australia |
| 3.28.34.78&lt;br&gt;3.29.103.105&lt;br&gt;3.29.118.210&lt;br&gt;40.172.248.172&lt;br&gt;40.172.249.33&lt;br&gt;51.112.137.196&lt;br&gt;51.112.152.225&lt;br&gt;51.112.35.98&lt;br&gt;51.112.64.17 | `me-central-1` | Dubai, United Arab Emirates |

## Private cloud environments

If you&#39;re using a private cloud environment, contact your support team to get the IP address specific to your account and add it to your allowlist.

If you&#39;re using the `PC-HMT` environment, also add 52.36.206.227 to your allowlist.

## AWS S3

Tealium [File Import]() can retrieve files from either the included Tealium S3 bucket or your S3 bucket. If you want to retrieve files from your company&#39;s own S3 bucket (not the included Tealium S3 bucket), the AWS bucket policy allowlist must include the VPCe IDs (VPC endpoint IDs) below and the above IP addresses.

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