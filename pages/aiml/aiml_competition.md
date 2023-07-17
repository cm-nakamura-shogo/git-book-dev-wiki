# Kaggleコンペ一覧


## 2021

- [2021-01-21 : 判例の個人情報の自動マスキング | Nishika](https://www.nishika.com/competitions/7/summary)
  - [判例の個人情報の自動マスキング　コンペ振り返り｜Nishika株式会社｜note](https://note.com/nishika_inc/n/n78447a423abe)
- [2021-05-10 to 2021-08-18 : SETI Breakthrough Listen - E.T. Signal Search | Kaggle](https://www.kaggle.com/c/seti-breakthrough-listen/leaderboard)
  - 宇宙人探索コンペ。データは模擬データで異常信号を見つける。
- [2021-06-01 to 2021-09-29 : G2Net Gravitational Wave Detection | Kaggle](https://www.kaggle.com/c/g2net-gravitational-wave-detection/)
  - ブラックホール発生時の重力波を予想するコンペ（疑似データ）
- [2021-06-10 to 2021-08-31 : MLB Player Digital Engagement Forecasting | Kaggle](https://www.kaggle.com/c/mlb-player-digital-engagement-forecasting)
  - テーブルデータ。
  - 推論コードコンペ（9h制限）
- [2021-06-28 to 2021-09-27 : Optiver Realized Volatility Prediction | Kaggle](https://www.kaggle.com/c/optiver-realized-volatility-prediction)
  - 銘柄の短期的なボラティリティ(10分間)を予測する。
  - 推論コードコンペ（9h制限）
- [2021-07-13 to 2021-10-15 : RSNA-MICCAI Brain Tumor Radiogenomic Classification | Kaggle](https://www.kaggle.com/c/rsna-miccai-brain-tumor-radiogenomic-classification)
  - MRI画像から脳腫瘍治療に重要な遺伝子バイオマーカを予想する。
  - 推論コードコンペ（9h制限）
- [2021-08-02 to 2021-09-30 : LearnPlatform COVID-19 Impact on Digital Learning | Kaggle](https://www.kaggle.com/c/learnplatform-covid19-impact-on-digital-learning)
  - 機械学習じゃなさそう？
- [2021-08-10 to 2021-10-08 : Google Landmark Retrieval 2021 | Kaggle](https://www.kaggle.com/c/landmark-retrieval-2021)
  - 画像検索コンペ。ランドマーク画像の検索。
  - 推論コードコンペ（9h制限）
- [2021-08-10 to 2021-10-08 : Google Landmark Recognition 2021 | Kaggle](https://www.kaggle.com/c/landmark-recognition-2021)
  - 画像認識コンペ。ランドマークを認識するが、81K個の多クラス分類。
  - 推論コードコンペ（9h制限）
- [2021-08-10 to 2021-11-02 : NFL Health & Safety - Helmet Assignment | Kaggle](https://www.kaggle.com/c/nfl-health-and-safety-helmet-assignment)
  - 動画からNFLの選手のヘルメットを識別して割り当てるタスク。
  - 入力は画像のみ。推論コードコンペ（9h制限）
- [2021-08-11 to 2021-11-15 : chaii - Hindi and Tamil Question Answering | Kaggle](https://www.kaggle.com/c/chaii-hindi-and-tamil-question-answering)
  - インドの言語のNLUタスク。QuestionからAnswerを予想する。
  - 推論コードコンペ（5h制限）
- [2021-08-16 to 2021-12-06 : Lux AI | Kaggle](https://www.kaggle.com/c/lux-ai-2021)
  - ゲームAIを作るコンペティション

## 2022

- [2022-08-04 DAICC forum ML Competition 製造工程データから破壊検査の結果を事前に予測](https://tech-ai.panasonic.com/jp/blog_page.html?id=20220805)
- [2022-12-15 to 2023-03-14 : Learning Equality - Curriculum Recommendations | Kaggle](https://www.kaggle.com/competitions/learning-equality-curriculum-recommendations)
  - 教育トピックに対してそのコンテンツを割り振るコンペティション。
  - K-12と呼ばれる米国等で用いられている幼稚園〜高校3年生までの教育用カリキュラムにおいて、“topic"と"content"をマッチングすること
  - 一見自然言語っぽいデータセットだが、contentsにはaudioやvideoもあり、マルチモーダル処理が求められるかも。
  - [6位解法](https://www.mcdigital.jp/blog/kaggle-lecr-2023/)
    - BERTによる距離学習を行いtopicとcontentに対するembeddingsを出力
    - 最も類似度が高い上位N(今回は50)個のcontentを出力
    - 一段目の出力であるtopic-contentのペアが本当に正解かをGBDTで予測
    - 2ステージが鉄板で、エラー分析も重要なのだなと言う感想
- [2022-12-27 to 2023-04-05 : Competition Detail - Solafune](https://solafune.com/ja/competitions/7a1fc5e3-49bd-4ec1-8378-974951398c98?menu=about&tab=overview)
  - [1位解法](https://hack.nikkei.com/blog/solafune202304/)
    - 基本
      - バックボーンとして事前学習済みの Swin2SR のモデルを使用（これで4倍となる）
      - 出力部分で Bicubic 補間で 5 倍まで画像を拡大しこれで学習
    - その他
      - Lion Optimizerの使用
      - x4推論したものからx2を学習して縮小
      - データ拡張(超解像分野のデータ拡張手法として有効であるとされている cutblur の論文に記載された手法)
      - Adversarial Weight Perturbation と言われる学習手法
      - 外部データ(過去コンペでも言及されていた練馬区の航空写真データセットを利用)
    - インフラ
      - Google Cloudを使っている

## 2023年

- [2023-01-xx to 2023-03-10 : 材料の物性予測 ~機械学習で材料の研究開発を推進しよう~ | Nishika](https://competition.nishika.com/competitions/bussei/summary)
  - [2023-04-16 Nishikaの材料コンペの2nd place solution解説](https://qiita.com/mi-212/items/694124649d2848a6b559)
  - GNNのアーキテクチャとしてNequIPを採用
- [2023-01-21 to 2023-04-30 : ブルーカーボン・ダイナミクスを可視化せよ！ | SIGNATE - Data Science Competition](https://signate.jp/competitions/936/)
  - 沖縄県全域を対象として、ブルーカーボンの重要な指標となる海草藻場の被度（一定面積の地表面や海底面を覆う割合）を、環境変数や衛星画像をもとに推定
  - [14位解法](https://github.com/upura/signate-jsai2023-bluecarbon)
    - シンプルにGBDT系のモデル
    - Linear Quiz Blending は気になる
- [2023-03-07 to 2023-05-24 : BirdCLEF 2023 | Kaggle](https://www.kaggle.com/competitions/birdclef-2023)
  - Soundscape（環境音）より、どんな鳥がその環境に居るのかを予測します
  - 264種の鳥の存在の予測確率を出すマルチラベルタスクのコンペ
  - [20位解法](https://moritake04.hatenablog.com/entry/2023/05/29/213619)
    - mobileNet v3, efn, efn v2などは現役
    - eca_nfnetは見たことないので新しいのかも
      - https://huggingface.co/timm/eca_nfnet_l0
    - メルスペクトログラムも現役、Augmentation法や前処理も詳細に解説してありありがたい
- [2023-04-19 to 2023-08-21 : CAFA 5 Protein Function Prediction | Kaggle](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction)
  - アミノ酸配列からタンパク質の機能を予測するコンペ
  - データが329MBと小さめなので参加しやすいかも
- [2023-04-11 to 2023-06-12 : Image Matching Challenge 2023 | Kaggle](https://www.kaggle.com/competitions/image-matching-challenge-2023)
  - 参照画像から対象画像の回転と並進を予測するコンペ
  - 用途としては3D再構成に使うのが目的らしい
- [2023-05-10 to 2023-08-09 : Google Research - Identify Contrails to Reduce Global Warming | Kaggle](https://www.kaggle.com/competitions/google-research-identify-contrails-reduce-global-warming)
- [2023-05-10 to 2023-08-10 : Google - American Sign Language Fingerspelling Recognition | Kaggle](https://www.kaggle.com/c/asl-fingerspelling)
- [2023-05-11 to 2023-07-16 : 2023 Kaggle AI Report | Kaggle](https://www.kaggle.com/competitions/2023-kaggle-ai-report/)
- [2023-05-11 to 2023-08-10 : ICR - Identifying Age-Related Conditions | Kaggle](https://www.kaggle.com/competitions/icr-identify-age-related-conditions)
- [2023-05-22 to 2023-07-31 : HuBMAP - Hacking the Human Vasculature | Kaggle](https://www.kaggle.com/competitions/hubmap-hacking-the-human-vasculature)
  - 毛細血管・細動脈・細静脈などの微小血管構造の画像のセグメンテーションが題材
- [2023-07-07 to 2023-09-05 : Finding AI-generated Images - Solafune](https://solafune.com/competitions/05724228-0ac1-4488-a42f-e945f2117632?menu=about&tab=overview)
  - 衛生画像と航空画像の画像生成モデルから生成された画像とオリジナル画像の判別
  - 賞金総額 10,000 USD(1位: $6,000)
  - Stability AIがスポンサー
