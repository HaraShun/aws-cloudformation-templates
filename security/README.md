# AWSCloudFormationTemplates/security

AWSCloudFormationTemplates/security sets basic configurations for **security**. This builds ``Amazon Inspector``, ``Amazon GuardDuty``, ``AWS Config``, ``AWS CloudTrail`` , ``AWS Security Hub`` and related resources.

## TL;DR

If you just want to deploy the stack, click press the button below.

[![cloudformation-launch-stack](../images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/template.yaml) 

If you want to deploy each service individually, press the buttons below.

| Services | Launchers |
| --- | --- |
| AWS Security Hub | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/securityhub.yaml) |
| Amazon Inspector | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/inspector.yaml) |
| Amazon GuardDuty | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/guardduty.yaml) |
| AWS CloudTrail | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/cloudtrail.yaml) |
| AWS Config | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/config.yaml) |

### Preparation

Before running this Cloudformation template, create an ``IAM Role Policy`` as shown in the following link, and attach the role to the user who will execute the template.

+ [CFn-Security-Settings.json](iam-policy/CFn-Security-Settings.json)

### Deployment

Execute the command to deploy.

```bash
aws cloudformation deploy --template-file template.yaml --stack-name DefaultSecuritySettings  --capabilities CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND
```

You can give optional parameters as follows.

| Name | Parameter | Details | 
| --- | --- | --- | 
| AuditOtherRegions | Enabled/Disabled | If it is Enabled, **CloudTrail** and **Include Global Resource Types** option in Config are enabled. |
| AutoRemediation | Enabled/Disabled | If it is Enabled, **AutoRemediation** by SSM Automation and Lambda are enabled. |

## Comply with Center for Internet Security (CIS) Benchmarks

This template helps you to comply with Center for Internet Security (CIS) Benchmarks.

| No. | Rules | Remediation |
| --- | --- | --- |
| 1.3 | Ensure credentials unused for 90 days or greater are disabled  | **Config** checks it and **Lambda** removes it automatically. |
| 1.4 | Ensure access keys are rotated every 90 days or less  | **Config** checks it and **Lambda** removes it automatically. |
| 1.5 | Ensure IAM password policy requires at least one uppercase letter | **Config** checks it and **SSM Automation** remediates the policy automatically. |
| 1.6 | Ensure IAM password policy requires at least one lowercase letter | **Config** checks it and **SSM Automation** remediates the policy automatically. |
| 1.7 | Ensure IAM password policy requires at least one symbol | **Config** checks it and **SSM Automation** remediates the policy automatically. |
| 1.8 | Ensure IAM password policy requires at least one number | **Config** checks it and **SSM Automation** remediates the policy automatically. |
| 1.9 | Ensure IAM password policy requires a minimum length of 14 or greater | **Config** checks it and **SSM Automation** remediates the policy automatically. |
| 1.10 | Ensure IAM password policy prevents password reuse | **Config** checks it and **SSM Automation** remediates the policy automatically. |
| 2.1 | Ensure CloudTrail is enabled in all Regions | This template enables **CloudTrail** and related resources in all Regions. |
| 2.2 | Ensure CloudTrail log file validation is enabled | This template enables **CloudTrail** and related resources in all Regions. |
| 2.3 | Ensure the S3 bucket CloudTrail logs to is not publicly accessible | This template enables **CloudTrail** and related resources in all Regions. |
| 2.4 | Ensure CloudTrail trails are integrated with Amazon CloudWatch Logs | This template enables **CloudTrail** and related resources in all Regions. |
| 2.5 | Ensure CloudTrail trails are integrated with Amazon CloudWatch Logs | This template enables **Config** and related resources. |
| 2.6 | Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket | This template enables **CloudTrail** and related resources in all Regions. |
| 2.7 | Ensure CloudTrail logs are encrypted at rest using AWS KMS CMKs | This template enables **CloudTrail** and related resources in all Regions. |
| 2.9 | Ensure VPC flow logging is enabled in all VPCs | **Config** checks it and **SSM Automation** enables VPC flow log automatically. |
| 3.1 | Ensure VPC flow logging is enabled in all VPCs | This template creates a log metric filter and alarm. |
| 3.2 | Ensure a log metric filter and alarm exist for AWS Management Console sign-in without MFA | This template creates a log metric filter and alarm. |
| 3.3 | Ensure a log metric filter and alarm exist for usage of "root" account | This template creates a log metric filter and alarm. |
| 3.4 | Ensure a log metric filter and alarm exist for IAM policy changes | This template creates a log metric filter and alarm. |
| 3.5 | Ensure a log metric filter and alarm exist for CloudTrail configuration changes | This template creates a log metric filter and alarm. |
| 3.6 | Ensure a log metric filter and alarm exist for AWS Management Console authentication failures | This template creates a log metric filter and alarm. |
| 3.7 | Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs | This template creates a log metric filter and alarm. |
| 3.8 | Ensure a log metric filter and alarm exist for S3 bucket policy changes | This template creates a log metric filter and alarm. |
| 3.9 | Ensure a log metric filter and alarm exist for AWS Config configuration changes | This template creates a log metric filter and alarm. |
| 3.10 | Ensure a log metric filter and alarm exist for security group changes | This template creates a log metric filter and alarm. |
| 3.11 | Ensure a log metric filter and alarm exist for changes to Network Access Control Lists (NACL) | This template creates a log metric filter and alarm. |
| 3.12 | Ensure a log metric filter and alarm exist for changes to network gateways | This template creates a log metric filter and alarm. |
| 3.13 | Ensure a log metric filter and alarm exist for route table changes | This template creates a log metric filter and alarm. |
| 3.14 | Ensure a log metric filter and alarm exist for VPC changes | This template creates a log metric filter and alarm. |
| 4.1| Ensure no security groups allow ingress from 0.0.0.0/0 to port 22 | **Config** checks it and **SSM Automation** remediates the rules automatically. |
| 4.2| Ensure no security groups allow ingress from 0.0.0.0/0 to port 3389 | **Config** checks it and **SSM Automation** remediates the rules automatically. |
| 4.3| Ensure the default security group of every VPC restricts all traffic | **Config** checks it and **SSM Automation** remediates the default security group automatically. |

