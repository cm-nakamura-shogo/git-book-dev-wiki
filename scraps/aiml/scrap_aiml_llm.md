# AIML

## Books

- [2023-07-29 大規模言語モデル入門：書籍案内｜技術評論社](https://gihyo.jp/book/2023/978-4-297-13633-8)

## Articles

- [2023-02-23 TransformerやAttentionの分かりにくい点についてのメモ](https://blog.statsbeginner.net/entry/2023/02/23/174435)
  - これはさすがに今更なのでええやろう
- [2023-04-26 サーバーレスGPU推論（Cerebrium）](https://zenn.dev/fusic/articles/fbafe544fb6301)
  - 1秒単位の課金でA100(80GB)だと$0.001023/secなので、15分で約$1
  - AWS Lambdaが10GBの100分で$1なので確かに安いのかも
  - 安定的に動かすためにはONNIX変換した方がよさそうな言及がる
  - やってみたブログ書いても良いかも
- [2023-05-29 Scikit-LLMの紹介](https://qiita.com/fuyu_quant/items/4d56553d6a6c951bd8f7)
  - こちらの方が詳しい
    - [Scikit-LLM: Sklearn Meets Large Language Models | by Fareed Khan | May, 2023 | Medium](https://medium.com/@fareedkhandev/scikit-llm-sklearn-meets-large-language-models-11fc6f30e530)
    - GPTSummarizerは使えそう
- [2023-05-31 BLOOMのようなOSSなLLMをHugging Face LLM Inference ContainerをSageMakerに展開する](https://huggingface.co/blog/sagemaker-huggingface-llm)
- [2023-07-17 Open-Source Text Generation & LLM Ecosystem at Hugging Face](https://huggingface.co/blog/os-llms)
  - オープンなLLMなどの説明
- [2023-09-06 TIIのFalcon-180BがHuggingFaceで公開](https://huggingface.co/blog/falcon-180b)
  - こちらは5月末に公開されたFalcon-40Bのさらなる大規模版
  - MMLUではLlama 2(70B)やOpenAIのGPT-3.5に匹敵する性能
  - HuggingFaceのSpacesで試すことが可能。日本語も理解・回答してくれる（多少不自然な場合もある）
    - [Falcon-180B Demo - a Hugging Face Space by tiiuae](https://huggingface.co/spaces/tiiuae/falcon-180b-demo)
  - 40B,7BはApach 2.0 Licenseであったが、こちらは特殊なライセンスとなっておりその点は注意
    - [LICENSE.txt · tiiuae/falcon-180b-license at main](https://huggingface.co/spaces/tiiuae/falcon-180b-license/blob/main/LICENSE.txt)
- [2023-09-07 自動運転EV開発のチューリング、日英言語対応のマルチモーダル学習ライブラリ「Heron」と最大700億パラメータの大規模モデル群を公開｜Turingのプレスリリース](https://prtimes.jp/main/html/rd/p/000000034.000098132.html)
  - いろいろなモデルの組み合わせでVision and languageモデルを学習できるライブラリ「Heron」を公開
  - ソースコード部分については研究・商用利用が可能なApache License 2.0で公開
  - 公開した学習済みのマルチモーダルモデル群は、Llama 2-chat、ELYZA-Llama 2、 Japanese StableLMなどをベースにHeronで追加学習を行い、マルチモーダル化させたもの
  - モデルは5種類公開されており、7Bまたは70B(Llama 2ベースのみ)となっている
  - LLaVAのInstruction Tuningで使われた15万件の画像に対する対話データセットを日本語化して学習（LLaVA-Instruct-150K-JAとしてHuggingFaceで公開）
  - モデル自体はそれぞれライセンスが異なるので注意
  - 異常検知をさせたり、画像から道路状況を説明させたりする例が出回っている
  - 以下のSpacesで利用可能
    - [Heronチャットデモ - a Hugging Face Space by turing-motors](https://huggingface.co/spaces/turing-motors/heron_chat_blip)
    - Spaceで使用されているheron-chat-blip-ja-stablelm-base-7b-v0は、CC-BY-NCなので商用利用不可
  - 日本語のマルチモーダルモデルまともに動くものがなかったが、ようやく使えるものがでてきたという印象
- [2023-09-08 OpenInterpreter / ついにAIがガチのアシスタントに!これは凄い、というか凄すぎる｜shi3z](https://note.com/shi3zblog/n/n7eaba88ffe4a)
  - ローカルで動くOpenAIのCode Interpreterみたいなやつ、pipで入れれば使える
  - 勝手にpipで色々なパッケージ入れてくるのは普通にツラいので使い捨て環境でやる方が良さそう
- [2023-09-08 LlamaIndex の VectorIndexAutoRetriever を試す｜npaka](https://note.com/npaka/n/n44a6d7842a5d)
  - クエリからメタデータを自動生成して、クエリ＋メタデータでRetrieveする
  - 多くのベクトルストアはメタデータフィルタにも対応しているため、実用ではこれらを使用する
- [2023-09-04 最近のLLMの学習法のまとめ - SFT・RLHF・RAG｜npaka](https://note.com/npaka/n/n862786604dc3)
  - 単なるまとめ
- [2023-09-11 【ChatGPT】オプトアプトを簡単に行う | 日々、学ぶ](https://take-tech-engineer.com/chatgpt-optout/)
  - お気軽にオプトアウトできる方法が最近追加されたらしい
  - ただしこの方法だと、過去のチャット履歴が見れなくなるため注意が必要
- [2023-09-12 好みのチャットbotを短い文章で作れるツール「Prompt2Model」　米カーネギーメロン大などが開発：Innovative Tech - ITmedia NEWS](https://www.itmedia.co.jp/news/articles/2309/12/news040.html)
  - 数例のプロンプトから言語モデルを作るツールとのこと
  - ModelやDatasetをRetrieverをしててこれでクオリティが出せるのか若干疑問
  - 大規模言語モデルのTrainが必要なので、マシンスペック的に大変な部分は特に改善されるものではない
- [2023-09-12 fine-tuningを使って、どのようなテキストコーパスからでも「知識を埋め込む」方法を紹介する新しいガイド](https://twitter.com/llama_index/status/1701264116311322937)
  - こちらも似たような話をしているが、ある論文をチャンクに分割してQAをGPT-4に作成させる
  - そのQAセットを使ってOpenAIのfine-tuningに適用するフレームワークを提供する予定らしい
- [2023-09-12 LLM開発のフロー | フューチャー技術ブログ](https://future-architect.github.io/articles/20230912a/)
  - 目新しいものはないが分かりやすく書く記事の参考になるな
- [2023-09-12 Transformersライブラリで準備されている量子化方法についての長所、短所を概観しその方式を選ぶべきかのガイドライン](https://huggingface.co/blog/overview-quantization-transformers)
  - Hugging Faceのガイドライン
- [2023-09-12 LLMが巡回セールスマン問題などの最適化問題を解く〜自分自身で優れたプロンプトを作成＆活用〜 | AIDB](https://aiboom.net/archives/55087)
- [2023-09-13 PyTorch FSDPを使ったLlama 2 70Bのファインチューニング](https://huggingface.co/blog/ram-efficient-pytorch-fsdp)
- [2023-09-13 算術タスクでGPT-4を圧倒的に上回るコンパクトなモデル『MathGLM』登場](https://aiboom.net/archives/55122)
- [2023-09-14 LLMのファインチューニングで事実の学習ができないのは本当か？ちょっと実験してみた](https://zenn.dev/ohtaman/articles/llm_finetune_lora)
  - 普通はできる。ちまたで言われているのはOpenAIのfine-tuningの話なので少し対象がずれるという認識
