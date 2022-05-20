# reliability


## reliabilityとは

- 障害による中断・停止と障害復旧の影響を軽減するインフラを構成する。
- ポイント
  - 障害復旧の自動化
  - 復旧手順ののテストによる検証
  - 需要変化に応じた水平方向へのスケーラビリティ
    - AutoScalingの設定によるスケーリング自動化
  - キャパシティの推測をやめる
    - 自動で察知しモニタリングしてスケーリングさせる。
  - モニタリングと自動化を進める。

- 3つのポイントと主要なサービス
  - 基盤(IAM, VPC, AutoScaling, ELB, Cloud Formation)
  - 変更管理(CloudTrail, AWS Config)
  - 障害管理(CloudWatch)

### 具体例

- 別リージョンや別AZへのバックアップ
- スタンバイ構成をとり、Route53でフェイルオーバー時の対応をしておく。
  - ホットでもコールドでもよい。

## 事業継続性計画(BCP)

- バックアップからの復元やフェイルオーバー手順を作成し、検証する。
- 実行する運用体制を確保する。

## 高可用性

- 高可用なサービスを利用(S3, ELB, Lambdaなど)
  - S3はイレブン9の高い高可用性
- ユーザー側で設計が必要(EC2, RDS, DirectConnect)

### 非機能要件

- 目標復旧時間(RTO: Recovery Time Objective)
  - いつまでにシステムが復旧するかという目標時間を表す指標。
- 目標復旧時点(RPO: Recovery Point Objective)
  - データが損壊した際に復旧する古さの目標。
- 耐障害性
  - アプロケーションのコンポーネントに組み込まれた冗長性。
- 復元可能性
  - 障害や災害発生時におけるサービス復旧に関わる機能とプロセス、ポリシー
- 拡張性
  - 既存の設計・構成において、アプリケーションの拡張性を確保する能力

### 高可用性とコスト

- 高可用性を挙げるとコストが高まる。
- また構成の複雑さも増す。

### 方針

- サービスの配置（リージョン、AZ、VPC、サブネット設計）
- AWSサービスの利用
  - Route53によるフェイルオーバー
  - ELBによるロードバランサ
  - CloudWatchによるモニタリング
  - Auto Scalingによる自動スケール
  - Lambdaによるスケーリング
  - ElastiCacheを利用したキャッシュアクセス活用

## 単一障害点の排除

- EC2, DirectConnect, RDSを高可用化するためELBやRoute53を使う。
- 単一AZ、単一VPCだとシステムダウンに弱くなる。
- 基本はマルチAZ、マルチVPCのアーキテクチャ設計を実施。
- DBについては以下のように実施する。
  - マスター・スレーブ構成をとり、自動フェイルオーバーで切り替える。
  - リードレプリカで日常的な負荷を分散する。
    - リードレプリカは読み込み専用のDBサーバー
- Elastic IPのフローティング
  - EC2インスタンスに障害が発生した場合、同じパブリックIPをもつ別のインスタンスにIPをフローティング(移動)する。
  - Route53を使って行う。

# ELB

- 複数のEC2インスタンスでの処理を可能にするロードバランサ
- ヘルスチェックを行い、正常なインスタンスのみ利用することも可能

## ELBの特徴

- インスタンスに限らず、IPアドレスをターゲットにした負荷分散も可能
- ヘルスチェックを実施し、正常なインスタンスのみに集中させる。
- public, privateどちらでも使用可能
- ELB自体の負荷に応じてキャパシティを自動増減するスケーリングをするが、これはAWS側でマネージドで提供される。
- 時間に応じたLCU(ロードバランサキャパシティユニット)使用料で課金
  - CLBのみ転送データ単位
  - ALB, NLB, CLBがあるが、CLBはEC2-Classicネットワークで構成されたアプリケーションなどで使われ、後方互換のために残されています。
- Auto Scaling, Route53, Cloud formationなどと連携

## ELBの構成

- マルチAZにインスタンスへのトラフィックを分散する構成が利用される。
- リージョンは跨がれないのでそこは要注意。
- privateなEC2インスタンスに対して設置するインターナルELBを使用することも可能
- publicとつながったELBを構成して、privateなEC2インスタンスにトラフィックを分散することも可能。

## ELBのタイプ

- 3つのタイプがある。

- CLB
  - 古いタイプなため、基本的にはALB, NLBを使用する
  - レイヤ4とレイヤ7に対応しているため、レイヤ4で使いたい場合は、こちらを使用する。
  - 対応するリスナー範囲が広く、TCP, SSL, HTTP, HTTPSに対応
  - IPアドレスが可変で、DNSのみ利用可能

