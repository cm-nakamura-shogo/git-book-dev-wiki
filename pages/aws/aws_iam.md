# AWS IAM

IAM: 
IAMロールとは
IAMポリシーとは
IAMユーザとは

## パスロールとは

- IAM ロールの PassRole と AssumeRole をもう二度と忘れないために絵を描いてみた
  - https://dev.classmethod.jp/articles/iam-role-passrole-assumerole/

## RBAC: Role Based Access Control

- 役割ベースのアクセス制御

### RBACとは

- よくないケース：Principal毎にポリシーを作成して適用する。
- まずはPrincipalの役割(Role)に基づいてポリシーを設計する。 
- その後、必要なポリシーをPrincipalに適用(Attach)する。
- 人が増えてもスケールに強い。

### RBAC設計のTips

- まずは職務機能のAWS管理ポリシーを確認する。
  - 管理者: AdministratorAccess
  - パワーユーザー: PowerUserAccess
  - セキュリティ監査: SecurityAudit
  - etc
- それで不足・過剰があれば、カスタマー管理ポリシーを活用する。

### RBACのつらさ

- 役割がプロジェクト毎に細分化されて、膨大になる場合

## ABAC: Attribute Based Access Control

- 属性ベースのアクセス制御

### ABACとは

- Principalに属性(タグ)を付与する。（プロジェクトA, B, Cなど）
- ポリシーは一つだけで適用(Attach)する。
- 管理するポリシーが少なくて済む。
- プロジェクトが増えてもスケールに強い。

### ABAC設計のTips

- リソース側に属性(タグ)を付与する。
- あらかじめ制御範囲（サービス、リソース）や属性名（タグキー）を決める
- 実現にはConditionをフル活用する。
  - https://dev.classmethod.jp/articles/aws-iam-condition-key-availability/

### 元動画

- 【AWS IAM】セキュアなアクセス管理の方法を語る会
  - https://www.youtube.com/watch?v=pBvrmB-4t90

## IAM評価論理

- IAM の評価論理をやんわり押さえるセッション「やんわり押さえよう IAM の評価論理」で登壇しました
  - https://dev.classmethod.jp/articles/devio-2021-iam-evaluation-logic/

## [IAMの設定ドキュメント](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

細かい制限を加える場合はここら辺を参照する必要がある

## AssumeRole

普段ロールの切り替えでプロジェクト横断してるのがAssumeRole

信頼ポリシーは、切り替えるときに基幹のAWSアカウントから払い出されたIAM UserがMFAを使った場合のみプロジェクトのIAM RoleにAssumeすることができるっていう定義

なので、IAM Roleには以下のような信頼ポリシーが記載されています。

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::000000000000:user/cm-watanabe.koki"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "Bool": {
                    "aws:MultiFactorAuthPresent": "true"
                }
            }
        }
    ]
}
```

このポリシーに基づいてIAM Roleの権限を使える様になることを移譲って表現する

## 参考記事

### [IAM ロールの PassRole と AssumeRole をもう二度と忘れないために絵を描いてみた | DevelopersIO](https://dev.classmethod.jp/articles/iam-role-passrole-assumerole/)

### [2023-05-04 【S3 Bucketへのアクセス管理】 特定のIAM RoleにのみS3 Bucketへのアクセスを許可し、IAM User GroupとIAM Roleで厳密にスイッチングする方法 | DevelopersIO](https://dev.classmethod.jp/articles/s3-bucket-access-control-with-iam-role-and-group-switching/)
- むずくてよく分からんかった…
