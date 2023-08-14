# AIML

## Books

- 未登録

## Contents

- [minido/Gasyori100knock-1: 画像処理100本ノックして画像処理を画像処理して画像処理するためのもの For Japanese, English and Chinese](https://github.com/minido/Gasyori100knock-1)
- BrainPad社の異常検知まとめ
  - [【連載⓪】 工業製品画像のデータセットで不良品検知手法の検証をする【不良品検知ブログ】（目次）](https://blog.brainpad.co.jp/entry/2020/12/04/113000)
  - [【連載①】画像に対する教師なし深層異常検知の基本手法【不良品検知ブログ】](https://blog.brainpad.co.jp/entry/2020/12/11/110000)
  - [【連載②】パラメータを自動調整する深層距離学習 -Adacos-【不良品検知ブログ】](https://blog.brainpad.co.jp/entry/2020/12/24/123000)
  - [【連載③】少量の学習データで機能する異常検知手法 -DifferNet-【不良品検知ブログ】](https://blog.brainpad.co.jp/entry/2021/01/15/110000)

## Articles

- [2020-05-14 MobileNetV2の転移学習](https://dev.classmethod.jp/articles/introduce-to-transfer-learning-by-tensorflow-for-beginner/)
- [2022-01-10 YOLOXので自作データの学習](https://zenn.dev/opamp/articles/d3878b189ea256)
- [2023-04-10 SparseFormer: 人間の視覚認識に基づいたスパースなプロセスへの挑戦](https://twitter.com/_akhaliq/status/1645278535878049792)
  - 現在の視覚ネットワークの多くは、画素やパッチなどの視覚単位を一律に処理する密なパラダイムに従っている
  - これを人間の疎な視覚認識をエンドツーエンドで模倣する手法
  - 計算コストの大幅な削減が可能
  - コードは1,2か月後らしい…
- [2023-04-11 Passregi CVの現在と取り組んできた改良](https://dev.classmethod.jp/articles/developers-io-day-one-passregi-cv-improvements/)
- [2023-04-14 SAMよりもより広範な機能をもつSEEMが公開](https://twitter.com/forasteran/status/1646829112844259329)
  - この界隈がまだよくわからいので、差異をまだ理解できていない。
- [2023-04-14 SAMを利用したZero-shotなPanoptic Segmentation](https://twitter.com/tobiascornille/status/1646812086154960896)
  - 「Segment Anything, Grounding DINO, and CLIPSeg.」というパイプラインで実現
- [2023-04-17 Meta AIが高性能なコンピュータビジョンモデルをトレーニングする新しい手法 DINOv2 を発表](https://ai.facebook.com/blog/dino-v2-computer-vision-self-supervised-learning/)
  - ファインチューニング不要で、さまざまなコンピュータビジョンのタスクに活用可能
  - 自己教師あり学習を採用。あらゆる画像の集合体から学習可能
  - 深度推定など、現在の標準的なアプローチでは学習が難しいものも学習できる
  - 続報解説がきている
    - [https://twitter.com/timdarcet/status/1649435730291093506](https://twitter.com/timdarcet/status/1649435730291093506)
  - よくみると、NC-4.0なので非商用かー
- [2023-04-22 Count-Anything: SAMを応用した物体数をカウントするOSS](https://github.com/ylqi/Count-Anything)
- [2023-04-24 SAMが様々な実世界のアプリケーションにおいてどのように機能するかを調査した論文](https://elith.substack.com/i/116461340/論文)
  - SAMの課題（医療画像、低コントラスト、夜間）も挙げられていて興味深い
  - 元論文
    - [[2304.05750] Segment Anything Is Not Always Perfect: An Investigation of SAM on Different Real-world Applications](https://arxiv.org/abs/2304.05750)
- [2023-04-29 Stability AIからDeepFloyd IFが公開](https://note.com/te_ftef/n/nd83eb09a3990)
  - と思ったらこの記事はベースとなっているImagenの記事
  - DeepFloydは学習元丸パクりのAI画像が作れると話題になってる模様
- [2023-05-03 SAM + ResNet(fine-tuning) + ChatGPTで冷蔵庫の具材からレシピ推薦](https://dev.classmethod.jp/articles/chatgpt-recomend-recip)
  - SAMのイメージがまだわかないな。
- [2023-05-04 CLIP ViT-L/14がリリース (Hugging Face)](https://huggingface.co/laion/CLIP-ViT-L-14-DataComp.XL-s13B-b90K)
  - ImageNetで79.2%のゼロショット精度を実現したCLIP ViT-L/14がリリース
  - CLIPを大きく上回り、LAION-2Bで学習させた大型モデル（ViT-g/14）を凌駕
- [2023-05-07 SAMで動画からデータセットを作る例 (DevIO)](https://dev.classmethod.jp/articles/sygment-anything-create-dataset-image/)
  - 追跡やノイズ除去の部分が参考になる
  - そもそもmatplotlibでマウスイベントとかとれるんや、知らんかった…
- [2023-05-07 医療画像解析の分野で広く使用される半教師あり医療画像セグメンテーションの精度を向上させるための新しい方法](https://elith.substack.com/i/119966648/論文)
  - 国際学会CVPR2023に採択されたBidirectional Copy-Paste for Semi-Supervised Medical Image Segmentationについて解説
  - 提案された新しい半教師あり医療画像セグメンテーション手法はBCPはBidirectional Copy-Pasteの略
  - BCPは、ラベル付きデータとラベルなしデータを双方向にコピー＆ペーストすることで、未ラベルデータがラベル付きデータから包括的な共通の意味を学ぶように促すことが目的
- [2023-05-10 Zero-shot Learning網羅的サーベイ：CLIPが切り開いたVision & Languageの新しい世界 - エクサウィザーズ Engineer Blog](https://techblog.exawizards.com/entry/2023/05/10/055218)
  - 網羅的サーベイ
- [2023-05-10 Metaが深度や熱、IMU信号を含めたマルチモーダルImageBindを公開](https://twitter.com/masahirochaen/status/1656176014714880003)
  - 「ImageBind」は、「画像」「テキスト」「音声」「深度(3D)」「熱」「IMU(慣性測定ユニット)」といった6つの異なるモダリティにまたがる共同埋め込みを学習
  - ロボット分野での活用が期待。
  - 凄いとは思うしOpenAI以上と言っているが、入力が以上と言っているのだけなので、まあ用途は限られるかな…
  - その他
    - [Google Colab で ImageBind を試す｜npaka](https://note.com/npaka/n/n22f7980e12bc)
- [2023-07-23 Prompting Large Language Models with Answer Heuristics for Knowledge-based Visual Question Answering - Speaker Deck](https://speakerdeck.com/tereka114/prompting-large-language-models-with-answer-heuristics-for-knowledge-based-visual-question-answering)
  - おもにVQAに関する研究まとめ