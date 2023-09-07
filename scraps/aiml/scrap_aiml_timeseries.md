# AIML

- [2023-04-17 1次元の時系列をFFT等を使い2次元にmapするTimeNetを提案](https://arxiv.org/abs/2210.02186)
  - 1次元時系列を複数の期間に基づく2次元テンソル集合に変換することで、時間変動の分析を2次元空間に拡張
  - 短期・長期予測、インピュテーション、分類、異常検知など、5つの主要な時系列解析タスクにおいて一貫した最先端を達成
  - 「FFT等」のところが論文読まないと分からないな
- [2023-09-06 TSMixer：時系列予測のためのAll-MLPアーキテクチャ – Google Research Blog](https://blog.research.google/2023/09/tsmixer-all-mlp-architecture-for-time.html)
  - 長期予測ベンチマークで優れたパフォーマンスを発揮する高度な多変量モデルであるTSMixerを開発
  - 実証結果は、TSMixerが、PatchTST、Fedformer、Autoformer、DeepAR、TFTなどの最新モデルを凌駕する
  - [google-research/tsmixer at master · google-research/google-research · GitHub](https://github.com/google-research/google-research/tree/master/tsmixer)