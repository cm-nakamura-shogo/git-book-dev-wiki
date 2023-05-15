# Professional Cloud Developer

## [GKE でマイクロ サービスの構築をする基礎から、高度なトラフィックルーティングと SLO 運用に至るまでの流れを解説 - YouTube](https://www.youtube.com/watch?v=I5Jz6Ay9oBY)

### Kubernetes / GKE概要

- コンテナ本番運用の課題
  - オペレーション（更新、複数のホストにどのように分散配置するか）
  - ネットワーク（コンテナ間通信
  - スケーリング
  - 可用性
- これを解決するのがkubernetes
  - ホスト、スケジュール
  - オートスケーリング、オートヒーリング、ローリングアップデート
  - 拡張性も高い（Custom Resource Definitionで独自機能を追加可能）
- kubernetesのアーキテクチャ
  - コントロールプレーン
    - kube-apiserver（kubectlの送り先）
    - etcd（マニフェストの永続化）
    - kube-controller-manager
    - kube-scheduler
  - ノード
    - kube-proxy
    - kubelet
    - コンテナランタイム
    - Pod
    - kube-dns
- kubernetesのマニフェストで利用される主なAPIリソース
  - Deployment, ReplicaSetとPodが基本的なもの
  - ユーザはDeployment -> ReplicaSetを介してPodに展開する
  - ネットワークはIngress -> Service -> Podという流れ
  - StatefulSetは、ステートフルなアプリを展開するのに使用
  - Horizontal Pod Autoscalerは水平方向のスケール
- GKE
  - Standard : コントロールプレーンがマネージド、ノードはユーザ管理（ユーザのプロジェクトに配置）
  - Autopilot : ノードもGKEがマネージドする
  - Load Balancer、Logging/Monitoring、Network Securityなどとネイティブに統合されている

### GKEへの継続的デプロイ(CD)

- ロケーションタイプ
  - シングルゾーン : コントロールプレーンは1つのゾーンでSLA99.5%
  - マルチゾーン : SLAは同じ。ノードが複数ゾーンに冗長化
  - そのため、クラスタのアップグレード時にマニフェストの適用などができなくなる
- リージョンクラスタ（Autopilotはこちらのみ）
  - コントロールプレーンも複数ゾーンに冗長化されSLA99.95%に
- kubernetesのバージョン選択方法
  - 静的バージョン指定 : バージョンを変更したくないケースに使用。
  - リリースチャンネル : Googleが推奨するベストプラクティスに基づき、コントロールプレーンとノードのバージョニングが自動的にGoogleに管理される。
- リリースチャンネルの種類
  - Rapid : 最新でSLAが除外。どちらかというと新機能の開発・検証用
  - Regular : Rapidの2,3か月後
  - Stable : さらに2,3か月後
- 一般的なデプロイフロー
  - Cloud Code
    - デプロイを支援するIDEプラグインを提供。OSSのBuildpacksやSkaffoldを活用し、ローカルからの開発を簡素化、デバッグを実現。
  - Cloud Build
    - マネージドなCI/CDプラットフォーム、あらゆるCLIをビルドステップとして組み込み可能
    - VMやキャパシティの管理が不要だが、逆にプライベートプールでマシンタイプやVPCを指定できる柔軟さも提供
    - リポジトリへの変更をトリガーに実行
  - Artifact Registory（Container Registryの後継）
    - DockerイメージだけではなくPythonなどのパッケージやOSパッケージもプライベート管理、リージョン指定も可能
    - 脆弱性スキャン、コンテナイメージのスキャンが動作する
    - Binary Authorizationによりポリシーに合うもののみをGKEやCloud Runにデプロイ可能に
  - Cloud Deploy
    - よりCDに特化。1つのクラスタであればCloud Buildのみでも可能だが、ステージング⇒本番などの一貫性を保つ
    - 重要指標の可視化も可能で、DORA4指標のデプロイ頻度とデプロイ時失敗率を可視化
    - 環境変数は、Skaffoldで定義したものを各環境毎に適用することができる

### 複数のアプリを連携

- 2種類の切り口
  - マイクロサービスの論理的な分離（各サービスをNamespaceとして展開）
  - Namespaceの単位でネットワークや権限を制御する
  - クラスタへの分散配置
- リソースの制御
  - 各NodeへのPodの配置を最適化する
