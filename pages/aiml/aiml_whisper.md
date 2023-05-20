# Whisper

### [2023-05-11 Whisper JAXのデモがHugging FaceのSpaceにて公開](https://twitter.com/sanchitgandhi99/status/1656665496463495168)

### [2023-04-21 faster-whisperてのもあるらしい](https://zenn.dev/ryoppippi/articles/b66fa477c1c3af)

- OpenAI 公式のモデルを軽量化、独自の最適化により、最大 4 倍の高速化を実現
- 軽いと評判の Whisper.cpp よりも高速に動作（ただしメモリは若干多め）
- Whisper.cpp と違って、GPU による高速化の恩恵が受けられる

### [2023-04-21 Whisper JAX : Whisperを70倍高速化を観測](https://twitter.com/currypurin/status/1649402118699360258)

- 一時間の音声を15秒で書き起こす
- なおGPU, TPU駆動が前提

### [2023-03-28 pytorch2 + ROCm で RWKV(LLM Chatbot) と Wisper 動作確認メモ](https://zenn.dev/syoyo/articles/12c649cfa34ea0)

- ROCmが良く分からんけどAMD GPUで動かす仕組みかな

### [2023-03-11 Slack上でOpenAI社のWhisper APIで文字書き起こしするSlackBot作成](https://qiita.com/ina111/items/1a7c3aac1ca02259783f)

- slack_boltを使っている
- 実装の多少参考にはなるはず。

### [2022-12-05 音声認識モデル Whisper の推論をほぼ倍速に高速化した話](https://qiita.com/halhorn/items/d2672eee452ba5eb6241)

- API版ですら1時間のデータに少し時間がかかるので、課題になる場合はここら辺を見る必要がある。