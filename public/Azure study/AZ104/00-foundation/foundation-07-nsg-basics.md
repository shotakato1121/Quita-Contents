---
title: AZ-104 学習ログ Day7：Network Security Group（NSG）の基本
tags:
  - Network
  - Azure
  - NSG
  - AZ104
  - 学習ログ
private: false
updated_at: '2026-03-12T22:05:23+09:00'
id: dc2c95e8c431e8d8ed83
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day7：Network Security Group（NSG）の基本

## はじめに
Azure ネットワークの通信制御を行う NSG（Network Security Group）を整理する。

### これまでに学習した内容
- VNet / Subnet / NIC の基本
- 境界設計と可用性・観測性の考え方

## 本文
### NSG とは
NSG は Azure ネットワークの通信を制御する仕組み。通信の許可・拒否をルールとして定義する。

### ルールの構成要素
NSG のルールは次の要素で構成される。

| 要素 | 内容 |
|---|---|
| Source | 送信元 |
| Destination | 宛先 |
| Port | ポート番号 |
| Protocol | TCP / UDP など |
| Action | Allow / Deny |

「誰が・どこへ・どのポートで通信できるか」を明示する。

### 適用できる場所
NSG は次の場所に適用できる。

- Subnet
- NIC

一般的には Subnet 単位で制御することが多い。

### Inbound / Outbound
NSG は通信方向を指定できる。

| 方向 | 意味 |
|---|---|
| Inbound | 外部から内部への通信 |
| Outbound | 内部から外部への通信 |

### Priority（優先順位）
NSG ルールは Priority の小さい順に評価され、最初に一致したルールで判定が確定する。

### 既定ルール（代表例）
既定ルールの代表例は次のとおり。

- Inbound：VNet 内通信は許可、Azure Load Balancer からの受信は許可、その他は拒否
- Outbound：VNet 内通信は許可、Internet への送信は許可、その他は拒否

### Subnet と NIC の両方に NSG がある場合
Subnet と NIC の両方に NSG が設定されている場合は、両方のルールを通過する必要がある。どちらかが拒否すると通信はブロックされる。

## まとめ
- NSG は Azure ネットワークの通信制御の基本
- ルールは Priority 順で評価される
- 既定ルールを踏まえて必要通信だけを許可する
- Subnet と NIC の両方に NSG がある場合は両方が適用される

## 次に学ぶこと
次は VNet Peering を整理する。