## Architecture

The following sections describe the individual components of the architecture.

![](../images/architecture.png)

### AWS Security Hub

This template enables ``AWS Security Hub`` and setup ``Amazon SNS`` and ``Amazon CloudWatch Events`` to receive a message when a result of a compliance check changes to failure.

### Amazon GuardDuty

This template enables ``Amazon GuardDuty``.

### AWS Cloudtrail

This template enables ``AWS Cloudtrail`` and creates a ``S3 Bucket`` its logs are stored.

### Amazon Inspector

This template creates an Amazon Inspector ``assessment target`` and some ``assessment templates`` as follows.

+ [Network Reachability](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_network-reachability.html)
+ [Common Vulnerabilities and Exposures](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_cves.html)
+ [Center for Internet Security (CIS) Benchmarks](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_cis.html)
+ [Security Best Practices for Amazon Inspector](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_security-best-practices.html)

They run **every Monday at 9am** kicked by ``Amazon CloudWatch Events``.

This template supports some specific regions.

+ US East (N. Virginia)
+ US East (Ohio)
+ US West (N. California)
+ US West (Oregon)
+ Asia Pacific (Tokyo)
+ Asia Pacific (Seoul)
+ Asia Pacific (Sydney)
+ EU (Frankfurt)
+ EU (Ireland)
+ EU (London)
+ EU (Stockholm)

### AWS Config

This template creates an AWS Config ``delivery channel``, ``configuration recorder`` and some ``managed rules`` as follows.

+ [cloudformation-stack-drift-detection-check](https://docs.aws.amazon.com/config/latest/developerguide/cloudformation-stack-drift-detection-check.html)
+ [cloudformation-stack-notification-check](https://docs.aws.amazon.com/config/latest/developerguide/cloudformation-stack-notification-check.html)
+ [guardduty-enabled-centralized](https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html)

The following rules are enabled ``Automatic Remediation`` feature and attached ``SSM Automation Documents``.

+ [iam-password-policy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)
+ [iam-root-access-key-check](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)
+ [vpc-flow-logs-enabled](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html)
+ [vpc-sg-open-only-to-authorized-ports](https://docs.aws.amazon.com/config/latest/developerguide/vpc-sg-open-only-to-authorized-ports.html)
+ [vpc-default-security-group-closed](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

### Amazon CloudWatch Events

This template creates an ``Amazon CloudWatch Events`` for ``AWS Health``.
CloudWatch Events transfer its events to ``Amazon SNS``.

### Other Resources

This template creates some other resources such as ``Service-linked Role``, ``IAM Role``, ``S3 Bucket``, ``Amazon SNS`` and so on.