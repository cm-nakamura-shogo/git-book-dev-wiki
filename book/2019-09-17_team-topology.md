# チームトポロジー

## まえがき

- チームトポロジーでは、コンウェイの法則を踏まえて、ソフトウェア開発組織の設計に取り組む
- 明確な境界があり、疎結合で、凝集性の高い構造
- ４つのチームタイプ
  - ストリームアラインドチーム
    - 中心となる構造でこの複数のチーム間の依存関係や調整を減らすことが組織の設計
  - 上記の負荷を減らすチーム
    - コンプリケイテッド・サブシステムチーム
    - プラットフォームチーム
  - 新しい技術の学習・調査を支援するチーム
    - イネイブリングチーム

## はじめに

- チームトポロジーは普遍的な公式ではなく、異なる組織での成功例は多くある
- チームトポロジーの狙いは明快なパターンを提供すること、取り入れたり応用が可能なわかりやすいもの
- 一流のソロ奏者向けのメロディではなく、オーケストラを構成するパート譜のようなもの
- PART1ではコンウェイの法則を掘り下げる
- PART2では業界で実績のあるパターンを見ていく
- PART3では組織設計を進化させる方法について扱う

## PART1 デリバリーの手段としてのチーム

- Chapter1
  - コンウェイの法則では、ソフトウェアアーキテクチャーとチームインタラクションを同時に設計する利点を説いている。両者に働く力は同じものだからだ
  - チームトポロジーはチームの目的と責任を明確にし、チーム間の相互関係の効果を向上させる
  - チームトポロジーでは、戦略適応性の実現のために組織を調整しつつ、ソフトウェアシステムの構築においては人間的なアプローチを利用する
- Chapter2
  - 組織はそのコミュニケーションパスを反映した設計を作り出す
  - 組織設計はソリューション探索の制約になり、取りうるソフトウェア設計を限定する
  - 全員が他のすべての人とコミュニケーションするよう求めるのは、混乱のもとである
  - チーム内のフローがよくなるようなソフトウェアアーキテクチャーを選択せよ
  - 明瞭なチームインタラクションだけにコミュニケーションパスを限定することで、モジュール化した疎結合なシステムが生まれる
- Chapter3
  - チームはソフトウェアデリバリーにおける最も効果的な手段である。個人ではない
  - ダンバー数を踏まえて、組織のグループのなかのチーム数を制限する
  - チームの認知負荷の許容量に合わせて、責任を限定する
  - チームごとに明確な責任の境界を作る
  - チームの成功の助けとなるよう作業環境を変える

### Chapter1 組織図の問題

- システムが人間の日々の活動のあらゆる側面に影響を与えており、その影響はますます大きくなってきている。
- 明確な社会工学的デザインがこれほどまでに重要となったことは、かつてなかった。
- 現代のIT組織は、ソフトウェアシステムをすばやく安全に提供、運用すると同時に、成長を続け、ビジネスや規制環境の変化や圧力に適応しなければいけない。
- いまだに多くの組織が人やチームを組織するやり方は、モダンなソフトウェア開発や運用に逆効果となるやり方のまま
  - 組織図やマトリクスに過度に依存して仕事を分割、管理している組織は、速いペースでのデリバリーとイノベーションへの適応の両立に必要な環境を作り出すのに失敗していることが多い。
- これを成功させるには、組織に、安定したチーム、効果的なチームパターンとインタラクションが必要だ。
- 適切なマインドセットと、再現性と適応性の両方を重視するツールがあれば、チームと人を中心に置きながら、安全にすばやく進めることが可能だ。
> - どういう意味だろう？
- 「高品質でインパクトのあるソフトウェアを提供するというゴールをサポートするため、組織構造は、説明責任をうまく調整しなければいけない」
> - どういう意味だろう？
- 「正しい」プロセスに従って「正しい」ツールを使いさえすればチームは成功するとか、チームは交換可能な個人の集まりだと考えてはいけない。
- そうではなく、人と技術を人間とコンピューター、カーボンとシリコンからなる単一の社会工学的エコシステムと考えるのだ。
> - どういう意味だろう？
- 同時に、チームは内発的に動機づけられ、システムのなかで最高の仕事ができる本物の機会を与えられなければいけないのだ。
> - どういう意味だろう？

