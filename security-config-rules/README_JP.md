# AWSCloudFormationTemplates/security-config-rules

AWSCloudFormationTemplates/security-config-rulesは、追加のConfigルールを提供します。

## Deployment

以下のコマンドを実行することで、CloudFormationをデプロイすることが可能です。

```bash
sam build
sam package --output-template-file packaged.yaml --s3-bucket S3_BUCKET_NAME
aws cloudformation deploy --template-file packaged.yaml --stack-name DefaultSecuritySettings-ConfigRules --s3-bucket S3_BUCKET_NAM --capabilities CAPABILITY_NAMED_IAM
```

デプロイ時に、以下のパラメータを指定することができます。

| Name | Parameter | Details | 
| --- | --- | --- | 
| AutoRemediation | Enabled/Disabled | Enabledを指定した場合、Lambda を用いた **自動修復機能** が有効化されます。 |
| RequiredTagKey | string | AWS Configは、このタグの無いAWSリソースを削除します。 |
| RequiredTagValue | string | AWS Configは、このタグの無いAWSリソースを削除します。 |