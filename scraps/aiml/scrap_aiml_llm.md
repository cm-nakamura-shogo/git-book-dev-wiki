# AIML

## Books

- [2023-07-29 大規模言語モデル入門：書籍案内｜技術評論社](https://gihyo.jp/book/2023/978-4-297-13633-8)

## Articles

- [2023-02-23 TransformerやAttentionの分かりにくい点についてのメモ](https://blog.statsbeginner.net/entry/2023/02/23/174435)
  - これはさすがに今更なのでええやろう
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