#### 組織のコミュニケーション構造

- ほとんどの組織では、チームや人を見渡すための「組織図」なるものを必要としている。
- 組織図はソフトウェアシステムの構築という文脈において、特に規制やコンプライアンスの遵守に役立つ。
- だが、アウトカムの不確実性が高く、コラボレーションを重視する状況では、やるべき仕事を分割する基本原則として組織図に頼るのは非現実的
- 疎結合で長続きするチームに頼るしかない。
- 人間は組織図の線でつながっている人たちだけとコミュニケーションするわけではない。仕事を終わらせるのに必要な相手であれば、誰とでも連絡を取る。
- 実際のコミュニケーションの線が組織図に描かれたものと大きく異なる理由だ。
> - 責任境界とコミュニケーションの断絶は違うという点は理解できる
> - CMの組織図ってどんなかんじだろう？

##### 組織図思考は問題

- 代わりに組織は、個人やチーム間のコミュニケーションにおいて、期待する形と現実の形を表すより現実的な絵を描かなければいけない。
- その差が、組織に適しているシステムの種類を理解するのに役立つ
> - 内部定義クラス同士の通信はしんどいことに似ているのか？
> - 上位部署経由で通信するのも設計的にしんどそう。
> - 上位部署クラスは親クラス（抽象クラス）ではない点に注意は必要か。
- 組織図の構造に基づく意思決定は、組織の一部分のみに最適化されがちで、上流と下流への影響は無視される。
- 局所最適化は直接関係のあるチームにとっては役に立つが、顧客への価値のデリバリー全体を改善するのに役立つとは限らない。
- 他に大きなボトルネックが仕事のストリームのなかにあったら、局所最適化の効果はないに等しい場合もある。
  - IaCを導入してもデプロイに必要な取締役会議が週１回のままなら、デリバリーは速くても１週間
- システム思考では全体の最適化に重点を置き、その時点で最大のボトルネックを特定して取り除く、これを繰り返す。
- チームトポロジーでは、新しい状況に素早く対応し、高速かつ安全にデリバリーするのに役立つ、動的なチーム構造とインタラクションモードをいかにして実現するかに焦点を当てる。
- 組織図が仕事の終わらせ方やチームを間のやりとりを忠実に表したものだと考えてしまうと、仕事の割り当てや責任について効果的な判断ができなくなる。
  - ソフトウェアのドキュメントが、実際の開発が始まると陳腐化するのと同様、組織図も常に現実と一致していない。

##### 組織図からの脱却

- 全ての組織に１つではなく３つの異なる組織構造がある
  1. 公式な構造：組織図、コンプライアンス準所を円滑にする
  2. 非公式な構造：個人間の「影響力の領域」
  3. 価値創造構造：個人間やチーム間の能力に基づいて、実際にどう仕事を終わらせるか
- 知的労働組織の成功のカギは、非公式な構造と価値創造構造のインタラクションにあるとしている
> - まだ非公式な構造と価値創造構造が何かイメージがついていない。
- チームに権限を与え、チームを基本的な構成要素として扱うことで、チーム内の個人は、単なる人の集まりとしてではなくチームとして密接に連携しながら進むようになる。
- 一方で、他のチームとのインタラクションモードを明示的に合意することで、期待するふるまいが明確になり、チーム間の信頼関係が育まれる。
> - インタラクションモードとは？今後説明があるか。
- 組織図やマトリクスマネジメントのような単一で静的な組織構造を利用していては、現代のソフトウェアシステムで効果的なアウトカムを生み出せないことが徐々に明らかになってきている。
- 必要なのは単一の構造ではなく、チームの成長やチーム間のインタラクションを考慮に入れた、現在の状況に適応可能なモデルが必要なのだ。
- チームトポロジーではあらゆる種類の組織で、チーム、プロセス、技術の整合性を保つための進化的なアプローチを提供する。
- 組織設計における経験則
  1. やむを得ない理由があるときに設計する
  2. 設計判断のために選択肢を用意する
  3. 適切な時期に設計する
  4. 整合性が取れていない箇所を探す
  5. 将来を見据える

