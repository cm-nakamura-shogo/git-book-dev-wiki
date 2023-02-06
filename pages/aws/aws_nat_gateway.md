# Amazon NAT Gateway

VPC内のPrivate IPを別のIPに置き換える役割を果たすゲートウェイ。

## 置き換えるプライベートIPが選択可能に(2022-11アップデート)

NATゲートウェイがネットワークアドレス変換に使用するプライベートIPアドレスを選択できるようになった。

発表以前は、NAT Gatewayは作成されたサブネットからランダムなプライベートIPアドレスを選択していた。

そのため、NATゲートウェイとオンプレを接続する際などは、NAT GatewayのサブネットのCIDR全体を許可リストに登録する必要がありました。

この機能拡張により、サブネットからNAT Gatewayの特定のプライベートIPアドレスを選択し、その特定のIPアドレスをパートナーネットワークにallowlistできるようになります。

- 参考
  - [https://aws.amazon.com/jp/about-aws/whats-new/2022/11/amazon-nat-gateway-allows-select-private-ip-address-network-address-translation/](https://aws.amazon.com/jp/about-aws/whats-new/2022/11/amazon-nat-gateway-allows-select-private-ip-address-network-address-translation/)

## NATゲートウェイに複数のIPアドレスを追加することで、一意の宛先への最大44万件の同時接続をサポートするように(2023-02)

同時接続数が8倍になった様子？

- [Amazon increases NAT Gateway’s capacity to support concurrent connections to a unique destination](https://aws.amazon.com/jp/about-aws/whats-new/2023/02/amazon-nat-gateways-capacity-concurrent-connections-unique-destination/)