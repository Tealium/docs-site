---
title: AWS S3
description: この記事では、AWS S3バケットを使用してファイルをアップロードおよび管理する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/file-import/file-transfer-service/aws-s3/
---
  S3バケットに多数のファイルを保存すると、読み取り時間が遅くなる可能性があります。効率的な読み取り時間を維持するために、定期的に処理済みのファイルをS3バケットから削除することをお勧めします。

## 資格情報

ファイルインポート構成でファイルサービスを構成するためには、以下のAWS資格情報が必要です：

* アクセスキー
* シークレットキー
* バケット

さらに、バケットプレフィックスとリージョンを追加することができます。詳細については、[AWS: IAMユーザーのアクセスキーを管理する](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)を参照してください。

## リージョン

Amazon S3バケットとTealiumプロファイルは、ファイルを正常にインポートするために同じリージョンに割り当てる必要があります。

## Amazon S3アクセス構成

ファイルサービスに自社のAmazon S3バケットを使用する場合（TealiumのS3バケットを含まない）、ファイルを処理する前にTealiumがAmazon S3バケットにアクセスできるように構成する必要があります。

## Amazonバケットポリシー

AWSポリシージェネレーターとAmazon S3コンソールを使用して、新しいバケットポリシーを追加します。Amazon S3バケットポリシーは、特定の仮想プライベートクラウド（VPC）エンドポイントからのバケットへのアクセスを制御します。

AWSバケットポリシーに関する詳細は、AWSドキュメントの以下の記事を参照してください：
* [Amazon S3コンソールを使用してバケットポリシーを追加する](https://docs.aws.amazon.com/AmazonS3/latest/userguide/add-bucket-policy.html)
* [バケットポリシーを使用してVPCエンドポイントからのアクセスを制御する](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies-vpc-endpoint.html)

ファイルインポートデータソースで使用するAmazon S3バケットへのTealiumアクセスを許可するための以下の構成詳細を使用してください。

```json
{
    &#34;Version&#34;: &#34;2012-10-17&#34;, //特定のAWSバケットポリシーバージョン。この値を使用してください。
    &#34;Id&#34;: &#34;VPCe and SourceIP&#34;,
    &#34;Statement&#34;: [
        {
            &#34;Sid&#34;: &#34;VPCe and SourceIP&#34;,
            &#34;Effect&#34;: &#34;Deny&#34;,
            &#34;Principal&#34;: &#34;*&#34;,
            &#34;Action&#34;: &#34;s3:*&#34;,
            &#34;Resource&#34;: [
                &#34;arn:aws:s3:::name&#34;, //バケットの名前に「name」を置き換えてください
                &#34;arn:aws:s3:::name/*&#34; //バケットの名前に「name」を置き換えてください
            ],
            &#34;Condition&#34;: {
                &#34;NotIpAddress&#34;: {
                    &#34;aws:SourceIp&#34;: [
                        &#34;18.158.6.183&#34;, //TealiumオフィスVPNの例です。Tealiumスタッフがオフィスからバケットを閲覧できるようにする場合は、このIPを追加してください。CSMからTealiumオフィスの値を取得してください。
                        &#34;50.18.192.141&#34;, //これと次のIPアドレスはus-west-1 Tealiumリージョンのものです。CDHがバケット内のファイルを表示するためには、常に含める必要があります。
                        &#34;52.52.159.89&#34;,
                        &#34;54.153.15.248&#34;,
                        &#34;54.176.233.190&#34;,
                        &#34;54.183.127.212&#34;,
                        &#34;54.193.243.80&#34;,
                        &#34;3.72.173.191&#34;, //これと次のIPアドレスは、この例ではeu-central-1リージョンのあなたの特定のCDHリージョンのものです。YOUR CDHリージョンの正しいリストを「Tealium IPアドレスを許可する」ページから見つけてください。
                        &#34;3.79.77.159&#34;,
                        &#34;3.125.211.165&#34;,
                        &#34;18.193.100.101&#34;,
                        &#34;18.195.141.132&#34;,
                        &#34;18.198.88.136&#34;,
                        &#34;18.199.16.199&#34;,
                        &#34;52.29.52.87&#34;,
                        &#34;52.29.185.253&#34;,
                        &#34;54.93.104.232&#34;
                    ]
                },
                &#34;StringNotEquals&#34;: {
                    &#34;aws:sourceVpce&#34;: &#34;vpce-0846ac0c8e0640982&#34; //あなたの特定のCDHリージョンのVPCエンドポイントIDです。この例では、eu-central-1リージョンです。YOUR CDHリージョンの正しい値を「Tealium IPアドレスを許可する」ページから見つけてください。
                }
            }
        }
    ]
}
```

## 許可するアドレス

`us-west-1`のVPCe（VPCエンドポイントID）とあなたのプロファイルリージョンのVPCeの両方を許可することを確認してください。

プロファイルリージョンを確認するには、サーバーサイド管理メニューに移動し、**Server-Side Settings &gt; Region**を選択します。リージョンを特定した後、[Tealium IPアドレスを許可する]()から対応するVPCeを選択してください。

## Amazon CLIを使用して空のS3バケットにファイルをアップロードする

S3バケットが最初に作成されると、それは空です。空のS3バケットにアクセスしようとすると、次のメッセージが表示されることがあります：

`Failure to read attributes of ACCOUNT-PROFILE`

CSVファイルをアップロードする前に、次の`aws s3api`コマンドを使用して空のバケットにファイルをアップロードしてください：

```bash
aws s3api put-object --bucket &lt;bucket&gt; --key &lt;key&gt; --body &lt;body&gt;
```

* `bucket`の値はリージョンドメインの形式`collect-REGION.tealium.com`です。
* `key`の値はファイルに割り当てたいファイル名を指定します。ファイルプレフィックスを含みます。
* `body`の値はローカルシステム上のファイルの場所を指定します。

例えば：

```bash
aws s3api put-object --bucket collect-us-east-1.tealium.com \
  --key bulk-downloader/ACCOUNT-PROFILE/test_fileimp_01.csv \
  --body ./test_fileimp_01.csv
```

詳細については、[AWSコマンドラインインターフェース（CLI）：S3バケットに接続する方法とその他の一般的なコマンド](https://support.tealiumiq.com/en/support/solutions/articles/36000363516-aws-command-line-interface-cli-how-to-connect-to-your-s3-bucket-and-other-common-commands)を参照してください。