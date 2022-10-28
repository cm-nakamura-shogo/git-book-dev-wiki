# 機械学習システム構成例

## デザインパターン(メルカリ)
- https://mercari.github.io/ml-system-design-pattern/README_ja.html

## EC2によるJupyter解析環境

Webhookを使って起動するアーキテクチャ。
ALB経由でEC2にアクセスし、ストレージにはEBSに加えてEFSを使用。
LambdaからのAPI Callで稼働状況を監視できる。

- [導入事例：機械学習の検証環境をAWSで構築 | AWS社内活用事例 | ソリューション | 株式会社BSNアイネット](https://www.bsnnet.co.jp/solution/casestudy/case03.html)