- リソースの割り当て
  - 指定しない場合はPodはできる限りのリソースを使用する
  - `kind: Pod`リソースの`spec.containers[].resources.limits`と`spec.containers[].resources.requests`を指定し、Pod毎に設定が可能
  - `kind: KimitRange`リソースの`spec.limits[].max`や`spec.limits[].defaultRequest`にNamespaceとしてPod毎のデフォルト制限を指定可能
- ResourceQuota
  - Namespace単位でリソース上限を制御（クラスタ管理者が管理するイメージ）
  - `kind: ResourceQuota`リソースの`spec.hard.requests.cpu`, `spec.hard.requests.memory`, `spec.hard.limit.cpu`, `spec.hard.limit.memory`という形
  - CPUやメモリ以外でも、`configmaps`, `persistentvolumeclaims`, `pod`, `replicationcontrollers`, `secret`, `services`, `services.loadbalancer`などのリソース数も制限可能
- マイクロサービス毎の権限管理
  - Role-Based Access Control(RBAC)の適用
    - kubernetesのサービスアカウントを特定Podの実行ユーザとして指定できる
    - `kind: ServiceAccount`を定義し、参照される側のNamespaceに`kind: Role`を参照した`kind: RoleBinding`を作成し、subjectsを参照してくる側のサービスアカウントに向ける
    - Workload Identity
      - Google Cloudのサービスアカウント（GSA）とkubernetesのサービスアカウント（KSA）を紐づける機能
      - 開発者はKSAのみを意識するだけで、必要最小限のGoogle Cloudプロダクトへのアクセス管理を可能に
  - ネットワークポリシーの適用
    - 選択したPodのL3L4レベルのネットワークポリシーを定義可能
    - `kind: NetworkPolocy`を定義し、`spec.podSelector.matchLabels.app`でPodを選択し、ingressを`spec.ingress[].from[].podSelector.matchLabels.app`で参照してくる側を設定
    - 実際の適用は、Dataplane v2を利用する
      - eBPFで実装され、ネットワークポリシーが常に有効化されており、マニフェストを展開できる
      - 接続の許可や拒否などの情報のロギングが可能
  - サービスメッシュを適用し、L7トラフィックを認可
    - 特定のパスに対するGETを許可するなどのアプリレイヤのアクセス許可が可能

### Cloud Load Balancing (GCLB) との連携

- ServiceとIngressがGCLDと連携する
- Service
  - 複数Podに対して負荷分散するL4ロードバランサーを提供
  - クラスタ内部・外部向けどちらにもエンドポイントを提供
  - L4のため、GCLBでTCPコネクションは終端せず、１つとなるため、接続先からみた送信元は接続元のクライアント
- Ingress
  - L7ロードバランサーを提供
  - ドメインやパスベースで複数のServiceに負荷分散
  - L7のためSSL通信を終端し、コネクションは２つ貼られるため、接続先バックエンドから見た接続先から見た送信元はロードバランサーとなる
- Multi-cluster Ingress
  - リージョンを跨いだクラスタ間でHTTP/HTTPSのロードバランシングが可能
- Gatewayコントローラ
  - Ingressの次世代コントローラ
  - インフラを管理するクラスタ管理者と、Namespace内を管理するサービス管理者の責任境界を分離
  - 本来クラスタ管理者はルーティングまでは管理したくない
  - また、Ingressのマニフェストでは使えなかったGCLBの機能をフル活用可能に
  - Namespaceをまたがるルーティングが可能なので、各サービスのNamespaceにIngressを作るのではなく、インフラ用のNamespaceにGatewayコントローラを配置する形が可能に

### サービスメッシュによるトラフィック管理

- サービスメッシュとは
  - サービスディスカバリやトラフィック制御、認証認可、通信の暗号化、可観測性などを提供するソフトウェアを指す
  - ビジネスロジックではない、トラフィック制御、認証認可、通信の暗号化、可観測性などをサイドカーとして分離する
  - 各ポッドのコンテナをサイドカー形式で構成し、それをコントロールプレーンで制御する
  - サイドカーにはEnvoyというサイドカープロキシが使われる
- 普及しているOSSのサービスメッシュであるIstioアーキテクチャ
  - Istiodがコントロールプレーンとして、データプレーンで動くEnvoyを管理する
  - Istioにはロギングやモニタリングがないため、PrometheusやGrafanaなどを使いEnvoyと連携して行う
