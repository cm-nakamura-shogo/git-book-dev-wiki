# Amazon Rekognition

## アップデート

### [2023-05-03 画像や動画に対するコンテンツモデレーションの精度を改善 (AWS)](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-rekognition-content-moderation-images-videos/)

### [2023-05-05 Rekognitionが本人確認精度を向上させる顔面オクルージョン検出を開始 (AWS)](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-rekognition-face-occlusion-identity-verification-accuracy/)

- 画像内の顔が、オブジェクト、衣服、体の一部が重なっているために部分的に写っているか、完全に見えていないかを検出する機能
- これはDetectFacesおよびIndexFaces APIでFaceOccluded属性として提供され、追加の品質チェックとして使用することができる
- 顔の隠蔽が検出された場合、お客様はユーザーから隠蔽されていない顔画像を要求することができる
- 真を返す例
  - 検出された顔の目、鼻、口が部分的に捉えられている場合、またはマスク、暗いサングラス、携帯電話、手、その他のオブジェクトで覆われている場合
- 偽を返す例
  - 眼鏡、薄い色のサングラス、髪の毛など、顔認証に影響を与えない一般的な事象を検出した場合