- ALB
  - レイヤ7に対応し、HTTP, HTTPSリスナー対応
  - パスルーティングが可能
  - LCUの時間使用量で課金
  - IPアドレスが可変で、DNSのみ利用可能
  - デフォルトでクロスゾーン負荷分散が有効
    - 分散するAZの各インスタンス数が異なる場合でも負荷を均等に分散する機能

- NLB
  - 高パフォーマンスなロードバランシングを実施する際に使用する。
  - L4レイヤで、NAT型のロードバランサ(戻りトラフィックがNLBを経由しない)
    - CLBとALBはプロキシ型
  - LCUの時間使用量で課金
  - サブネット拡張をサポート
    - サブネットを追加して複数にすることができる。
  - 固定IPのためDNSとIPどちらも利用可能
  - デフォルトでクロスゾーン負荷分散が無効

### CLB

- Proxyプロトコルによる発信先IPアドレス識別
- ELBとバックエンドのEC2インスタンス間で、HTTPS/SSL使用時にサーバ証明書認証を実施
- CLB配下のインスタンスは、すべて同一の機能を持ったインスタンスが必要。
- リクエスト内容を確認して分散先を振り分けるコンテントベースルーティングはできない。

### ALB

- WebScoketとHTTP/2のリクエストを受付
- 1インスタンスに複数ポートを登録可能
- 複数ポートを個別のターゲットとして登録することが可能なため、ポートを利用するECSなどのコンテナのロードバランシングが可能
- ターゲットグループでのヘルスチェックが可能
  - グループ毎にヘルスチェックが可能
- EC2と同様に削除保護ができる
- 加重ロードバランシングが可能
  - インスタンス毎に重みを変える。
  - Route53でも似たようなことができるが、それをALBで実現可能。
- リクエスト内容を確認して分散先を振り分けるコンテントベースルーティングが可能
- URLのパスに基づいてルーティングが可能なパスベースルーティングが可能

### NLB

- 最も高性能なELB
- L4 NATロードバランサーでTCPリスナーに対応（戻りトラフィックがNLBを経由しない）
  - TCP, UDP, TLSのプロトコルに対応
- 揮発性ワークロードを処理し、数百万リクエストを対応できる能力
- VPC外のターゲットを含めたIPアドレスや静的IPアドレスでの登録が可能
  - オンプレミスなども指定できる。
- 複数のポートで各インスタンスまたはIPアドレスを同じターゲットグループに登録可能
- 大規模アクセスが予想される場合にCLBやALBで必要であった事前申請が不要
- ALBとCLBはX-Forwarded-Forで送信元を判断するが、NLBは送信元IPとポートを書き換えないため、パケットからアクセス元を判断可能
- NLBはフォルトトレランス機能を内蔵したコネクション処理を持ち、数か月から数年のオープンなコネクションを処理できる
- ECSサポート
- 各サービスの個別のヘルスステータスのモニタリングのサポート
- サブネット拡張サポート（サブネットを追加できる）

### GLB

- サードパーティー仮想アプライアンスをVPC内にデプロイ、スケーリング、管理を容易にする。
- セキュリティアプライアンス(firewall, IDS/IPS)をVPC内に設置し、GLBを介して冗長化したり、トラフィックを一元的にすることができる。
- そのため、レイヤー３で動作する点も異なる。
- 5タプルまたは３タプル使用し、特定アプライアンスへのスティッキ状態を維持。
- ポート6081のGENEVEプロトコルを使用してアプリケーショントラフィックを交換
- 最大伝送ユニット(MTU)は8500バイト
- GLBエンドポイントにより、VPC境界を超えてトラフィックを安全に交換

- 搭乗前は、ゲートウェイ型のファイアフォールやIPSを設定することがとても複雑で、スケーリングも難しかった。

### ELBの主要機能

- ヘルスチェック
  - EC2インスタンスの正常／異常を確認し、利用する EC2 の振り分けを行う
- クロスゾーン負荷分散
  - 配下のEC2 の負荷に応じて、複数の AZ に跨る EC2 インスタンスに均等に負荷分散を行う
- 暗号化通信
  - SSL/TSL証明書を ELB に設定することで HTTPS または TLS 通信を実施することができる。
- スティッキーセッション
  - セッション中に同じユーザから来たリクエストを継続して同じ EC2 インスタンスに送信する