- Anthos Service Mesh (ASM)
  - Istioベースのフルマネージドサービスメッシュ
  - Istiodがクラスタから分離されてGoogle管理となるマネージドコントロールプレーン（MCP）を選択可能
  - MCPではなく、istiodがクラスタに配置される従来型のIn-cluster Control Planeも選択可能
  - CA機能はMesh CAにロギングやモニタリングはCloud MonitoringやCloud Loggingが使用可能
- istioが提供する機能
  - 分散トレーシング
    - Envoyによりrequest IDやTrace Headersを生成し、アプリ側でヘッダを伝搬させられる
    - ヘッダ情報を元に一つの通信に対するトレースが可能に
  - Traffic SplittingによるCanaryリリース
    - マイクロサービス間のルーティングのweightを設定できる
  - ヘッダ情報に基づくルーティング
  - Circuit Breakerによる障害影響範囲の極小化
    - サービス障害の連鎖的な波及を防ぐ
    - 一定期間負荷分散対象から除外するなどが可能に

### SLOをモニタリングする運用の必要性

- kubernetesの基本的なモニタリング
  - ダッシュボードでみれることと、アラートを飛ばす部分を分離して考える
- GKEダッシュボード
  - GKEはCloud Monitoring上にデフォルトでGKEダッシュボードが用意される
  - クラスタ、Namespace、ノード、ワークロード（Deployment / Statefulset）、K8s Service、Pod、コンテナ、それぞれの単位で使用率が確認可能
- Prometheusメトリクスの収集
  - Google Cloudで利用する場合２種類の方法がある
  - Google Cloud Managed Service for Prometheus (GMP)
  - Gloud MonitoringとGKEワークロード指標を有効化する
    - より簡易的に設定が可能でGKEに閉じているのであればこちらを推奨
- SREの３つの基本原則
  - ユーザの信頼性を測ることができる指標を探す必要がある
- SREで重要な概念
  - SLI : モニタリングする指標で、SLOとSLAの特定に利用
  - SLO : サービスレベルの目標
  - エラーバジェット : 許容できる不具合の割合（1-SLO）
  - SLA : サービスレベル保証、契約として対外的に効力を発揮するもの
- 具体的なの例
  - SLIは可用性や（良いイベント / 有効なイベント）、レイテンシなど
  - SLOは目標と測定期間を定める
  - SLOのモニタリング
    - ASMを導入するとEnvoyがサービス間通信で使われるため、レイテンシなどが計測可能に
  - エラーバジェット
    - 1 - SLOで、信頼性レベルと期間の表などで表し、許容可能なエラーを把握する
    - Canaryリリースを利用してエラーバジェットを節約したりすることが可能に
    - エラーバジェットにより、開発と運用チーム間で目標を合意できる
      - 中立的な成果測定
      - エラーバジェットに余裕があればデプロイ頻度を下げずに機能開発に集中、残り少ない場合は安定化など

## [Kubernetes道場のカレンダー | Advent Calendar 2018 - Qiita](https://qiita.com/advent-calendar/2018/k8s-dojo)

### [Kubernetes道場 3日目 - Podについてとkubectlの簡単な使い方 - Toku's Blog](https://cstoku.dev/posts/2018/k8sdojo-03/)

- Podのマニフェスト例

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
```

### [Kubernetes道場 4日目 - Container Objectのフィールドについて - Toku's Blog](https://cstoku.dev/posts/2018/k8sdojo-04/)

- ほぼDockerfile

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:alpine
    imagePullPolicy: Always
    command: []
    args: ["nginx", "-g", "daemon off;"]
    env:
    - name: HOGEHOGE
      value: fugafuga
    ports:
    - containerPort: 80
      protocol: TCP
    workingDir: /tmp
```

### [Kubernetes道場 5日目 - Volumeについて - Toku's Blog](https://cstoku.dev/posts/2018/k8sdojo-05/)

- Volumeはデータの永続化やPod内でのコンテナ間のデータ共有に使用される
- Volumeの種類

```
- emptyDir
- hostPath
- configMap
- secret
- gcePersistentDisk
- awsElasticBlockStore
- csi
- downwardAPI
- nfs
```

