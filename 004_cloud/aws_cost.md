# AWSコスト見積もり

## 公式の試算例

- [https://aws.amazon.com/jp/cdp/](https://aws.amazon.com/jp/cdp/)

## 個別ノウハウ
- NAT Gateway
  - 100GBで50ドルくらい
```
730 hours in a month x 0.062 USD = 45.26 USD (Gateway usage hourly cost)
100 GB per month x 0.062 USD = 6.20 USD (NAT Gateway data processing cost)
45.26 USD + 6.20 USD = 51.46 USD (NAT Gateway processing and month hours)
```

- VPC Endpoint
  - 月で1000円くらい

- Redshift
  - 4時間で1000円くらい

- S3
  - 1TBで25ドル
```
1024 GB x 0.0250000000 USD = 25.60 USD
```