- Connection Draining
  - インスタンスが登録解除されるか異常が発生した場合に、そのバックエンドインスタンスへの新規リクエスト送信を中止する
- ログ取得
  - ELBのログ取得を有効化すると S3 バケットにログを収集

## ELBの作成

### Target Group作成

- 4つのTarget Typeがある。
  - Instances
    - VPC内のインスタンス
  - IP Addresses
    - VPCとオンプレにも使える
  - Lambda
  - ALB
- target groupを設置するVPCを選択する。
- Protocolは以下から選択
  - HTTP1
  - HTTP2
  - gRPC
- ヘルスチェック
  - HTTP, HTTPSから選択する。
- Advanced health checking settings
  - タイムアウト時間やリトライ回数や間隔などを設定する。
- ターゲットを登録
  - 入れるインスタンスを指定

### ELB作成

- ALBを選択
- 名前を決める
- Internet/Internalを選択
- IPaddress type
  - IPv4, dual(v4+v6)
- VPCを選択
- AZとsubnetを選択する。
  - 同一AZ内の複数subnetは選択できない？？
- SGを選択
  - EC2と似ている、同じものを選択する。
- ターゲットグループとProtocol, Portを選択

### 確認

- ロードバランサ(DNS名)にアクセスすると、2つのインスタンスが切り替わる。
- 片方を落として確認すると、１方にしかアクセスできないことがわかる。

# Auto Scaling

- 負荷が高まった場合に新しいインスタンスを増設してパフォーマンスを向上させる。

## Auto Scalingの説明

### スケーリングタイプ

- 垂直スケーリング
  - スケールアップ/ダウン
    - サーバーの性能をup/downする
- 水平スケーリング
  - スケールアウト/イン
    - サーバー台数をup/downする
- Auto Scalingは水平スケーリングとなる。

### 設定プロセス

- ELBと起動テンプレートを準備する必要がある。

- ELBとターゲットグループを作成
- 起動設定または起動テンプレートの作成
  - 起動するインスタンスタイプなどを選択
  - 起動設定はAUto Scaling専用だが機能がすくない
  - 起動テンプレートの方がバージョニングなどの機能が充実
- Auto Scalingグループの作成
  - 起動設定または起動テンプレートとの紐づけ
  - ロードバランシングを有効化し、ELBとの紐づけ
  - グループサイズの指定
  - 閾値設定
  - スケーリング規模の設定
    - インスタンス数の設定
  - スケーリング方式の設定
    - スケーリングポリシーを選択肢、スケールアウトとスケールインを選択
    - ターミネーションポリシーを設定

### Auto Scalingの構成

- Auto Scalingグループは、特定のVPCのサブネットを指定し、サブネットがあるAZ内にAuto Scalingを紐づける。
- 複数のサブネットを選択し、複数AZにまたがる構成も可能

### グループサイズの設定

- 希望する容量
  - Auto Scalingされていない状態のインスタンス数を設定
  - これを上げることで手動でスケールさせることも可能。
  - Auto Scaling後は、この値が変化することとなる。
- 最小キャパシティ
  - スケールインする際の下限インスタンス数
  - 希望する容量より大きい値にはできない。
- 最大キャパシティ
  - スケールアウトする際の上限インスタンス数
  - 希望する容量より小さい値にはできない。

### ターゲット追跡スケーリングポリシー

- CloudWatchのモニタリングメトリクスを利用したスケーリングを実施する。
- モニタリングの例は以下の通り。
  - 平均CPU使用率
  - 平均ネットワーク入力(バイト)
  - 平均ネットワーク出力(バイト)
  - ターゲット毎のALBリクエスト数
- 基本的にはこれを使うが、使わない場合は手動となる。

### スケーリングポリシーの設定

- 動的スケーリング
  - 簡易スケーリングポリシー
    - ターゲット追跡スケーリングポリシーの通常設定
    - アラーム設定に基づき１段階のスケーリングを実施
  - ステップスケーリングポリシー
    - アラーム超過サイズに基づいて、インスタンス数を動的に調整する、複数段階のスケーリングを実施
- 手動スケーリング
  - 希望容量を手動で調整する。
- スケジュールされたスケーリング
  - 実施日時を指定する。

- スケーリングポリシーの複数組み合わせて利用することも可能

- スケールインを無効にして、スケールアウトのみを有効にすることもできる。
- スケールインの保護機能
  - ？？？

### 通知の追加

- SNSによる通知が可能。

### ヘルスチェック

