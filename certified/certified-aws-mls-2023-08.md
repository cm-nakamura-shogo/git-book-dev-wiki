# AWS Certified (MLS-C01)

### Practice Exam 1 - MLS-C01

- instance_type=localはEstimatorのインスタンス作成時
- モデルが極小値の場合はバッチサイズを小さくする
- ニューラル トピック モデリング「NTM」と潜在ディリクレ割り当て「LDA」は、どちらもドキュメントをトピックに編成するために使用される教師なし機械学習アルゴリズム
- オートパイロットは現在、表形式のデータ形式のみをサポート（JSONは使えない）
- SageMaker Object2Vec アルゴリズムは、高度にカスタマイズ可能な汎用のニューラル埋め込みアルゴリズムです。高次元オブジェクトの低次元の密な埋め込みを学習できます。Object2Vec では、埋め込みを生成するための入力として、類似または異なるオブジェクトのペアが必要

### Practice Exam 2 - MLS-C01 part1: 7/10

- Adaboostはアンサンブル手法
- Kinesis Firehoseを直接分析するのはKinesis Data Analytics
- QuicksightにはMLを使った異常検出が可能で、アラートを通知することも可能

### Practice Exam 2 - MLS-C01 part1: 7/10

- Adaboostはアンサンブル手法
- Kinesis Firehoseを直接分析するのはKinesis Data Analytics
- QuicksightにはMLを使った異常検出が可能で、アラートを通知することも可能

### Practice Exam 2 - MLS-C01 part2: 9/10

- マルチラベルはsigmoid
- DeepAR アルゴリズムは、時系列データを予測するために使用される教師あり学習アルゴリズム

### Practice Exam 3 - MLS-C01 part1: 5/10

- パイプモード
- Data Streams は変換できない
- KNN アルゴリズムは分類/回帰、K-meansはクラスタリング
- RCFは異常検知
- SSE-KMSはSSE-S3に比較して証跡(CloudTrail)を残すことが可能
- SSE-S3では暗号化キーを管理できない
- 右に傾いている == 右の裾野が広い
- F1 = (2*Preci*Recall) / (Preci + Recall)

### Practice Exam 3 - MLS-C01 part2: 5/10

- Rで構築された場合SageMakerのスクリプトモードは使用できない
- Kinesis Data Analytics は異常検出
- SageMaker IP Insights は、IPv4 アドレスの使用パターンを学習する教師なし学習アルゴリズム
- クラスタ数を決めるエルボー法は折れ線グラフ

### Practice Exam 4 - MLS-C01 part1: 6/10

- 「高いバイアス: 過小適合、高い分散: 過学習」らしい？
- SageMaker Neoはエッジ用
- 古いデータは変更しないでください == ボールトロック
- 欠損がカテゴリカルか数値かでアプローチが変わる。カテゴリカルなら列モード(バイアスが入る可能性あり)、深層学習、数値ならkNN。
- XGBoost は、ヘッダーが削除されている必要がある
- AWS Glue FindMatches ML は、データ内の重複を検出できる
- L1 正則化は特徴選択を実行する正則化方法、L2 正則化はすべての特徴が考慮されたままとなる正則化方法、XavierやAdamは正則化ではないという認識らしい

### Practice Exam 4 - MLS-C01 part2: 8/10

- SMDebugRulesは過学習時の通知などが可能
- 推論パイプラインを実行する場合、前処理・予測・後処理コンテナは同じEC2インスタンスである必要がある
- BlazingtextにはWord2Vecとテキスト分類がある

### Practice Exam 5 - MLS-C01 part1: 5/10

- 「デシジョン ツリー」には機能選択が組み込まれています。したがって、相関の強い特徴は強い影響を及ぼしません。
- Amazon Ground TruthはMechanical Turk(オンデマンド労働者)とprivate(自社内スタッフ)に分けられる
- Quicksight ML の洞察は、機械学習の事前知識がなくても、特定の時系列データに関する予測を生成できます。外れ値を削除し、欠損データを事前に補完する

### Practice Exam 5 - MLS-C01 part2: 8/10

- コンテンツ ベースのフィルタリングと協調フィルタリングの違いに注意
- XGBoostは相関を削除しろと言われた（なぜだ…）

### Practice Exam 6 - MLS-C01 part1: 7/10

- kinesis Firehose にはストリームを複数の宛先に送信する機能がない
- Data Streams は手動でスケーリングする必要があるのに対し、Kinesis Firehose はフルマネージドであり、自動的にスケーリングできること
- 外れ値は箱ひげ図とヒストグラム
- MICE 技術は、欠損データの代入に使用される最も最新の技術
