# Amazon Transcribe

## Articles

- [2023-06-06 Transcribeで実際のトランスクリプトと一緒に提供するメタデータに基づいて自動的に段落を導入する方法](https://aws.amazon.com/blogs/machine-learning/arrange-your-transcripts-into-paragraphs-with-amazon-transcribe/)
  - 無音時間を使って段落分けを実現している。他の認識エンジンでも実現できそう。

## Updates

- [2023-07-26 Amazon Transcribeが会話内の有害性の検知をサポート](https://aws.amazon.com/jp/about-aws/whats-new/2023/07/amazon-transcribe-toxicity-detection-conversations/)
  - 有害なコンテンツは、セクシャルハラスメント、ヘイトスピーチ、脅迫、罵倒、冒涜、侮辱、グラフィックなど、7つのカテゴリーにわたってフラグが立てられ、分類される
  - この機能は主にオンラインゲームやソーシャルメディアの分野で利用される
  - Toxicity Detectionを使うことで、人間のモデレーターは、会話のどこで有害な内容が話されたかを正確に把握し、使用された言語を毒性スコアで分類することができる
  - これにより、コンテンツの聞き取りに費やす時間が95%削減される
  - Toxicity Detection は現在、バッチ処理でUS Englishで利用可能
  - APIが先行していたみたい
    - [2023-07-20 Transcribeがstoxicity-detectionを追加し、送信された音声の毒性スコアを表示できるように](https://awsapichanges.info/archive/changes/00fc0c-transcribe.html)