- ２つのどちらかを利用する。
  - EC2のステータス（runnning以外の状態を以上と判断）
  - ELBのヘルスチェック機能を活用

### 終了ポリシー

- デフォルト
  - AZの選択
    - 一番多いAZのインスタンス数を減らす（同数の場合はランダムで選択）
  - インスタンスの選択
    - 起動設定・テンプレートが一番古いインスタンスを削除
    - 古いインスタンスが複数ある場合は、次の課金が始まるタイミングが最も近いインスタンスから削除。
    - これで絞れなかった場合は、ランダムで削除。
- カスタム
  - AZの選択
    - デフォルトと同じ
  - インスタンスの選択
    - カスタムポリシーに従う。

- ４つのポリシー
  - OldestInstance
    - 古いインスタンスから削除
  - NewestInstance
    - 新しいインスタンスから削除
  - OldestLaunchCOnfiguration
    - 最も古い起動設定により起動しているインスタンスから削除
  - ClosestToNextInstanceHour
    - 次の課金が始まるタイミングが最も近いインスタンスから削除

### クールダウン期間

- スケールインした直後に、スケールアップしたり、更にスケールインすることを防ぐ時間。
- クールダウン期間の例外
  - スケジュールされたスケーリング
  - インスタンスが正常でなくなった場合

### Auto Scalingの挙動

- AZに適切に分散されるようにインスタンス数が調整される。
- 基本
  - 最も少ないAZでインスタンスを起動
  - インスタンスの起動が失敗した場合は、起動が成功するまで別AZで起動する。
- AZ間にアンバランスが発生した場合の挙動
  - 再分散の実施
  - 再分散の挙動
    - 古いインスタンスを終了する前に新しいインスタンスを起動し、一時的にパフォーマンスが低下しないようにする。
    - 最大容量に近づくと再分散が遅くなったり、完全に停止する可能性がある。
    - そのため、一時的に最大容量を増やすなどしてこれを回避する。

### ライフサイクルフック

- インスタンスの起動時または削除時にインスタンスを一時停止してカスタムアクションを実行。
- lambdaと連携した処理も可能。

### トラブルシューティング

- インスタンスのメンテナンス調査時にはAuto Scalingを中断して対応することが必要。
- インスタンス起動失敗
  - Auto Scaling は インスタンスの起動を繰り返し実施し、 24 時間失敗し続けると Amazon 側で停止される可能性がある。
- インスタンスの障害
  - インスタンスの状態が Impaired となると、数分間リカバリーされるかチェックする
  - リカバリーされない場合は新しいインスタンスを起動して、Impaired のインスタンスを終了する。
- トラブルシューティングのステップ
  - Auto Scaling グループを一時的に停止 しないでインスタンスを停止すると新規インスタンスが起動してしまう 。
  - Auto Scaling を停止 して、 調査・復旧し、 Auto Scaling を再開することが基本的な実施方法

### インスタンスをAutoScalingグループに追加

- あとからELBに紐づいたインスタンスをAutoScalingグループに追加することができる。
- インスタンスのアクションで、AutoScalingグループにアタッチすることで可能。
  - nameタグがAutoScalingグループ側の設定に自動で変更されるかもしれない？

### 負荷テスト

```sh
#stressのインストール
wget https://rpmfind.net/linux/dag/redhat/el7/en/x86_64/dag/RPMS/stress-1.0.2-1.el7.rf.x86_64.rpm
rpm -ivh stress-1.0.2-1.el7.rf.x86_64.rpm
rpm -qa|grep stress
stress --version

#stressによるCPU負荷がけコマンド
stress -c 1 -q &
```

# RDS

## RDS概要

### RDSとは

- RDSは様々なデータベースに対応したフルマネージドなリレーショナルデータベース
  - MySQL
  - ORACLE
  - Microsoft SQL Server
  - PostgreSQL
  - MariaDB
  - Amazon Aurora

### AWSにおけるデータベース構築

- EC2にDBを構築
  - 自由に構成が可能だが、構築・運用が手間
- RDS
  - 構築・運用が楽だが、AWS提供の範囲内での利用制限がある。

### RDSの制約事項

- バージョンが限定される。最新版をすぐには使えない。
  - 状況としては最新版をユーザーで検証する必要があるためあまり変わらない。
- キャパシティに上限がある
- OS への ログインができない
- ファイルシステムへのアクセスができない
- IP アドレスが固定できない
- 一部の機能が使えない
- 個別パッチは適用できない

### RDSの特徴

