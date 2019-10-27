# AWSCloudFormationTemplates/security-config-rules

AWSCloudFormationTemplates/security-config-rules sets extended Config rules.

## Deployment

Execute the command to deploy.

```bash
sam build
sam package --output-template-file packaged.yaml --s3-bucket S3_BUCKET_NAME
aws cloudformation deploy --template-file packaged.yaml --stack-name DefaultSecuritySettings-ConfigRules --s3-bucket S3_BUCKET_NAM --capabilities CAPABILITY_NAMED_IAM
```

You can give optional parameters as follows.

| Name | Parameter | Details | 
| --- | --- | --- | 
| AutoRemediation | Enabled/Disabled | If it is Enabled, **AutoRemediation** by SSM Automation and Lambda are enabled. |
| RequiredTagKey | string | AWS Config removes AWSnresouces without this tag. |
| RequiredTagValue | string | AWS Config removes AWSnresouces without this tag. |