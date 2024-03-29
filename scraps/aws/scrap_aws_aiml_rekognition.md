# Amazon Rekognition

## article

- [2022-09-09 Amazon Rekognition Custom Labels でモデル精度を向上するための Tips](https://aws.amazon.com/jp/blogs/news/tips-to-improve-your-amazon-rekognition-custom-labels-model/)
  - プロジェクトで使う際に有用かも

- [2023-09-08 コンピュータ・ビジョン技術を使用して、電柱の異常を自動検出する](https://aws.amazon.com/jp/blogs/machine-learning/improving-asset-health-and-grid-resilience-using-machine-learning/)
  - ヘリコプター飛行で収集した高解像度画像を使用して、電柱の異常検出を自動化するコンピュータビジョンベースのソリューションを開発
  - コアはAmazon Rekognition Custom Labelsらしい

## update

- [2023-05-03 画像や動画に対するコンテンツモデレーションの精度を改善 (AWS)](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-rekognition-content-moderation-images-videos/)

- [2023-05-05 Rekognitionが本人確認精度を向上させる顔面オクルージョン検出を開始 (AWS)](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-rekognition-face-occlusion-identity-verification-accuracy/)
  - 画像内の顔が、オブジェクト、衣服、体の一部が重なっているために部分的に写っているか、完全に見えていないかを検出する機能
  - これはDetectFacesおよびIndexFaces APIでFaceOccluded属性として提供され、追加の品質チェックとして使用することができる
  - 顔の隠蔽が検出された場合、お客様はユーザーから隠蔽されていない顔画像を要求することができる
  - 真を返す例
    - 検出された顔の目、鼻、口が部分的に捉えられている場合、またはマスク、暗いサングラス、携帯電話、手、その他のオブジェクトで覆われている場合
  - 偽を返す例
    - 眼鏡、薄い色のサングラス、髪の毛など、顔認証に影響を与えない一般的な事象を検出した場合

- [2023-05-17 Amazon Rekognition、Face APIsで視線方向検出を開始](https://aws.amazon.com/jp/about-aws/whats-new/2023/05/amazon-rekognition-eye-gaze-direction-detection-face-apis/)
  - Rekognition DetectFacesおよびIndexFaces APIsの新しい属性としてEyeDirectionが追加される形
  - 画像内で検出された各顔について、人の視線方向のヨー（縦軸の回転）およびピッチ（横軸の回転）角度を予測
  - ヨー角とピッチ角の値を-180度から180度の間で予測し、0から100の間の信頼度スコアが設定される
  - APIアップデート
    - [https://awsapichanges.info/archive/changes/5f8543-rekognition.html](https://awsapichanges.info/archive/changes/5f8543-rekognition.html)
  - devio
    - [[アップデート] Amazon Rekognition で顔写真の視線の方向（Eye Direction）を検出できるようになりました | DevelopersIO](https://dev.classmethod.jp/articles/amazon-rekognition-eyes-gaze-direction-detection-in-face-apis/#toc-1)
    - 正直精度は低そうやな…

- [2023-06-13 Rekognitionがユーザーベクトルで顔検索の精度を向上](https://aws.amazon.com/jp/about-aws/whats-new/2023/06/amazon-rekognition-face-search-accuracy-user-vectors/)
  - 同一ユーザーの複数の顔画像を活用することで、顔検索の精度を大幅に向上させる新機能を発表
  - 顔ベクトルとは、画像から顔を数学的に表現したもので、今回同一ユーザーの複数の顔ベクトルを集約したユーザーベクトルを作成することが可能に
  - ユーザーベクターは、照明、シャープネス、ポーズ、見た目など様々な要素を含んでいるため、よりロバストな描写で高い顔検索精度を実現
  - [AWS API Changes](https://awsapichanges.info/archive/changes/106e8b-rekognition.html)
