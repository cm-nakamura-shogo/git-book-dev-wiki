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

## アップデート

### [2023-02-24 東京リージョンで「C7g」AWS Graviton 3のEC2が利用可能に](https://dev.classmethod.jp/articles/c7g-ec2-tokyo-region/)