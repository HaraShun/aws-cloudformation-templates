# AWSCloudFormationTemplates

AWSCloudFormationTemplates は、一般的な設定を含む便利なCloudformationテンプレートを提供します。

## テンプレート

本プロジェクトは、以下のCloudformationテンプレートから構成されます。

| テンプレート名 | リージョン | 実行 |
| --- | --- | --- |
| [Security Template](/security/README_JP.md) | ap-northeast-1 | [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/template.yaml) |
| [Global Settings Template](/global/README_JP.md) | us-east-1 | [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=GlobalSettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/global/template.yaml) |
| [Static Website Hosting Template](/static-website-hosting-with-ssl/README_JP.md) | ap-northeast-1 | [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=StaticWebsiteHosting&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/static-website-hosting-with-ssl/template.yaml)  |

## アーキテクチャ

これらのテンプレートが作成するAWSリソースのアーキテクチャ図は、以下の通りです。

![](images/architecture.png)