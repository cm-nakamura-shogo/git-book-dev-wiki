# Amazon Comprehend

## アップデート

### [2023-04-19 Comprehend、レイアウトデータを利用した文書分類の精度を向上](https://aws.amazon.com/jp/about-aws/whats-new/2023/04/amazon-comprehend-document-classification-layout-data/)

- Comprehend APIs for Document Classificationがテキストに加えて、文書内のレイアウト情報を使用するようになったとのこと
- re:Invent 2022では、一般的なドキュメントタイプに対する推論をサポートしていたが、レイアウトデータを持つPDF/Word/Imageファイルのカスタム文書分類モデルを訓練する機能を持っていなかった
- レイアウト情報対応としては、英語でのドキュメントを処理することができるとされており、日本語に対応していない
- 関連するAPI更新
  - [https://awsapichanges.info/archive/changes/6019f5-comprehend.html](https://awsapichanges.info/archive/changes/6019f5-comprehend.html)
- 関連ブログ
  - [https://aws.amazon.com/jp/blogs/machine-learning/amazon-comprehend-document-classifier-adds-layout-support-for-higher-accuracy/](https://aws.amazon.com/jp/blogs/machine-learning/amazon-comprehend-document-classifier-adds-layout-support-for-higher-accuracy/)