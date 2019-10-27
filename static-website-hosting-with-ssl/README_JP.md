# AWSCloudFormationTemplates/static-website-hosting-with-ssl

AWSCloudFormationTemplates/static-website-hosting-with-ssl は、 ``Amazon CloudFront``, ``Amazon S3`` などの **静的Webサイトホスティング** に関連するAWSサービスを設定します。

### 準備

このテンプレートを実行する前に、本プロジェクトに含まれる ``Security`` テンプレートと ``Global Settings`` テンプレートの両方を実行してください。

+ [Security Template](../security/README_JP.md)
+ [Global Settings Template](../global/README_JP.md)

## デプロイ

以下のボタンをクリックすることで、**CloudFormationをデプロイ**することが可能です。

[![cloudformation-launch-stack](../images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=StaticWebsiteHosting&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/static-website-hosting-with-ssl/template.yaml) 

以下のコマンドを実行することで、CloudFormationをデプロイすることも可能です。

```bash
aws cloudformation deploy --template-file template.yaml --stack-name StaticWebsiteHosting --parameter-overrides DomainName=XXXXX CertificateManagerARN=XXXXX
```

デプロイ時に、以下のパラメータを指定することができます。

| 名前 | デフォルト値 | 詳細 |
| --- | --- | --- |
| CertificateManagerARN | | ARNを指定した場合、**CloudFront** に **SSL証明書** が紐付けられます。 |
| **DomainName** | | **必須** |
| CloudFrontDefaultTTL | 86400 | |
| CloudFrontMinimumTTL | 0 | |
| CloudFrontMaximumTTL | 31536000 | |
| CloudFrontViewerProtocolPolicy | redirect-to-https | |
| CloudFrontAdditionalName | | AdditionalNameを指定した場合、**CloudFront** に **エイリアス名** が紐付けられます。 |
| CloudFrontSecondaryOriginId | | SecondaryOriginIdを指定した場合、**CloudFront** に **セカンダリS3バケット** が紐付けられます。 |
| S3DestinationBucketArnOfCrossRegionReplication | | ARNを指定した場合、**S3** に **クロスリージョンレプリケーション** が設定されます。 |
| LoggingEnabled | Enabled | Enabledを指定した場合、**CloudFront** と **S3** のログ機能が有効化されます。 |
| LogBacketName | | バケット名を指定しなかった場合、ログが保管されるバケット名は、 'defaultsecuritysettings-logs-${AWS::Region}-${AWS::AccountId}' になります。 |

### 手動設定

本テンプレートを実行することで、 ``CloudFront`` に ``secondary origin server`` を設定することはできますが、 現時点ではCloudFormationで ``Origin Group`` がサポートされていません。
したがって、 CloudFormationのデプロイ完了後に、``Origin Group`` の作成と ``Default Cache Behavior Settings`` の**手動設定**が必要です。

1. ``Origins`` と ``Failover criteria`` を含んだ ``Origin Group`` を作成します。
2. ``Default Cache Behavior Settings`` の ``Origin or Origin Group`` に 1. で作成した ``Origin Group`` を指定します。

## アーキテクチャ

このテンプレートが作成するAWSリソースのアーキテクチャ図は、以下の通りです。

![](../images/architecture.png)

### Amazon S3

このテンプレートは、WebディストリビューションのオリジンとしてS3バケットを作成します。
``オリジンアクセスアイデンティティ``（``OAI``）を用いたCloudFrontからのアクセスは許可されますが、匿名ユーザからの直接アクセスは拒否されます。

### Amazon CloudFront

このテンプレートは、CloudFrontを作成します。
CloudFrontは、``Custom Domain Name with ACM``、 ``Aliases``、 ``Origin Access Identity``、 ``Secondary Origin``、``Logging``に対応します。