- クラウドサービスの場合、awsElasticBlockStore や gcePersistentDiskも選択できる
- volumesで指定し、各コンテナではvolumeMoutsでマウントする

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: date-tail
spec:
  containers:
  - name: date
    image: alpine
    command: ["sh", "-c"]
    args:
    - |
      exec >> /var/log/date-tail/output.log
      echo -n 'Start at: '
      while true; do
        date
        sleep 1
      done
    volumeMounts:
    - name: log-volume
      mountPath: /var/log/date-tail
  - name: tail
    image: alpine
    command: ["sh", "-c"]
    args:
    - |
      tail -f /var/log/date-tail/output.log
    volumeMounts:
    - name: log-volume
      mountPath: /var/log/date-tail
  volumes:
  - name: log-volume
    emptyDir:
  terminationGracePeriodSeconds: 0
```

### [Kubernetes道場 6日目 - Init Container / Lifecycleについて - Toku's Blog](https://cstoku.dev/posts/2018/k8sdojo-06/)

- Init Container
  - コンテナが起動する前に初期化処理を目的として起動することが可能
  - 複数書いてある場合は順次実行
  - 再起動や再実行されることがありえるため、初期化処理を実装する際は冪等性を考慮しなければならない
- Lifecycle（Podのライフサイクル）
  - Pending : Kubernetesによって承認されたが、一つ以上のコンテナが作成されていない状態。ImageのPullやInit Containerの処理中がこの状態にあたる
  - Running : コンテナが作成され、少なくとも1つのコンテナが実行されているか開始・再起動中の状態
  - Succeeded: Pod内の全てのコンテナが正常に終了し、再起動されていない状態
  - Failed : Pod内の全てのコンテナが終了し、少なくとも1つ以上のコンテナの終了ステータスが0以外だったか、Kubernetesによって強制終了させられた場合この状態になる
  - Unknown : 何らかの理由によりPodのサーバーと通信が失敗し、Podの状態を取得できなかった際の状態Podのライフサイクル
- Lifecycle Events
  - コンテナが開始された際とPodが削除される際にHookして任意の処理を実行することが可能
  - postStart : コンテナが作成された後、即座に実行される。このHandlerが失敗した場合終了させ、 restartPolicy に従い再起動させる
  - preStop : コンテナが終了される前に実行される。コンテナのルートプロセスに対して SIGTERM が送出される前にこのHandlerが実行される。
- Lifecycle Handler
  - postStart や preStop に指定できるHandler
  - exec : コンテナ内でコマンドを実行
  - httpGet : HTTPのGETリクエストを発行

#### [Kubernetes道場 7日目 - Resource Requirements / Security Contextについて - Toku's Blog](https://cstoku.dev/posts/2018/k8sdojo-07/)

- Resource Requirementsの例

```yaml
resources:
  requests:
    cpu: 100m
    memory: 64Mi
  limits:
    cpu: 2
    memory: 1Gi
```

- Security Contextで設定可能なもの
  - DAC(Discretionary Access Control)による権限制御。ファイルのようなオブジェクトに対してUser ID(UID)やGroup ID(GID)を元に設定する
  - SELinuxのコンテキストの適用
  - 特権モードの設定
  - Capabilityの付与
  - 特権昇格の有無
  - AppArmor / Seccompのプロファイルの適用

### [Kubernetes道場 8日目 - ReplicaSet / Deploymentについて - Toku's Blog](https://cstoku.dev/posts/2018/k8sdojo-08/)

- ReplicaSetについて
  - 直接使用することは少ないが、次に出てくるDeploymentを抑える上で理解が進む
  - ReplicaSetは指定された数のPodを複製し、実行する
  - 要点としては以下の3つだ。
    - replicas : Podの複製数
    - selector : Label Selector
    - template : Pod Templateを指定、ReplicaSetで複製するためのPodの雛形を指定する
- ReplicaSetの例

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx
        name: nginx
```

- Deploymentについて
  - 以下の機能を提供する。
    - PodのRolling Update
    - Rolloutの履歴を保持
    - Rollback
  - 実際のところPodを直接管理しているのではなく、ReplicaSetを管理する
- Deploymentで抑えるべきフィールドは以下の物がある。(他はReplicaSetと同じ)
  - minReadySeconds : Podが作成されてから使用可能な状態になるまでの待ち時間を指定
  - paused
  - progressDeadlineSeconds : Deploymentの処理時間がこの時間を超えた場合、 処理を失敗とする（デフォルト600秒）
  - revisionHistoryLimit : リビジョンの履歴の保持する数を指定（デフォルト10）
  - strategy :Podを置き換える際の戦略をRecreateやRollingUpdateから指定（デフォルトはRollingUpdate）
