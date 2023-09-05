# Amazon EC2

## インスタンスファミリー

例：C5d.xlarge

- Cが狭義のインスタンスファミリー
  - AWS公式でもこの表現をしている場合がある。
  - カテゴライズの際など。
- C5dが広義のインスタンスファミリー
  - RI(リザーブドインスタンス)やSP(Savings Plans)購入時はこちらに気を付ける必要がある。
  - インスタンスサイズの柔軟性やインスタンスファミリーの指定が広義レベルの話となっている。
- 5は世代
- dは追加機能
- xlargeはインスタンスサイズ
- C5d.xlarge全体でインスタンスタイプ

## AMI

### Red Hat公式のAMIを探す方法

以下に公式のアカウント番号がある。

- [Amazon EC2 で公式の Red Hat Enterprise Linux AMI を特定する方法 - Red Hat Customer Portal](https://access.redhat.com/ja/solutions/274443)

なのでdescribe-imagesコマンドで以下のようにすればよい。

```bash
aws ec2 describe-images --owners 309956199498 --query 'sort_by(Images, &CreationDate)[*].[CreationDate,Name,ImageId]' --filters "Name=name,Values=RHEL-8.7*" --region ap-northeast-1 --output table
```

### Amazon公式のAMIのアカウントIDを調べる

```bash
aws ec2 describe-images --owners amazon --query 'Images[].OwnerId' | jq unique
```

- [公開されているAMIの所有者がAmazonであることを確認する方法 | DevelopersIO](https://dev.classmethod.jp/articles/tsnote-ami-amazon-cli/)