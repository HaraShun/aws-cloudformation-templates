# AWSCloudFormationTemplates/security

AWSCloudFormationTemplates/security は、 ``Amazon Inspector``, ``Amazon GuardDuty``, ``AWS Config``, ``AWS CloudTrail`` , ``AWS Security Hub`` などの **セキュリティ** に関連するAWSサービスを設定します。

## 準備

このテンプレートを実行する前に、下のリンクに示すような ``IAM Role Policy`` を作成し、このテンプレートを実行する ``IAM User`` にアタッチしてください。

+ [CFn-Security-Settings.json](iam-policy/CFn-Security-Settings.json)

## デプロイ

以下のボタンをクリックすることで、**CloudFormationをデプロイ**することが可能です。

[![cloudformation-launch-stack](../images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/template.yaml) 

以下のボタンから、個別のAWSサービスを有効化することも可能です。

| 作成されるAWSサービス | 個別のCloudFormationテンプレート |
| --- | --- |
| AWS Security Hub | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/securityhub.yaml) |
| Amazon Inspector | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/inspector.yaml) |
| Amazon GuardDuty | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/guardduty.yaml) |
| AWS CloudTrail | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/cloudtrail.yaml) |
| AWS Config | [![cloudformation-launch-stack](https://raw.githubusercontent.com/eijikominami/aws-cloudformation-templates/master/images/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=DefaultSecuritySettings&templateURL=https://eijikominami.s3-ap-northeast-1.amazonaws.com/aws-cloudformation-templates/security/config.yaml) |

以下のコマンドを実行することで、CloudFormationをデプロイすることも可能です。

```bash
aws cloudformation deploy --template-file template.yaml --stack-name DefaultSecuritySettings  --capabilities CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND
```

デプロイ時に、以下のパラメータを指定することができます。

| 名前 | デフォルト値 | 詳細 |
| --- | --- | --- | 
| AuditOtherRegions | Enabled/Disabled | Enabledを指定した場合、**CloudTrail** と Config の **Include Global Resource Types** オプションが有効化されます。 |
| AutoRemediation | Enabled/Disabled | Enabledを指定した場合、SSM Automation と Lambda を用いた **自動修復機能** が有効化されます。 |

## Center for Internet Security (CIS) ベンチマークへの準拠

このテンプレートを実行することで、Center for Internet Security (CIS) ベンチマークの以下の項目に準拠します。

| No. | ルール | 実行内容 |
| --- | --- | --- |
| 1.3 | 90 日間以上使用されていない認証情報は無効にします | **Config** で定期的に確認を行い、非準拠の場合は **Lambda** で自動的に削除します。 |
| 1.4 | アクセスキーは 90 日ごとに更新します | **Config** で定期的に確認を行い、非準拠の場合は **Lambda** で自動的に削除します。 |
| 1.5 | IAM パスワードポリシーには少なくとも 1 つの大文字が必要です | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。 |
| 1.6 | IAM パスワードポリシーには少なくとも 1 つの小文字が必要です | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。 |
| 1.7 | IAM パスワードポリシーには少なくとも 1 つの記号が必要です | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。 |
| 1.8 | IAM パスワードポリシーには少なくとも 1 つの数字が必要です | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。 |
| 1.9 | IAM パスワードポリシーは 14 文字以上の長さが必要です | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。 |
| 1.10 | IAM パスワードポリシーはパスワードの再使用を禁止しています | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。 |
| 2.1 | CloudTrail はすべてのリージョンで有効になっています | **CloudTrail** と関連サービスを有効化します。 |
| 2.2 | CloudTrail ログファイルの検証は有効になっています | **CloudTrail** と関連サービスを有効化します。 |
| 2.3 | CloudTrail が記録する S3 バケットはパブリックアクセスできません | **CloudTrail** と関連サービスを有効化します。 |
| 2.4 | CloudTrail 証跡は Amazon CloudWatch Logs によって統合されています | **CloudTrail** と関連サービスを有効化します。 |
| 2.5 | すべてのリージョンで AWS Config が有効になっていることを確認します | **Config** と関連サービスを有効化します。 |
| 2.6 | S3 バケットアクセスログ記録が CloudTrail S3 バケットで有効になっていることを確認します | **CloudTrail** と関連サービスを有効化します。 |
| 2.7 | CloudTrail ログは保管時に AWS KMS CMK を使用して暗号化されていることを確認します | **CloudTrail** と関連サービスを有効化します。 |
| 2.9 | すべての VPC で VPC フローログ記録が有効になっていることを確認します  | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。  |
| 3.1 | 不正な API 呼び出しに対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.2 | MFA なしの AWS マネジメントコンソール サインインに対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.3 | ルート」アカウントに対してログメトリクスフィルタとアラームが存在することを確認します  | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.4 | MFA なしの IAM ポリシーの変更に対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.5 | MFA なしの CloudTrail 設定の変更に対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.6 | AWS マネジメントコンソール 認証の失敗に対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.7 | カスタマー作成の CMK の無効化またはスケジュールされた削除に対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.8 | S3 バケットの変更に対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.9 | AWS Config 設定の変更に対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.10 | セキュリティグループの変更に対するメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.11 | ネットワークアクセスコントロールリスト (NACL) への変更に対するログメトリクスとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.12 | ネットワークゲートウェイへの変更に対するログメトリクスとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.13 | ルートテーブルの変更に対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 3.14 | VPC の変更に対してログメトリクスフィルタとアラームが存在することを確認します | ログメトリクスフィルタとCloudWatchアラームを作成します。 |
| 4.1| どのセキュリティグループでも 0.0.0.0/0 からポート 22 への入力を許可しないようにします | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。 |
| 4.2| どのセキュリティグループでも 0.0.0.0/0 からポート 3389 への入力を許可しないようにします | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。 |
| 4.3| すべての VPC のデフォルトセキュリティグループがすべてのトラフィックを制限するようにします | **Config** で定期的に確認を行い、非準拠の場合は **SSM Automation** で自動修復を行います。 |

## アーキテクチャ

このテンプレートが作成するAWSリソースのアーキテクチャ図は、以下の通りです。

![](../images/architecture.png)

### AWS Security Hub

このテンプレートは、 ``AWS Security Hub`` を有効化します。
また、コンプライアンスチェックが失敗したとき、 ``Amazon SNS`` は ``Amazon CloudWatch Events`` 経由でメッセージを受け取ります。

### Amazon GuardDuty

このテンプレートは、 ``Amazon GuardDuty`` を有効化します。

### AWS Cloudtrail

このテンプレートは、 ``AWS Cloudtrail`` を有効化し、ログを蓄積する ``S3バケット`` を生成します。

### Amazon Inspector

このテンプレートは、以下の Amazon Inspector ``アセスメントターゲット`` といくつかの ``アセスメントテンプレート`` を作成します。

+ [Network Reachability](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_network-reachability.html)
+ [Common Vulnerabilities and Exposures](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_cves.html)
+ [Center for Internet Security (CIS) Benchmarks](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_cis.html)
+ [Security Best Practices for Amazon Inspector](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_security-best-practices.html)

Amazon Inspector は、``Amazon CloudWatch Events``　によって **毎週月曜日午前9時** に実行されます。

このテンプレートは、以下のリージョンをサポートしています。

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

このテンプレートは、Amazon Config ``デリバリーチャンネル``、 ``レコーダ``と、以下の ``マネージドルール`` を作成します。

+ [cloudformation-stack-drift-detection-check](https://docs.aws.amazon.com/config/latest/developerguide/cloudformation-stack-drift-detection-check.html)
+ [cloudformation-stack-notification-check](https://docs.aws.amazon.com/config/latest/developerguide/cloudformation-stack-notification-check.html)
+ [guardduty-enabled-centralized](https://docs.aws.amazon.com/config/latest/developerguide/guardduty-enabled-centralized.html)

以下のルールは、``自動修復機能`` が有効化されており、 ``SSM Automation Documents`` が紐づけられています。

+ [iam-password-policy](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)
+ [iam-root-access-key-check](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)
+ [vpc-flow-logs-enabled](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html)
+ [vpc-sg-open-only-to-authorized-ports](https://docs.aws.amazon.com/config/latest/developerguide/vpc-sg-open-only-to-authorized-ports.html)
+ [vpc-default-security-group-closed](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

### Amazon CloudWatch Events

このテンプレートは、 ``AWS Health`` に関する  ``CloudWatchイベント`` を作成します。
CloudWatchイベントは、Amazon SNS にこれらのイベントを転送します。

### その他

このテンプレートは、 ``Service-linked Role``、 ``IAM Role``、 ``S3 Bucket``、 ``Amazon SNS`` などのリソースも合わせて作成します。