- RollingUpdateの設定例

```yaml
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: 50%
    maxUnavailable: 10%
```

### [Kubernetes道場 9日目 - Serviceについて - Toku's Blog](https://cstoku.dev/posts/2018/k8sdojo-09/)

- Serviceには4つの種類（`spec.type`）がある。
  - ClusterIP : 一番基本となるサービス。クラスタ内部でポッドにアクセスを振り分け。クラスタ内でのみ疎通できる仮想IP。None を指定するとHeadless Serviceを作成することが可能。
  - NodePort : 外部から疎通できるサービス。あらかじめ指定したポートでアクセスする。振り分け先はClusterIPサービスとなる。
  - LoadBalancer : GKE内でのTCPロードバランサの仕組み。ワーカーノードのNodePortを宛先としてバランシングする
  - ExternalName : 外部のサービスに対してのエイリアス(別名)を作成
  - Headless：ポッドのIPアドレスを返却する仕組み
- ClusterIP / NodePort / LoadBalancer はそれぞれ拡張されている形で実装


## Cloud Run

- コンテナ化アプリを実行するためのフルマネージド環境
- GKEと比較
    - 上位のレイヤまで運用管理が不要で、１つのDockerfileで構築できるアプリケーションがユースケース
    - GKEはより柔軟にストレージやネットワーク構成が可能で、コンテナ同士の通信が必要な場合はGKEが良い
- App Engineとの違いは、コンテナかどうかという点
- デプロイ方法
    - イメージのURLを指定
        - Cloud Runからアクセス可能なストレージにビルド済みイメージを格納してURLを指定
    - ソースリポジトリを指定
        - Dockerfileを用意してCloud Buildを使用してデプロイ
        - ソースレポジトリには、GitHub、Bitbucket、Cloud Source Repositoriesが指定可能
- 料金
    - 実行時に使用したCPUやメモリ、下りネットワークの使用量
    - リクエスト数に応じた料金
    - リクエストがないときは、自動でインスタンス数を0に下げることが可能で無課金できる

## Cloud Functions

- 小さなコードのスニペットを開発し、実行することを基本とするサーバーレスサービス
- HTTPリクエストやGoogle Cloud の各種サービスのイベントをトリガーに、関数を実行するサーバーレスサービス
- Cloud Storageなどにファイルのアップロード等あらかじめ登録した操作が行われた際に自動起動可能
- あくまで小規模な機能を実行するサービスという位置づけ
- フロントエンドサービスのバックエンドプログラムのプラットフォームとして選択することも多い
- 2022-08-22に2nd genがGAとなり、Cloud Runベースとなった
    - 使用可能なリクエスト処理時間やインスタンス規模がパワーアップ
- デプロイ方法
    - gcloudコマンド、コンソールからデプロイ
    - GitHub、Bitbucketからのデプロイ
- 料金
    - 関数の実行時間、実行回数、ネットワーク（下り）でそれぞれ課金

## App Engine

- アプリとバックエンド向けのサーバーレスアプリケーションプラットフォーム
- 設定ファイル（YAML形式）を書き、コマンドを1つ実行するだけでデプロイ
- デプロイはBlue-Green デプロイメントにもとづいて行われる
- 自動でスケールするWebアプリケーションを簡単に構築可能
- ２種類の環境
    - スタンダード環境
        - 低コスト運用を目的とした環境。制限は多いが、最小インスタンス数を0にすることも可能
        - 対応言語は、Python、Java、Node.js、PHP、Ruby、Goのみ
        - SSH接続不可
    - フレキシブル環境
        - 任意の言語を使用可能で、SSH接続も可能。
- 複数のyamlから構成する
    - app.yaml
        - アプリケーション全体の仕様が記載
    - cron.yaml
        - スケジュールされたジョブを実行するための仕様が記述
    - dispatch.yaml
        - ルーティング・ルールを上書きするためのもの
    - index.yaml
        - 複数の属性を参照する複雑なクエリ用のインデックスを記載
- アプリケーションはステートレスである必要があるため、セッション管理には Redis や Memcached といったインメモリデータベースを利用するというアーキテクチャが、前提として設定されることが多い。
- Memorystore
  - App Engine (Standard) から Memorystore へ接続: サーバレス VPC アクセスが必要
  - App Engine (Flexible) から Memorystore へ接続: App Engine が authorized network にいる必要あり