- RDS自体がマネージド型の高可用
- マルチ AZ によるMaster Slave 構成を容易に構築することができる。
  - マスターからスレーブ側に同期レプリケーション
  - スレーブ側に自動ファイルオーバー
- リードレプリカ最大5台（Aurora は 15 台）設置し、 DBの読み取り処理をスケールアウトできる。
- 自動／手動でS3スナップショットを取得して保存管理し、耐障害性を確保
- トランザクションログもS3に保存可能。

### DBインスタンスの暗号化

- 暗号化対象
  - DB インスタンス
  - 自動バックアップ
  - リードレプリカ
  - スナップショット
- 暗号化方法
  - AES-256
  - KMSによるキー管理
  - リードレプリカも同じキーを使用可能
  - 設定可能なのはインスタンス作成時のみ

### スケーリング詳細

- マネージメントコンソールやAPIからスケールアップ可能
  - インスタンスタイプを変更してスケールアップ／ダウンを実施
  - 一時的にインスタンスタイプを大きくして、その後戻すことも可能
  - ストレージサイズは、拡張はできるが縮小はできない

- シャーディング
  - RDSの書き込み処理をスケーリングする。
  - IDでこの範囲はこちらのRDSマスターなど振り分け可能。

### スケーリングのタイプ

- スケールアップ、スケールアウト双方が可能。

- スケールアップの種類
  - インスタンスタイプの変更
    - 様々なタイプを選択可能
    - インスタンスの得意とする領域を決定する要素
  - インスタンスサイズの変更
    - vCPU数やRAMなどが変化する
  - ストレージタイプの変更
    - IOPSなど

- DBインスタンスを起動する際に、選択することができる。

### インスタンスタイプの種類

- 2つの種類がある。
- 汎用
- メモリ最適化
  - 高速データベース、インメモリDBを使用する際に選択

### 汎用インスタンスタイプ

- t2
  - バースト可能な汎用インスタンス
- t3
  - t2の次世代型
- m4
  - バランスの取れたコンピューティング
- m5
  - 最新の汎用インスタンスでm4より優れたパフォーマンス

- t1やm3も選択できるが、古い。

### メモリ最適化インスタンス

- r4
  - メモリ負荷の高いワークロード向けで安価
- r5
  - r4の次世代型
- x1
  - 大規模アプリケーション向け
  - 大容量だがRAM1GBあたりの価格が最も安いインスタンスのひとつ
- x1e
  - 高性能データベース用に最適化されたインスタンス
  - 大容量だがRAM1GBあたりの価格が最も安いインスタンスのひとつ
- z1d
  - クラウドインスタンスの中で最も高速で最大4GHzで動作可能
  - コストは高い

### ストレージタイプ

- 汎用(SSD)
  - GB あたりの容量課金を実施
  - 100～10,000IOPS を実現可能（サイズによって変わる）
- プロビジョンドIOPS(SSD)
  - IO性能がより高い。
  - GB あたりの容量課金を実施＋プロビジョンド済み IOPS 単位の課金
  - 1,000～30,000IOPS を実現可能（サイズによって変わる）
- マグネティック(HDD)
  - あまりリクエストがない用途に使えるかもしれない。
  - 古いタイプでありあまり使用しない。
  
### ストレージ容量の変更

- 増加はできるが、減少はできない。
- Auto Scalingで容量を自動で増加することも可能。

### スケールアウト

- リードレプリカの増設
  - 読み込み専用のインスタンスを増設し、読み込み処理を負荷分散する
- キャッシュの利用
  - ElastiCacheを連携することが一般的。クエリ処理をインメモリで高速に実施可能。
  - MySQLの場合、MySQL Memcached機能を利用してキャッシュを使用し、読み込み処理を高速化できる。
- Auroraへの移行
  - RDS MySQLをAurora MySQLに移行することで性能をアップ利できる。

### リードレプリカの増設

- 最大5台、Auroraは15台
- マルチAZやクロスリージョンとも併用可能
- インスタンスやストレージタイプを異なるものにすることも可能
- リードレプリカからスタンドアロンのDBインスタンスに手動で切り替え可能(Aurora以外)
  - Auroraの場合はプライマリーインスタンスに昇格できる。

### マルチAZ構成

- 高可用性が目的

||Aurora以外|Aurora|
|:---|:---|:---|
|同期方式|同期レプリケーション|非同期レプリケーション|
|アクセス|アクティブなのはプライマリインスタンスのみ|全インスタンスがアクティブ|
|バックアップ|スタンバイから自動バックアップ|共有ストレージレイヤーから取得|
|障害時の切り替え|スタンバイへの自動フェイルオーバー|リードレプリカへの自動フェイルオーバー|

