# MLOps

## [MLOps のこれまでとこれから - Speaker Deck](https://speakerdeck.com/asei/mlops-nokoremadetokorekara-eb9ed3f9-3635-4709-8b48-5ccf201c4ae7)

- AWS, Google, Microsoftの３大ベンダが考えるMLOpsとその比較
- 新規のFaireness課題
  - 既知は人種差別など
  - モデル開発者が利益を得て、データ作成者に還元されない構造
  - アノテータが評価されない点も
- 新規のSecurity課題
  - 学術的興味のハックから現実的な攻撃に変化
- データ品質と透明性
  - 再現性の危機
  - データの収集方法だけでは不十分、クラウドソーシングではラベル品質の担保が困難
  - アノテーションのベンダ登場および内製化が進んでいる
  - ラベル誤りを検出するアルゴリズムが必要（Confident Learning）
- Data Perf
  - train dataとtest dataを固定し、モデル改善するのが現状
  - 「モデルとtest dataを固定し、train dataを改善する」・「モデルとtrain dataを固定し、test dataを改善する」が検討
  - これら３つを同時に解決することを模索している

## digdag

- GUIから理解するDigdagチュートリアル
  - https://dev.classmethod.jp/articles/digdag-tutorial-gui

## k8s

- k8s
  - https://qiita.com/Kta-M/items/ce475c0063d3d3f36d5d