## Cloud Storage

- ライフサイクルマネジメント機能、署名付き URL
- Cloud Storage + 外部 HTTP ロードバランサー + Cloud CDN 有効化 のようなアーキテクチャが可能

## Firestore

- モバイルアプリや Web アプリのバックエンドデータベースとして利用できるマネージドな NoSQL データベース
- クラウドネイティブなドキュメント型のNoSQLデータベース
- クライアントからの直接アクセスが可でWebやモバイルアプリ、IoTアプリに使用
- コレクションやドキュメントという概念でデータを保存し、柔軟なデータ検索が可能
- ドキュメントの読み書きに対してトランザクションを実行するので、データ整合性を保持可能
- リアルタイム同期
    - 複数のデバイスによるリアルタイム同期が可能
    - オフライン時には、ローカルストレージに永続化し、オンライン復帰時に同期
- ネイティブモードとDatastoreモードがある
- ネイティブモード
  - ドキュメント志向データベースであることから、テーブル、カラム、レコードといった概念ではなく、「 ドキュメント 」「 コレクション 」という概念
  - モバイルアプリを想定しており、通信が切れても通信が回復した際に同期 を取るようにすることが可能
- Datastoreモード
    - 一般的なキーバリューストアと違いエンティティグループ仕組みでデータ同士を紐付け可能
    - すべてのクエリで強整合性を保証し、更新直後から最新であることが保証
    - 以前のDatastore単体のサービス時はクエリ種類により結果整合性となっていた
    - 以下の場合はDatastoreを選択可能
        - クライアントライブラリが不要
        - リアルタイム機能が不要
- 大規模なバイナリファイルを効率的に処理するのには向かない
- コマンド例
    - バックアップをバックグラウンド実行
        - `gcloud datastore export gs://my-datastore-backup --async`

## Cloud SQL

- MySQLやPostgreSQL、SQL Serverをフルマネージド環境として提供するサービス
- バックアップやレプリケーション、暗号化、容量増加を簡単に実施可能
- MySQL、PostgreSQL、SQL Serverからの移行が可能
- 柔軟なスケーリング、すばやいプロビジョニング
    - ああ
- セキュリティの仕組み
    - 暗号化、プライベート接続、ユーザー認証
    - テーブルごとのアクセス制御も可能
- マシンタイプ
    - 共有コア、軽量、標準、ハイメモリの４種に加えてカスタムがある
    - SQL Serverでは共有コアが使用できない
    - 各タイプで、複数のスペック（vCPU・メモリ）が選択可能
- 料金
    - マシンタイプ、ストレージ、ネットワーク単位で課金
    - 共有コアの場合は、マシンタイプではなく、インスタンス料金となる
    - SQL Serverの場合は、上記に加えてライセンス料金が必要
- ロケーション
    - リージョン、ゾーンを選択する
    - リージョンは作成後変更不可、ゾーンは変更可能
- 接続方法
    - パブリックIPの場合
        - 接続元のIPの登録が必要
        - 複数の接続元がある場合は、Cloud SQL Auth Proxyを使用
    - プライベートIPの場合
        - 同じVPCや共有VPC、Cloud VPNやCloud Interconnectで接続したオンプレから接続可能

## Cloud Spanner

- グローバル分散機能を備えたクラウドネイティブなRDB
- 無制限なスケーリングが可能
- 世界規模でトランザクションの一貫性を確保可能
- マルチリージョナルの構成で99.999%（ファイブナイン）の可用性
- 負荷やデータサイズにもとづいて自動的にシャーディング（水平分割）を実施
    - シャーディングとは、データを複数のノードに分散して保存し、スルー プットを上げる手法
- 制約
    - 自動採番機能が実装されていない。
    - 単調に増加するシーケンシャルな値を主キーとして使用することは推奨されておらず、ランダムなUUIDが推奨
        - 主キーの値に応じてデータを分散保存するため、シーケンシャルな主キーではデータの偏りが発生
    - テーブルごとのアクセス制御は不可
        - IAMによるデータベースレベルでのアクセス制御のみをサポート

## Cloud Bigtable