#### チームトポロジー：チームについての新しい考え方

- チームトポロジーはチームについてのサイズ、形、配置、責任、境界、インタラクションを網羅
- ４つのチーム
  - ストリームアラインドチーム
  - コンプリケイテッド・サブシステムチーム
  - プラットフォームチーム
  - イネイブリングチーム
- ３つのインタラクションモード
  - コラボレーション
  - X-as-a-Service
  - ファシリテーション
- インタラクションモードの例
  - 技術やプロダクトの探索段階ではチームの境界がオーバーラップしたコラボレーションが多い環境が重要
  - プロダクトが出来上がった後は逆に非効率的になる
- チーム間の相互関係に積極的に優先順位をつける
> - どういう意味だろう
- 人間てピなアプローチも重視しており、チームの認知容量には尊重すべき上限があることを認めている

#### コンウェイの法則の再評価

- 1968年のメルヴィン・コンウェイの寄稿による
  - 「システムを設計する組織は、その構造をそっくりまねた構造の設計を生み出してしまう」
  - 組織の本当のコミュニケーションパス（価値創造構造）と、結果として得られるソフトウェアアーキテクチャには強い相関関係がある
  - チーム間のコミュニケーション構造を理解し、アーキテクチャが理想的にでも組織モデルに合わなければ、どちらか一方を変えなくてはならない
- 「アーキテクチャの青写真」どおりのソフトウェアを作った経験のある人であれば、アーキテクチャが自分たちを正しい方向に導いてくれるというよりも、アーキテクチャと戦っていると感じたことが何度もあったのを思い出せるはずだ。
> - 実際そうなのかな？
- 逆コンウェイ戦略
  - システムに反映したいアーキテクチャに合うようなチーム構造にするという考え
- ソフトウェアアーキテクチャを独立した概念と捉え、独立して設計可能で、そうすればどんなチームの集まりでも実装できると考えるのは、根本的に間違っている

#### 認知負荷とボトルネック

- チームもチーム全員の認知容量の合計を越えることはできない
- チームの認知負荷について議論することが少ないのは、どんなものなのか、定量化などが難しいからと勘がられる
- 認知負荷を考慮しないと、チームの責任範囲と担当領域が拡がりすぎ、熟達するだけの余裕がなくなり、担当業務のコンテキストスイッチに悩まされる
> - これは感じるな…
- 内発的動機付けの３つの要素が失われる
  - 自律（複数の要求や優先順位を絶えず調整することで失われる）
  - 熟達（多芸は無芸）
  - 目的（広すぎる責任範囲）
- 認知負荷をしっかりと考えるのは、チームサイズを決めたり、責任を割り当てたり、他のチームとの境界を設定したりする上で、とても役に立つ。
- 全体としてチームトポロジーのアプローチでは、変更フロート稼働中のシステムからのフィードバックを最適化する組織設計を提唱している。

#### まとめ チーム構造、目的、インタラクションを再考する

- ほとんどの企業は、ソフトウェア開発を専門分野ごとに分けた人たちが完成させる一種の製造業と見なしており、大規模プロジェクトを事前に計画し、社会工学的な力学はまったく考慮していなかった。
- 従来型の組織の多くはその組織モデルゆえに、アジャイル、リーンIT、DevOpsのメリットを十分に享受できていない。
- 自動化やツールを導入することばかりに注力してしまい、文化や組織面での変化は場当たり的になっている。
- 私たちは組織図ではなく、コンウェイの法則、認知負荷の制限、チームファーストのアプローチを活用しなければいけない。

2023-06-05 : (42/354)