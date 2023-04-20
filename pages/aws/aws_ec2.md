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

## 参考記事

### [2017-11-21 パラメーターストアから最新のWindows AMIのIDを取得する](https://dev.classmethod.jp/articles/latest-windows-ami-from-parameter-store)

parameter storeからAMIの情報を取得することができる。

### [2023-04-18 Amazon Linux 2023でDNSサーバーを指定する方法](https://dev.classmethod.jp/articles/amazon-linux-2023-static-dns/)

- 今までと少し違うらしい。

### 2023-04-17 Red Hat公式のAMIを探す方法

以下に公式のアカウント番号がある。

- [Amazon EC2 で公式の Red Hat Enterprise Linux AMI を特定する方法 - Red Hat Customer Portal](https://access.redhat.com/ja/solutions/274443)

なのでdescribe-imagesコマンドで以下のようにすればよい。

```bash
aws ec2 describe-images --owners 309956199498 --query 'sort_by(Images, &CreationDate)[*].[CreationDate,Name,ImageId]' --filters "Name=name,Values=RHEL-8.7*" --region ap-northeast-1 --output table
```

## アップデート

### [2023-02-24 東京リージョンで「C7g」AWS Graviton 3のEC2が利用可能に](https://dev.classmethod.jp/articles/c7g-ec2-tokyo-region/)