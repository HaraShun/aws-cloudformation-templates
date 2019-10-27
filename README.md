# AWSCloudFormationTemplates

AWSCloudFormationTemplates contains useful Cloudformation templates for basic settings.

## Templates

This project contains Cloudformation templates as follows.

| Template Name | AWS Region Code | Launch |
| --- | --- | --- |
| [Security Template](/security/README.md) | ap-northeast-1 | [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/template.yaml) |
| [Global Settings Template](/global/README.md) | us-east-1 | [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=GlobalSettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/global/template.yaml) |
| [Static Website Hosting Template](/static-website-hosting-with-ssl/README.md) | ap-northeast-1 | [![cloudformation-launch-stack](images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=StaticWebsiteHosting&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/static-website-hosting-with-ssl/template.yaml)  |

## Architecture

The following section describes the individual components of the architecture.

![](images/architecture.png)