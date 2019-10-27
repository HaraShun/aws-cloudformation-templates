# AWSCloudFormationTemplates/global

AWSCloudFormationTemplates/global は、 N.Virginia (`us-east-1`)リージョンに ``ACM``と ``CloudFront`` および ``Billing`` に関する ``CloudWatch`` アラームを作成します。

## デプロイ

以下のボタンをクリックすることで、**CloudFormationをデプロイ**することが可能です。

[![cloudformation-launch-stack](../images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=GlobalSettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/global/template.yaml) 

以下のコマンドを実行することで、CloudFormationをデプロイすることも可能です。 
``ACM``, ``CloudFront``, ``Billing``は、``us-east-1`` リージョンでのみリソース作成が可能であるため、 ``us-east-1`` リージョンで実行してください。

```bash
aws cloudformation deploy --template-file template.yaml --stack-name GlobalSettings --parameter-overrides DomainName=XXXXX --region us-east-1
```

デプロイ時に、以下のパラメータを指定することができます。

| 名前 | デフォルト値 | 詳細 | 
| --- | --- | --- |
| ACMValidationMethod | DNS | |
| ACMDomainName | | ドメイン名を指定した場合、**SSL証明書**が作成されます。 |
| BillingAlertThreshold | 0 | 0以外の値を指定した場合、**CloudWatchアラーム**が作成されます。 |
| CloudFrontErrorRateThreshold | 0 | 0以外の値を指定した場合、**CloudWatchアラーム**が作成されます。 |
| CloudFrontErrorRequestPerMinuteThreshold | 0 | 0以外の値を指定した場合、**CloudWatchアラーム**が作成されます。 |
| CloudFrontBytesDownloadedPerMinuteThreshold | 0 | 0以外の値を指定した場合、**CloudWatchアラーム**が作成されます。 |
| CloudFrontDistributionId | | 監視対象のCloudFrontのディストリビューションID |

## アーキテクチャ

このテンプレートが作成するAWSリソースのアーキテクチャ図は、以下の通りです。

![](../images/architecture.png)

### AWS Certificate Manager

このテンプレートは、 ``AWS Certificate Manager`` を用いてSSL証明書を作成します。

### CloudWatch Alarm

このテンプレートは、 ``Billing`` と ``CloudFront`` (エラー率、リクエスト数、ダウンロードサイズ) のCloudWatchアラームを作成します。

### その他

このテンプレートは、 ``Amazon SNS`` などのリソースも合わせて作成します。