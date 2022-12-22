# aws cli設定

## 更新

```
> msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
> aws --version
```

- 今の設定を知りたい場合

```
$ aws configure list
```

- defaultのprofileを作成する場合

```
$ aws configure
AWS Access Key ID [None]: XXXXXXXXXXXXXXX
AWS Secret Access Key [None]: XXXXXXXXXXXXXXXXXXX
Default region name [None]: ap-northeast-1
Default output format [None]: json
```

- default profileをベースにスイッチロールする場合
  - 以下を追記する
  - これは元アカウントでMFA認証が必須なケース

```
[profile mlteam]
mfa_serial = arn:aws:iam::{スイッチ元アカウント}:mfa/{ユーザー名}
role_arn = arn:aws:iam::{スイッチ先アカウント番号}:role/{ユーザー名}
source_profile = default
```

- 別名のprofileを作成する場合

```
$ aws configure --profile {プロファイル名}
AWS Access Key ID [None]: XXXXXXXXXXXXXXX
AWS Secret Access Key [None]: XXXXXXXXXXXXXXXXXXX
Default region name [None]: ap-northeast-1
Default output format [None]: json
```

- 実行時のprofileを指定する場合

wslなどであれば

```
$ export AWS_PROFILE={プロファイル名}
```

powershellであれば

```
> $env:AWS_PROFILE = "cm-nakamura-test-mlflow"
```

- 実行する都度にprofileを指定する場合(例)

```
$ aws s3 ls --profile example
```

- 参考
  - [AWS CLI のコンフィグファイルと環境変数とコマンドラインオプションで指定できる内容をまとめて確認してみた](https://dev.classmethod.jp/articles/aws-cli-configuration-file-env-option/)
  - [AWS CLIのプロファイル切り替えをいい感じにする](https://qiita.com/crossroad0201/items/f84b3e2fece41750755b)
