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

### [2023-04-18 Amazon Linux 2023でDNSサーバーを指定する方法](https://dev.classmethod.jp/articles/amazon-linux-2023-static-dns/)

- 今までと少し違うらしい。

## アップデート

### [2023-02-24 東京リージョンで「C7g」AWS Graviton 3のEC2が利用可能に](https://dev.classmethod.jp/articles/c7g-ec2-tokyo-region/)