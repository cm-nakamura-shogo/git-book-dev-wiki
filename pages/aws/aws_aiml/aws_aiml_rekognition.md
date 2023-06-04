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

### [2023-05-17 Amazon Rekognition、Face APIsで視線方向検出を開始](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-rekognition-eye-gaze-direction-detection-face-apis/)

- Rekognition DetectFacesおよびIndexFaces APIsの新しい属性としてEyeDirectionが追加される形
- 画像内で検出された各顔について、人の視線方向のヨー（縦軸の回転）およびピッチ（横軸の回転）角度を予測
- ヨー角とピッチ角の値を-180度から180度の間で予測し、0から100の間の信頼度スコアが設定される
- APIアップデート
  - [https://awsapichanges.info/archive/changes/5f8543-rekognition.html](https://awsapichanges.info/archive/changes/5f8543-rekognition.html)
- devio
  - [[アップデート] Amazon Rekognition で顔写真の視線の方向（Eye Direction）を検出できるようになりました | DevelopersIO](https://dev.classmethod.jp/articles/amazon-rekognition-eyes-gaze-direction-detection-in-face-apis/#toc-1)
  - 正直精度は低そうやな…