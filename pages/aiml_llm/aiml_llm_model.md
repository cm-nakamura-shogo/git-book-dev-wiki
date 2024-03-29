# LLM : モデル

## まとめ

- [2023-06-11 ローカルLLMの情報まとめ｜npaka](https://note.com/npaka/n/nd95fba328b65)
- [2023-07-04【令和最新版】対話型AI、ローカル支部最前線レポート - Qiita](https://qiita.com/sald_ra/items/85bf58bee374cc2e5f86)
- [2023-07-06 国産LLMまとめツイート](https://twitter.com/Ina_pfgt/status/1676868630540328960)

## FLAN

- [2023-03-04 Google の FLAN-20B with UL2 を動かしてChatGPT APIのように使ってみる！](https://qiita.com/sakasegawa/items/7394fe68eb0087b3c4a5)
  - デカ言語モデルが手元で動く。A100を使う必要がある。
  - 日本語対応していないため、FuguMTで翻訳している。

## Koala

- [2023-04-05 LLaMAをWeb対話データでチューニングしたKoala-13B](https://twitter.com/sakuragi_zero/status/1643308310807052288)
  - Alpacaとかとの差が良く分からん…
  - 公式
    - [https://bair.berkeley.edu/blog/2023/04/03/koala/](https://bair.berkeley.edu/blog/2023/04/03/koala/)
  - LLaMA系なので商用利用はできない

## Vicuna

- [2023-04-18 VicunaがGPT-4のように画像を入力として処理できるように](https://twitter.com/tikgiau/status/1647767975804452864)
  - MiniGPT-4とうたっており、Gradioを使ったデモも公開されている
- [2023-04-24 vicuna-13bは日本語でも結構性能いいらしい](https://twitter.com/nucode/status/1650354319323979778)
  - 一般のご家庭のGPUマシンでも動作する
- [2023-04-26 vicuna-13bで embedding vectorの計算 (& GPT･RWKVとの比較)｜Kan Hatakeyama｜note](https://note.com/kan_hatakeyama/n/n2fbd81ac1d45)
  - 埋め込みを別ライブラリで実施する記事としては参考となる
  - 比較結果自体は、評価が主観であり、モデル規模もアンフェアな条件なので参考程度
- [2023-04-27 vicuna-13bのデータセットについて](https://twitter.com/npaka123/status/1651435773298880518)
  - CarperAI/vicuna-13b-fine-tuned-rlhfや報酬モデルで使われるデータセットが整理されている
- [2023-04-29 さらにブラッシュアップされたVicuna「StableVicuna-13B」を試す｜はまち](https://note.com/hamachi_jp/n/n60f8663ca898)

## Cerebras-GPT

- [2023-04-12 ColabでCerebras-GPTを試す](https://note.com/npaka/n/n82f74e62c30f)
  - 日本語はダメそう

## Dolly 2.0

- [2023-04-12 商用利用可能なDolly 2.0がDatabricks社からリリース](https://gigazine.net/news/20230413-dolly-2-0-open-instruction-following-llm-for-commercial-use/)
  - 公式
    - [https://www.databricks.com/blog/2023/04/12/dolly-first-open-commercially-viable-instruction-tuned-llm](https://www.databricks.com/blog/2023/04/12/dolly-first-open-commercially-viable-instruction-tuned-llm)
- [2023-04-14 Databricks社のプラットフォームで学習した12Bの言語モデルを使ってみた](https://note.com/masayuki_abe/n/n72f66715a4f8)
  - dolly-v2-12bという名前でHugging Faceに公開。
    - [https://huggingface.co/databricks/dolly-v2-12b](https://huggingface.co/databricks/dolly-v2-12b)
  - 日本語はNGっぽい。

## RedPajama

- [2023-04-17 OSS版LLaMAみたいなRedPajamaプロジェクトが発表](https://github.com/togethercomputer/RedPajama-Data/)
  - LLaMAトレーニングデータセット再現
  - 今のところデータセットのみの話っぽい
- [2023-05-06 RedPajama-INCITEの発表](https://twitter.com/togethercompute/status/1654600390288064513)
  - LLaMAのレシピを可能な限り再現するモデルとインストラクトチューニング版とチャット版を公開
  - npakaさんの記事でも
    - [Google Colab で RedPajama-INCITE を試す｜npaka｜note](https://note.com/npaka/n/nd4b73951a46f)
  - その他の反応
    - [https://twitter.com/jaguring1/status/1654625307541004288](https://twitter.com/jaguring1/status/1654625307541004288)
- [2023-06-06 RedPajama-INCITEのInstructとChat版が公開](https://www.together.xyz/blog/redpajama-7b)
  - 7Bモデルでは最高の性能を出したとのこと

## GPT4All

- [2023-04-19 GPT4All-JがGPTであるLLaMaを除去しApacheとなった](https://twitter.com/sonesuke/status/1648414463517949953)
  - オープン化は急速に進んでいる

## StableLM
- [2023-04-20 Stability AIがLLMとなるStableLMを発表](https://github.com/Stability-AI/StableLM)
  - AWSとの連携は期待が持てる。日本語対応が期待されるところ。
  - OpenAssistantはさっそくStableLMに対応
    - [https://huggingface.co/OpenAssistant](https://huggingface.co/OpenAssistant)
  - ファインチューニング済みモデルもいくつか公開されている
    - [https://twitter.com/haruto_qu/status/1648734352933818370](https://twitter.com/haruto_qu/status/1648734352933818370)
  - 日本語も頑張ってくれるつもりみたい
    - [https://twitter.com/stabilityai_jp/status/1648709992281948160](https://twitter.com/stabilityai_jp/status/1648709992281948160)
- [2023-04-28 Stability.aiがStableVicunaを発表](https://ja.stability.ai/blog/stablevicuna-open-source-rlhf-chatbot)
  - Vicuna系ということはLLaMA系なので商用利用不可
- [2023-08-10 日本語言語モデル「Japanese StableLM Alpha」をリリースしました — Stability AI Japan](https://ja.stability.ai/blog/japanese-stablelm-alpha)

## RWKV

- [2023-04-21 Jpn10%のRWKVが観測](https://twitter.com/meteor_eternal/status/1649361381697929217)
  - いままではOtherという形だったので、日本語に特化している点は期待できる
- [2023-04-22 Google Colab で RWKV-LoRA のファインチューニングを試す｜npaka](https://note.com/npaka/n/ndb1df153aed5)
- [2023-04-23 次世代のRWKVモデルに使用する想定のマルチ言語トークナイザーが公開](https://twitter.com/forasteran/status/1649919025458323456)
  - 日本語の例でも示されており今後に期待できる。
- [2023-04-28 RWVK v10 14bが公開](https://twitter.com/meteor_eternal/status/1651716023605919744)
  - これが商用利用可能なOSSの頼みの綱やで。ホンマに。
- [2023-05-15 RWKVの紹介 - Transformerの長所を生かしたRNN](https://huggingface.co/blog/rwkv)
  - 仕組みや強みなどが詳しく書いてある。Transformersライブラリとの統合も正式にサポート（`pip install rwkv`が不要）
  - ネイティブで非常に長いコンテキスト長をサポートするなど
  - 新しい多言語トークナイザーがリリースされ、今後は多言語対応を進める
- [2023-06-06 RWKVを論文と実装から読み解く](https://zenn.dev/jow/articles/f66d6403b9a509)
- [2023-06-28 Google Colab で RWKV-4-World を試す - RWKVパッケージ版｜npaka](https://note.com/npaka/n/n401dccfadedc)
  - 「RWKV-4-World」は、「Pile」と「RedPajama」で学習した多言語用のベースモデル
  - 多言語用の新トークナイザーが使われている
- [2023-07-14 日本語対応が大きく強化](https://twitter.com/blinkdl_ai/status/1679816885695807489)
- [2023-07-15 Google Colab で RWKV-4-World-JPNtuned を試す - ChatRWKV版｜npaka](https://note.com/npaka/n/n7c89a8df7a8d)
- [2023-07-16 rwkv.cpp を試す｜npaka](https://note.com/npaka/n/n9ffb39a1c32f)

## SpikeGPT

- [2023-05-03 SpikeGPT: より軽量な環境で動かすことが可能な言語モデルの可能性](https://zenn.dev/octu0/scraps/0078b6e9925674)

## OpenLLaMA

- [2023-05-03 OpenLLaMA : LLaMAのApache-2.0実装が動き始めている](https://twitter.com/haoliuhl/status/1653460937897295873)
  - 各所の反応
    - [https://twitter.com/manjiroukeigo/status/1653543983325515776](https://twitter.com/manjiroukeigo/status/1653543983325515776)
    - [https://twitter.com/umiyuki_ai/status/1653506794503942148](https://twitter.com/umiyuki_ai/status/1653506794503942148)
    - [https://twitter.com/_kaiinui/status/1653498780501807105](https://twitter.com/_kaiinui/status/1653498780501807105)

## MPT (Mosaic.ML)

- [2023-05-05 MPT-7Bの発表](https://www.mosaicml.com/blog/mpt-7b)
  - 6万5000トークン使用可能（GPT-4の2倍）
  - 7Bと比較的小さいモデルながら、かなり高性能
  - 日本語を扱える
  - npakaさんの記事でも
    - [Google Colab で MPT-7B を試す｜npaka｜note](https://note.com/npaka/n/nf442fc9f9c8d)
  - その他の反応
    - [https://twitter.com/jaguring1/status/1654613738727804933](https://twitter.com/jaguring1/status/1654613738727804933)
    - [https://twitter.com/forasteran/status/1654609679392346112](https://twitter.com/forasteran/status/1654609679392346112)
- [2023-05-06 MosaicMLのLLMホスティング推論が安価かもという話 (mah_labさん)](https://twitter.com/mah_lab/status/1654769352439386112)
  - いま話題のMPT-7B-Instructの場合は$0.0005/1k tokens
  - OpenAIのgpt-3.5-turboは$0.002/1k tokensなので1/4になる
- [2023-06-26 MPT-30Bが公開](https://www.mosaicml.com/blog/mpt-30b)
  - 参考ツイート
    - [https://twitter.com/ImAI_Eruel/status/1673277752462680064](https://twitter.com/ImAI_Eruel/status/1673277752462680064)
  - MPT-30B-chatというモデルもあるが商用利用できないためこちらは注意
    - [https://twitter.com/sakkusakumura/status/1673833822973214721](https://twitter.com/sakkusakumura/status/1673833822973214721)

## HyperCLOVA (LINE)

- [2023-05-10 ソフトバンク、LINEと和製GPT立ち上げへ](https://www.itmedia.co.jp/news/articles/2305/10/news170.html#utm_term=share_sp)
  - LINEが開発してきた独自の大規模言語モデルHyperCLOVAがキーか。
- [2023-08-14 36億パラメータの日本語言語モデルを公開しました](https://engineering.linecorp.com/ja/blog/3.6-billion-parameter-japanese-language-model)

## OpenCALM (CyberAgent)

- [2023-05-11 サイバーエージェント、独自の日本語LLM（大規模言語モデル）を開発](https://www.cyberagent.co.jp/news/detail/id=28797)
  - すでに13Bまでの開発が完了しており、当社が提供する「極予測AI」「極予測TD」「極予測LP」などAIを活用した広告クリエイティブ制作領域のサービスにおいて活用を始めている
  - まあ言ってるだけなので確認するすべがないが、リソースは本気度が高いので、そうなのかもしれん。
    - [80基の「NVIDIA H100 Tensor コア GPU」※2を活用したAI開発環境](https://www.cyberagent.co.jp/news/detail/id=28484)
  - NVIDIAと協業してたのか、知らんかった。
- [2023-05-17 CA-OpenCALM サイバーエージェント、日本語の大規模言語モデルを一般公開](https://www.itmedia.co.jp/news/articles/2305/17/news096.html)
  - CC BY-SA 4.0で商用利用も可能。サイズは7B。
  - モデルはOpenCALMというやつでなじみないがGPT-NeoXベースで独自の様子？Hugging Faceで公開されている
  - 13Bパラメータまで開発が完了しているらしい。公開されるかな。
  - そのままではチャット用途では微妙か…？
    - [オープンなLLMをDockerで動かす](https://zenn.dev/karaage0703/articles/2b753b4dc26471)
  - npakaさんが試している
    - [Google Colab で OpenCALM-7B を試す｜npaka](https://note.com/npaka/n/n2185b422a2f2)
    - [Google Colab で OpenCALM-7B のLoRAファインチューニングを試す｜npaka](https://note.com/npaka/n/na5b8e6f749ce)

### [2023-05-18 OpenCALM-7Bをdolly-15k-jaでLoRAした例](https://twitter.com/masuidrive/status/1659089478781227008)

### [2023-06-06 Google Colab + trlx で OpenCALM のRLHFファインチューニングを練習する｜npaka](https://note.com/npaka/n/nb8034942b642)

## 株式会社レトリバ

- [2023-05-12 日本語T5モデルの公開｜株式会社レトリバ](https://note.com/retrieva/n/n7b4186dc5ada)
  - 3Bパラメータ(xl)まで対応
  - cc-by-sa-4.0なので商用利用もOK。クレジット表示と改変した場合のライセンス継承が必要。
  - 11Bとなるxxlも公開しそうな雰囲気がある
  - 2023-05-18に再度公開された
    - [https://twitter.com/jnishi/status/1659084719651160066](https://twitter.com/jnishi/status/1659084719651160066)

## Claude

- [2023-05-12 Anthropicのテキスト生成AI「Claude」が100kトークンに対応](https://gigazine.net/news/20230512-claude-token-context/)
  - 平均的な人物は約5時間で10万トークン分の文章を読むことが可能だが、Claudeであれば1分以内にこれらの処理を行える
  - 実際に小説全体をClaudeに読み込ませ、一文を書き換えたうえでClaudeに対して「元の文章と何が違いますか」と尋ねたところ、わずか22秒で正解が出せる
- [2023-07-11 Claude2の発表](https://twitter.com/jaguring1/status/1678778901122916353)

## rinna

- [2023-05-17 rinnaさんも日本語に特化した36億パラメータのGPT言語モデルを公開](https://prtimes.jp/main/html/rd/p/000000042.000070041.html)
  - 同じくGPT-NeoXベースで、MITライセンス
  - npakaさんが試している
    - [Google Colab で Rinna-3.6B を試す｜npaka](https://note.com/npaka/n/ne4a38239f420)
    - [Google Colab で Rinna-3.6B のLoRAファインチューニングを試す｜npaka](https://note.com/npaka/n/nc387b639e50e)
- [2023-07-02 ローカルでも動く！？日本語に特化した強化学習済み対話GPT言語モデルを検証してみる - Qiita](https://qiita.com/tsuno0821/items/e18a1bc6b7e1885f375c)

## Gorilla

- [2023-05-26 ハルシネーションを大幅に減らす言語モデル「Gorilla」が公開](https://gigazine.net/news/20230526-llm-connected-massive-api-gorilla/)
  - 「API呼び出しの記述においてGPT-4の性能を上回るように調整された」なので何かに特化した話らしい

## Falcon

- [2023-05-27 オープンLLMリーダーボードで上位を占めるLLM、Falcon-40B & 7Bをリリース](https://huggingface.co/tiiuae/falcon-40b)
  - リリース当初は商用利用には報酬が必要であったが、Apache 2.0化された
  - LLaMAの代替なるかといったところ（LLaMAは7B～65B）
  - 関連
    - [オープンソースで商用利用可能な大規模言語モデル「Falcon」が登場、オープンソースモデルの中では最高の性能に - GIGAZINE](https://gigazine.net/news/20230606-falcon-open-llm/)
    - [The Falcon has landed in the Hugging Face ecosystem](https://huggingface.co/blog/falcon)

## Aurora genAI (Intel)

- [2023-05-30 Intel、1兆パラメータの科学向けAI「Aurora genAI」を発表](https://twitter.com/shi3z/status/1663492032231522305)

## Orca (Microsoft)

- [2023-06-13 Microsoft AIが「Orca」を発表、GPT-4から複雑な説明のトレースと段階的な思考プロセスを学習する130億パラメータのモデル](https://www.marktechpost.com/2023/06/13/microsoft-ai-introduces-orca-a-13-billion-parameter-model-that-learns-to-imitate-the-reasoning-process-of-lfms-large-foundation-models/)
  - あれGPT-4に乗っかり学習している…？

## phi-1 (Microsoft)

- [2023-06-22 Microsoftがたった13億のパラメーターでGPT-3.5超えのHumanEval50.6％をたたき出す「phi-1」を発表](https://gigazine.net/news/20230622-phi-1-large-language-model-microsoft/)
  - プログラミング能力を評価するためのデータセットであるHumanEvalで50.6％、MBPPで55.5％と、高い精度
  - GPT-4の67％には及ばないが、パラメーター数が1750億のGPT-3.5を上回る

## Ernie 3.5 (Baidu)

- [2023-06-28 Baiduが「GPT-3.5を上回る」AIモデル「Ernie 3.5」を発表 - GIGAZINE](https://gigazine.net/news/20230628-baidu-ernie-3-5/)
  - 中国の検索大手Baiduが、自社のAIモデル「Ernie」の最新版である「Ernie 3.5」を発表
  - Ernie 3.5はOpenAIのGPT-3.5を上回り、中国語能力ではGPT-4を上回ったと主張

## NICT-40b

- [2023-07-04 日本語に特化した大規模言語モデル（生成AI）を試作｜2023年｜NICT-情報通信研究機構](https://www.nict.go.jp/press/2023/07/04-1.html)
  - 現在は、更に大規模な1,790億パラメータにも取り組んでいる
  - 非公開かぁ

## NEC

- [2023-07-06 NECが国産LLM 日本語“トップクラス” - Impress Watch](https://www.watch.impress.co.jp/docs/news/1514419.html)
  - 非公開

## Salesforce

- [2023-06-29 xGenの理論的な話](https://twitter.com/hillbig/status/1674183027046612994)
- [2023-07-02 Google Colab で xGen を試す｜npaka](https://note.com/npaka/n/nf56d2df63e53)
  - 「xGen」は、「Salesforce」が開発した、8Kの文脈をあつかえる7BのローカルLLM
  - 長い文脈をあつかう対話、質問応答、要約が同サイズのモデルと比べ大きく改善されている
  - 日本語も少しできますが、英語の方が精度が高い

## Llama 2

- [2023-07-19 商用可能な Llama-2 がリリース](https://twitter.com/_kaiinui/status/1681341214896058368)
- [2023-07-19 ggml版が早速でている](https://huggingface.co/TheBloke)
- [2023-07-19 llama2のセットアップメモ (ダウンロードと推論)｜Kan Hatakeyama](https://note.com/kan_hatakeyama/n/n7dc20556f55f)
- [2023-07-19 Llama.cpp で Llama 2 を試す｜npaka](https://note.com/npaka/n/n0ad63134fbe2)
- [2023-08-01 Llama 2 の日本語出力性能を評価してみた](https://note.com/lightblue_tech/n/nd996c7d85984)
  - 日本語でチューニングされたLlama 2の情報がまとまっている