- 列指向でキーバリューストア型のNoSQLデータベース
- Cloud Bigtableは、ペタバイト規模のNoSQLで、特定のクエリに最適化された行キーを持つカラムファミリー・データベースです。歴史的、時間的なデータの保存に用いられ、この要件に応えるものです。
- 低レイテンシ、高スループットが特徴で、BigQUeryよりも低レイテンシが特徴
- IoT で求められる高速の読み書きなどに対応
- バイナリファイルの保存には制限があるため適さない
- Google検索やYoutube、Googleマップなどのサービス基盤にも使用
- HBase API規格をサポートし、HBaseからの移行が可能
- Hadoopなどを利用している場合は、移行に関わる変更が少なくて済む
- ノード追加により再起動なしでスケールが可能

## Cloud Pub/Sub

- イベント取り込みと配信を行うための非同期なメッセージングサービス
- ストリーミング分析パイプラインを構築する際のデータの受け口として利用
- 送信側は受信側を意識することなく処理を行えるため、受信側のシステム変更や障害に強い
    - そのため、マイクロサービスのアプリケーション同士の連携にも使用可能
- Publisher、Subscriberには、Google Cloudサービス以外にIoT機器やオンプレシステムも使用可能
- 複数サーバーに大量のタスクを効率的に、スケーラブルに割り当てるアーキテクチャにも使用
- ack-deadline
    - subscriberのackが無い場合、そのsubscriberには再度配信する。その待ち時間の設定値

## Cloud Build

- CI/CDのためのビルド環境
- コンテナのビルドも可能
- ほかのGoogle Cloud サービスを利用する際に、自動的にCloud Build が使わ れるケースもある
    - たとえば、App Engine にデプロイする際は、自動でCloud Build が起動
    - このように自動的に使われるケースでも、コンソールから実行状況を確認
- ソースリポジトリが必要でGitHubやBitbucket、Cloud Source Repositorieと連携可能
    - ソースリポジトリにpush すると、自動的にCI/CD の処理が行われるといっ た自動化も可能
- トリガーの例
    - 指定したソースリポジトリのブランチへpush する
    - 指定したソースリポジトリに新しいタグをpush する
    - 指定したソースリポジトリにpull リクエストを作成する
    - 手動実行
- マシンタイプを指定可能で、料金がそれに応じて変わる

## Cloud Monitoring

- 豊富なメトリクスでインフラの監視を行うサービス
- 予算アラートを受信する電子メール受信者を定義するために、最大5つのCloud Monitoringチャネルを設定することができます。
- アラートの通知先
    - メールやチャットツールをはじめとする複数のサービス選択可能
    - また、通知先にwebhookも指定可能
- マネージドではないサーバーにエージェントを導入することで、指標をCloud Monitoringに集約可能
    - たとえば、Compute Engineインスタンスの場合、Monitoring API経由である程度の指標を収集できるが、エージェントをインストールすると、より詳細な情報を収集
    - エージェント無し
        - CPU使用率、ネットワーク送受信量、ディスクIO
    - エージェントあり
        - 上記に加え、ロードアベレージ、TCP接続数、ディスク使用率、メモリ使用率
    - collectdをベースとしたstackdriver-agentが使用

## Cloud Trace

- 分散システムにおけるパフォーマンスを把握するために使用
- リクエストごとに詳細なレイテンシ情報を分析する、またはアプリケーション全体のレイテンシを確認することができます。
- Cloud Run、Cloud Functions、App Engineは自動的に測定され、それ以外はライブラリを用いて最小限の設定を行います。

## Cloud Profiler

- 統計を目的として本番環境アプリケーションから CPU 使用率とメモリ割り当てに関する情報を継続的に収集する、オーバーヘッドの少ないプロファイラ

## Cloud Debugger

- 実行中のアプリを停止したり遅らせたりすることなく、任意のコードの場所でアプリケーションの状態を検査できる
- テスト、開発、本番など、アプリケーションのあらゆるデプロイで使用できます。
- 2023年6月以降に非推奨となる予定

## Cloud IAP（Cloud Identity-Aware Proxy）

- Google Cloudが提供するフルマネージドのリバースプロキシ
- IAPを経由してVPCにある各種リソース（Compute Engineなど）にアクセス可能
- 参考
    - 踏み台サーバはもういらない。IAP(Identity-Aware Proxy)の便利な使い方
        - [https://blog.g-gen.co.jp/entry/login-your-vm-with-iap](https://blog.g-gen.co.jp/entry/login-your-vm-with-iap)

### Cloud Endpoints

- APIデプロイと開発管理のためのサービス
- 認証、割り当て / レート制限、指標を提供

## PCD模擬試験

- 75%くらいの正答率
