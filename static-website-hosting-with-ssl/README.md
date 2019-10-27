# AWSCloudFormationTemplates/static-website-hosting-with-ssl

AWSCloudFormationTemplates/static-website-hosting-with-ssl builds ``Amazon CloudFront``, ``Amazon S3`` and related resources for **static website hosting**.

## TL;DR

If you just want to deploy the stack follow these steps.

[![cloudformation-launch-stack](../images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=StaticWebsiteHosting&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/static-website-hosting-with-ssl/template.yaml) 

### Preparation

Before running this Cloudformation template, run both the ``Security`` template and ``Global Settings`` template of this project.

+ [Security Template](../security/README.md)
+ [Global Settings Template](../global/README.md)

### Deployment

Execute the command to deploy with ``DomainName`` parameter.

```bash
aws cloudformation deploy --template-file template.yaml --stack-name StaticWebsiteHosting --parameter-overrides DomainName=XXXXX CertificateManagerARN=XXXXX
```

You can give optional parameters as follows.

| Name | Default | Details | 
| --- | --- | --- |
| CertificateManagerARN | | If it's NOT empty, **SSL Certification** is associated with **CloudFront**. |
| **DomainName** | | **Required** |
| CloudFrontDefaultTTL | 86400 | |
| CloudFrontMinimumTTL | 0 | |
| CloudFrontMaximumTTL | 31536000 | |
| CloudFrontViewerProtocolPolicy | redirect-to-https | |
| CloudFrontAdditionalName | | If it's NOT empty, **Alias name** is set on **CloudFront**. |
| CloudFrontSecondaryOriginId | | If it's NOT empty, **Secondary S3 bucket** is associated with **CloudFront**. |
| S3DestinationBucketArnOfCrossRegionReplication | | If it's NOT empty, Cross region replication is enabled on **S3**. |
| LoggingEnabled | Enabled | If Enabled, Logging is enabled on **CloudFront** and **S3**. |
| LogBacketName | | If it's empty, the bucket name logging data are stored is named 'defaultsecuritysettings-logs-${AWS::Region}-${AWS::AccountId}'. |

### Manual Deployment

You can add ``secondary origin server`` in ``CloudFront`` by this CloudFormation Template, but it does **NOT suppport** creating ``Origin Group``.
Therefore create ``Origin Group`` and edit ``Default Cache Behavior Settings`` manually after comleting cloudFormation deployment.

1. Create ``Origin Group`` with ``Origins`` and ``Failover criteria`` .
2. Change ``Origin or Origin Group`` at ``Default Cache Behavior Settings`` to ``Origin Group`` you created.

## Architecture

The following sections describe the individual components of the architecture.

![](../images/architecture.png)

### Amazon S3

This template create a S3 bucket as origin for web distributions.
S3 allows to be accessed from CloudFront using an ``origin access identity`` (``OAI``) , but denies direct access from anonimous users.

### Amazon CloudFront

This template creates a CloudFront.
It supports ``Custom Domain Name with ACM``, ``Aliases``, ``Origin Access Identity``, ``Secondary Origin`` and ``Logging``.