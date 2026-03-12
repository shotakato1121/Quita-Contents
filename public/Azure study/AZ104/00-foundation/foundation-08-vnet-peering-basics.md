---
title: "AZ-104 学習ログ Day8：VNet Peering の基本"
tags: [Azure, AZ104, 学習ログ, VNet, Peering]
private: false
updated_at: '2026-03-07T11:01:29+09:00'
id: c1cb65ff3e321f95c586
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day8：VNet Peering の基本

## はじめに
VNet は独立したネットワークとして作成されるため、VNet 間の通信には接続手段が必要になる。今回は VNet Peering を整理する。

### これまでに学習した内容
- VNet / Subnet / NSG の基本
- NSG のルール設計

## 本文
### なぜ VNet 同士を接続するのか
VNet は独立したネットワークのため、別 VNet のリソースとはそのままでは通信できない。そこで VNet 同士を接続する仕組みが必要になる。

### VNet Peering とは
VNet Peering は 2 つの VNet を接続する仕組み。設定すると相互通信が可能になる。

### 通信経路
Peering の通信は Azure バックボーンネットワークを通る。インターネットを経由しない。

### アドレス空間の条件
Peering を設定するには VNet のアドレス空間が重複していないことが必要。

```
VNet-A 10.0.0.0/16
VNet-B 10.1.0.0/16
```

### Non-Transitive（経由接続できない）
Peering は経由接続できない。例えば A-B と B-C があっても、A-C は別途 Peering を設定する必要がある。

### 設計例
Production と SharedServices を接続し、Development と SharedServices を接続するが、Production と Development は接続しない、といった構成がよく使われる。

## まとめ
- VNet は独立したネットワーク
- VNet 間通信には VNet Peering を使う
- 通信は Azure バックボーンを通る
- アドレス空間の重複は不可
- Peering は経由接続できない

## 次に学ぶこと
次は Service Endpoint / Private Endpoint を整理する。
