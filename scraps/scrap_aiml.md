# AIML

### [2023-05-24 Hugging Faceがマイクロソフトと協業し、Azure上でHugging Faceのモデルカタログを提供開始](https://huggingface.co/blog/hugging-face-endpoints-on-azure)

- Azure Machine Learning Studio内で直接利用できる新しいHugging Face Hub Model Catalogを構築

### [2023-05-24 Microsoft Build 2023のAI/MLアップデート最速まとめ](https://zenn.dev/microsoft/articles/dbd3119d44faf0)

### [2023-05-17 Cloudflare、エッジアプリにAIをもたらす「Constellation」発表](https://www.publickey1.jp/blog/23/cloudflareaiconstellation.html)

- 画像認識、アノマリ検出、テキスト処理、音声認識など可能

### [2023-05-12 iroiro-lora](https://twitter.com/2vXpSwA7/status/1656920989350105088)

### [2023-05-10 Metaが深度や熱、IMU信号を含めたマルチモーダルImageBindを公開](https://twitter.com/masahirochaen/status/1656176014714880003)

- 「ImageBind」は、「画像」「テキスト」「音声」「深度(3D)」「熱」「IMU(慣性測定ユニット)」といった6つの異なるモダリティにまたがる共同埋め込みを学習
- ロボット分野での活用が期待。
- 凄いとは思うしOpenAI以上と言っているが、入力が以上と言っているのだけなので、まあ用途は限られるかな…
- その他
  - [Google Colab で ImageBind を試す｜npaka](https://note.com/npaka/n/n22f7980e12bc)

### [2023-05-09 信頼されるAIプロダクトを作るポイントの解説 (piqcy)](https://twitter.com/icoxfog417/status/1655593727543373827)

- 利用目的に合わないAIの利用(abuse)、過信による不適切な利用(misuse)をコントロールして、不信による不使用(disuse)を防止する

### [2023-05-08 頭の中に浮かんだ文章の意味を fMRI で解読する驚くべきデコーダーの開発](https://aasj.jp/news/watch/22018)

- 単語単位ではないが、それっぽい埋め込みを生成できるらしい

### [2023-05-07 onoderaさんはTwitterを使っています: 「polarsのvertical concatはcolumnsの順番も揃ってないといけないっぽい」 / Twitter](https://twitter.com/0verfit/status/1655151985988091905?s=12&t=0nszgXsDXAd-L4WiCutIWg)

### [2023-05-07 piqcyさんはTwitterを使っています: 「Amazonのシニアプロダクトマネジャーが、プロダクトマネジメントにおけるAIの用途とを語った動画](https://twitter.com/icoxfog417/status/1655130947069804546?s=12&t=0nszgXsDXAd-L4WiCutIWg)

### [2023-05-07 SAMで動画からデータセットを作る例 (DevIO)](https://dev.classmethod.jp/articles/sygment-anything-create-dataset-image/)

- 追跡やノイズ除去の部分が参考になる
- そもそもmatplotlibでマウスイベントとかとれるんや、知らんかった…

### [2023-05-04 CLIP ViT-L/14がリリース (Hugging Face)](https://huggingface.co/laion/CLIP-ViT-L-14-DataComp.XL-s13B-b90K)

- ImageNetで79.2%のゼロショット精度を実現したCLIP ViT-L/14がリリース
- CLIPを大きく上回り、LAION-2Bで学習させた大型モデル（ViT-g/14）を凌駕

### [2023-05-03 AWS Batch で OpenMPI を使った並列ジョブの実行をやってみた | DevelopersIO](https://dev.classmethod.jp/articles/tried-aws-batch-multi-node-parallel-jobs/)

### [2023-05-03 SAM + ResNet(fine-tuning) + ChatGPTで冷蔵庫の具材からレシピ推薦](https://dev.classmethod.jp/articles/chatgpt-recomend-recip)

- SAMのイメージがまだわかないな。

### [2023-05-02 Liam BranniganさんはTwitterを使っています: 「One important point is checking if your query is running in streaming mode.](https://twitter.com/braaannigan/status/1653323252473774081?s=12&t=0nszgXsDXAd-L4WiCutIWg)

### [2023-04-29 Stability AIからDeepFloyd IFが公開](https://note.com/te_ftef/n/nd83eb09a3990)

- と思ったらこの記事はベースとなっているImagenの記事
- DeepFloydは学習元丸パクりのAI画像が作れると話題になってる模様

### [2023-04-28 音声合成に使用可能な事前学習モデルHuBERTをApache-2.0ライセンスで公開](https://twitter.com/yasyune1023/status/1651893684521287682)

### [2023-04-27 Hugging Face Transformersを使いTensrFlowとTPUを言語モデルの学習方法](https://huggingface.co/blog/tf_tpu)

### [2023-04-22 Count-Anything: SAMを応用した物体数をカウントするOSS](https://github.com/ylqi/Count-Anything)

### [2023-04-19 CAFA 5 Protein Function Prediction](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction)

- アミノ酸配列からタンパク質の機能を予測するコンペ
- データが329MBと小さめなので参加しやすいかも
- 締めは2023-08-21

### [2023-04-17 1次元の時系列をFFT等を使い2次元にmapするTimeNetを提案](https://arxiv.org/abs/2210.02186)

- 1次元時系列を複数の期間に基づく2次元テンソル集合に変換することで、時間変動の分析を2次元空間に拡張
- 短期・長期予測、インピュテーション、分類、異常検知など、5つの主要な時系列解析タスクにおいて一貫した最先端を達成
- 「FFT等」のところが論文読まないと分からないな

### [2023-04-17 Meta AIが高性能なコンピュータビジョンモデルをトレーニングする新しい手法 DINOv2 を発表](https://ai.facebook.com/blog/dino-v2-computer-vision-self-supervised-learning/)

- ファインチューニング不要で、さまざまなコンピュータビジョンのタスクに活用可能
- 自己教師あり学習を採用。あらゆる画像の集合体から学習可能
- 深度推定など、現在の標準的なアプローチでは学習が難しいものも学習できる
- 続報解説がきている
  - [https://twitter.com/timdarcet/status/1649435730291093506](https://twitter.com/timdarcet/status/1649435730291093506)
- よくみると、NC-4.0なので非商用かー

### [2023-04-17 Inferentia2によるHuggng Face Transformersの高速化](https://huggingface.co/blog/accelerate-transformers-with-inferentia2)

- こちらはHugging Face側の記事

### [2023-04-16 Nishikaの材料コンペの2nd place solution解説](https://qiita.com/mi-212/items/694124649d2848a6b559)

- GNNのアーキテクチャとしてNequIPを採用

### [2023-04-14 SAMよりもより広範な機能をもつSEEMが公開](https://twitter.com/forasteran/status/1646829112844259329)

- この界隈がまだよくわからいので、差異をまだ理解できていない。

### [2023-04-14 SAMを利用したZero-shotなPanoptic Segmentation](https://twitter.com/tobiascornille/status/1646812086154960896)

- 「Segment Anything, Grounding DINO, and CLIPSeg.」というパイプラインで実現

### [2023-04-12 MLOps のはじめかた - Speaker Deck](https://speakerdeck.com/asei/mlops-nohazimekata)

- Money Forward社のMLOpsの知見
- StepFunctionsやInferenciaがでてくる
- MLOpsだからと言って新しい技術を採用すると痛い目にあう（これは確かに）

### [2023-04-11 Kaggle: Image Matching Challenge 2023が開始](https://www.kaggle.com/competitions/image-matching-challenge-2023/overview/evaluation)

- 参照画像から対象画像の回転と並進を予測するコンペ
- 用途としては3D再構成に使うのが目的らしい

### [2023-04-11 Passregi CVの現在と取り組んできた改良](https://dev.classmethod.jp/articles/developers-io-day-one-passregi-cv-improvements/)


### [2023-04-10 SparseFormer: 人間の視覚認識に基づいたスパースなプロセスへの挑戦](https://twitter.com/_akhaliq/status/1645278535878049792)

- 現在の視覚ネットワークの多くは、画素やパッチなどの視覚単位を一律に処理する密なパラダイムに従っている
- これを人間の疎な視覚認識をエンドツーエンドで模倣する手法
- 計算コストの大幅な削減が可能
- コードは1,2か月後らしい…

### [2023-04-10 Pandas 2のバックエンドについて](https://blog.amedama.jp/entry/pandas2-dtype-backend)

- NumPyバックエンドだと、Pandas 1と同じ動作となる
- バックエンドを変えることで、整数型の欠損値を表現できるようになっている点は大きいかも

### [2023-04-01 音源分離技術の基礎と動向](https://www.jstage.jst.go.jp/article/essfr/16/4/16_257/_pdf/-char/ja)

- 音源分離について日本語でまとめられている記事

### [2023-03-16 データの Concept drift 問題について - Debug me](https://yukinoi.hatenablog.com/entry/concept_drift)

### [2023-03-08 日本のロボティクスに関する記事](https://www.nature.com/articles/d41586-023-00668-z)

### [2023-03-02 Dropout Reduces Underfitting](https://arxiv.org/abs/2303.01500)

- [https://twitter.com/shriver_light/status/1649395937457094657](https://twitter.com/shriver_light/status/1649395937457094657)
  - Dropoutが過学習だけでなく、学習初期の未学習にも効くことを発見
  - バッチ間の勾配分散を減らし、学習初期だけDropoutすると最終的なlossも削減可能
  - 学習後期だけ使うと汎化性能が向上するという研究

### [2023-02-23 TransformerやAttentionの分かりにくい点についてのメモ](https://blog.statsbeginner.net/entry/2023/02/23/174435)

- これはさすがに今更なのでええやろう

### [2023-02-24 PythonでTableau風 BIツールによる視覚的データ探索をやってみよう 〜PyGWalker〜](https://qiita.com/hima2b4/items/dfdfb77cf3a588f4131a)

- BIツールみたいなことをPythonでやる

### [2023-02-03 自民党AIの進化と実装に関するプロジェクトチーム](https://note.com/akihisa_shiozaki/n/n4c126c27fd3d)

- 松尾さんとかの見解も資料として上がってて面白い
- がその思いとは裏腹に国産LLMを作る話にはならなかったらしい

### [2022-06-09 NN時代のモダンな不均衡データ補正](https://tjo.hatenablog.com/entry/2022/06/09/120000)

- 均衡にしたデータセットで学習して、その後全データセットでチューニングし直す方法があるみたい。
- 界隈ではtwo-phase trainingと呼ばれている
- 題材は、画像データに対する不均衡データに限定されているのかも

### [2019-12-01 Captumを試す](https://qiita.com/gorogoroyasu/items/819ce2613e72ac96d588)

- 機械学習モデルを解釈し、理解するための手法をまとめたライブラリ
- SHAPやGradCAMの話と思えばいい、その他の手法も多くある

### [2013-12-29 ソシャゲ分析講座　基本編（その６）：ソシャゲの「4つのステージとKPI」を理解する - Real Analytics （リアルアナリティクス）](https://analytics.hatenadiary.com/entry/20131229/p1)
