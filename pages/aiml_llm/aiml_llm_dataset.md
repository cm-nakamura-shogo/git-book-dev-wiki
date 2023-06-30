# LLM : データセット

### [2022-03-03 JGLUE](https://twitter.com/shunk031/status/1670589712615219200)

### [2023-04-13 Alpacaフォーマットの日本語データセットが CC BY-SA 3.0で公開](https://huggingface.co/datasets/kunishou/databricks-dolly-15k-ja)

- 商用利用も可能なAlpacaのデータセット
- これを元にしたLLMが今後活発になるのでは

### [2023-04-16 OpenAssistantの発表](https://twitter.com/omarsar0/status/1647339407173664772)

- みんなで作るInstructGPTという位置づけ
- リリースにはモデル、データセット、チャットインターフェイスが含まれている
- データセットOASST1をApache 2.0で公開している
  - [https://twitter.com/_philschmid/status/1647288182252228612](https://twitter.com/_philschmid/status/1647288182252228612)

### [2023-05-06 OpenAssistantのオープンソースデータセットOASST1の日本語翻訳版が公開 (クニえもんさん)](https://twitter.com/kun1em0n/status/1654781915315191813)

- 自動翻訳なので元言語がマイナーな言語は除外することを推奨されている

### [2023-05-19 日本語翻訳したデータセットhh-rlhf-49k-ja, cnn_dailymail_27k_jaが公開 (クニえもんさん)](https://twitter.com/kun1em0n/status/1659394751949582336)

- hh-rlhf-49k-ja
  - Anthropicのデータセット hh-rlhfのうち、Mosaic MLのMPT-7B-Instructの学習に使われているものを抜粋して翻訳したもの。
  - 日本語DollyデータとマージすればMPT-7Bの学習データセットに
- cnn_dailymail_27k_ja
  - CNNとDailymailが公開しているニュース要約コーパスで30万レコードのうちの一部を抜粋して翻訳

### [2023-05-29 SEAHORSE: 多面的に要約を評価するツール・大規模データセット](https://twitter.com/AIBoom_net/status/1663043297596813319)

- 6つの軸に沿った評価済み要約96k個のデータセットで、「要約システム」や「要約そのもの」を評価する技術に貢献する
- 要約を評価する軸は以下の6つ。
  - 理解がしやすい、繰り返しになっていない、文法が正しい、正確、重要なポイントを抽出している、簡潔である
- 日本語訳して流用すると良いかも

### [2023-06-13 SlimPajamaの発表](https://twitter.com/cerebrassystems/status/1668357494782001152)

- RedPajama-1Tのオープンソース、クリーニング、重複排除バージョンが公開