### マルチリージョン配置

- 障害復旧が目的
- 非同期レプリケーションのみ
- Auroraはセカンダリリージョンのものをマスターに昇格可能

### Auroraへの移行

- RDSのMySQLとPostgreはAuroraと互換性のあるバージョンに容易に移行することができる。

## RDSの作成

### DBサブネットグループの作成

- マルチAZ構成するためのサブネットグループを作成する。
- VPCを選択
- AZをチェックして、privateのサブネットを選択

### DBの作成

- 簡単作成の場合、ベストプラクティス設定を使用できる。
- 標準作成の場合、以下を選択する

- エンジンのオプション
  - エンジンのタイプ
    - Aurora, MySQL, MariaDB, PostgreSQL, Oracle, SQL Server
  - エディションの選択
    - MySQL Community
  - バージョンの選択
    - よく使われるのは5.7など、最新は8.0などとなる。
- テンプレート
  - 本番稼働、開発・テスト、無料枠から選択できる。
  - 無料枠ではマルチAZが使用できない。
- インスタンスタイプの選択
- ストレージタイプの選択
- ストレージの自動スケーリングを有効にするか選択できる。
- 可用性と耐久性
  - マルチAZ配置を設定することができる。
  - マルチAZにするとスタンバイインスタンスを作成する。
  - プライマリ、セカンダリを指定することはできない。
- 接続
  - VPCを選択する。
  - さきほど作成したサブネットグループを選択する。
  - セキュリティグループを選択、作成する。
- 追加の設定
  - DBパラメータグループの選択
  - オプショングループの選択
  - バックアップ有効化
  - バックアップ保持期間
  - バックアップ時間の指定
  - 暗号化の有効化
  - 拡張モニタリングの有効化
    - 細かいモニタリングが実行できる
  - ログのエクスポート
    - CloudWatch Logに発行できる(IAMロールは自動で作成される)
    - ログの種類
      - 監査ログ
      - エラーログ
      - 全般ログ
      - スロークエリログ
  - メンテナンス
    - 自動アップグレードの有効化
    - メンテナンス時間の設定
  - 削除保護機能

### プロキシの作成

- lambdaからRDSにアクセスする場合、プロキシが必要となる。

### クエリエディタ

- Auroraサーバレスを使った場合に使用できる機能
- SQLでアクセスができる？

### リザーブドDBインスタンス

- 中長期用の予約したインスタンスをしようすることができる。

### パラメータグループの設定

- DBサーバー自体のパラメータをたぶんこれでさわることができる。

### オプショングループの設定

- DBに対して追加の機能を付加することができる。
- タイプによって追加できる機能が異なる

### カスタムエンジンバージョン

- OracleとSQL Serverのみ、OSなどにアクセス可能なカスタムバージョンがある。

### イベントサブスクリプション

- イベント発生時にEメールで通知するトピックなどを作成できる。

### 証明書設定

- RDSはSSL/TLS証明書を設定することでHTTPS通信が可能
- 証明書が期限切れの場合はコンソール画面で通知される。

### スナップショット

- 共有したり、パブリックで誰かが公開しているスナップショットを見ることができる。
- スナップショットは、指定したS3へのエクスポートなども可能。
  - 以前はS3に保存されるものの、特定のS3はユーザー指定できなかった。
- 復元時は別のDBインスタンスとして起動される。

### 自動バックアップ

- 自動バックアップでもスナップショットとして取得している。
- それ以外にもトランザクションログをバックアップしている。
- トランザクションログが細かい時間間隔で取得されているため、トランザクションログを使って細かい時刻単位で復元できる。

### リードレプリカ

- 別リージョンに作成することも可能。
- マルチAZ構成にすることも可能。
- リードレプリカ専用のエンドポイントが作成される。
- 冗長化にも使うことができ、昇格というアクションを実行する。

### インスタンスタイプの変更

- 変更操作により簡単に実行できる。
- メンテナンス時間に実施するか、即時実行するか選択できる。
- 一時的に変更中のステータスとなる。

### Auroraへの移行

- スナップショットから移行することができる。
- 互換性があるAuroraのバージョンを選択する。
- 比較的大きめなインスタンスタイプしか選択できない可能性がある。
- Auroraはクラスター構成となるため、クラスター内にリーダーインスタンスがある構成となる。