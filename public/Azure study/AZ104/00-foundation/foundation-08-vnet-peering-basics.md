---
title: AZ-104 学習ログ Day6：VNet Peering を理解する
tags:
  - Network
  - Azure
  - peering
  - 学習記録
  - vnet
private: false
updated_at: '2026-03-07T11:01:29+09:00'
id: c1cb65ff3e321f95c586
organization_url_name: null
slide: false
ignorePublish: false
---

# はじめに

AZ-104取得に向けた学習ログ。

これまでの学習内容：

- Day1：Azureの基本構造（Tenant / Subscription / Resource Group）
- Day2：RBAC（Role Based Access Control）
- Day3：Azure Storage
- Day4：Virtual Network（VNet）
- Day5：Network Security Group（NSG）

今回は **VNet Peering** を整理する。

VNet Peeringは

> 複数のVNetを接続する仕組み

Azureネットワーク設計では頻繁に使われる重要な機能。

---

# なぜVNet同士を接続するのか

VNetは

> 独立したネットワーク

として作成される。

例：
VNet-A
└ Web VM

VNet-B
└ DB VM

この場合
Web → DB
の通信はできない。

理由：

- VNetは独立したネットワーク
- ルーティングが存在しない

そのため **VNet同士を接続する仕組み**が必要になる。

---

# VNet Peeringとは

VNet Peeringは

> 2つのVNetを接続する仕組み

Peeringを設定すると

VNet-A
↕
VNet-B

の通信が可能になる。

---

# 通信経路

VNet Peeringの通信は

> Azureバックボーンネットワーク

を通る。

つまり

- インターネットは通らない
- Azure内部ネットワークで通信される

---

# アドレス空間の条件

Peeringを設定するには

> VNetのアドレス空間が重複していない必要がある

例：
VNet-A 10.0.0.0/16
VNet-B 10.1.0.0/16


この場合はPeering可能。

一方
VNet-A 10.0.0.0/16
VNet-B 10.0.1.0/24

のようにアドレスが重複する場合は設定できない。

---

# Peeringの制限

VNet Peeringには次の特徴がある。

### Non-Transitive（経由接続できない）

例：
VNet-A ↔ VNet-B
VNet-B ↔ VNet-C


この場合
VNet-A ↔ VNet-C
の通信はできない。

VNet-AとVNet-Cを通信させるには

> 新しくPeeringを設定する必要がある

---

# 設計例

次の構成を考える。

VNet-Production
VNet-Development
VNet-SharedServices

要件：

- Production → SharedServices 通信
- Development → SharedServices 通信
- Production ↔ Development 通信なし

この場合の接続は
Production ↔ SharedServices
Development ↔ SharedServices
の2つのPeeringを設定する。

---

# 今日の学び

- VNetは独立したネットワーク
- VNet同士の通信にはVNet Peeringを使う
- 通信はAzureバックボーンを通る
- アドレス空間が重複するとPeeringできない
- Peeringは経由接続できない

---

# 次に学ぶこと

次は **Private Endpoint / Service Endpoint** を学習予定。

これは

> AzureのPaaSサービスを安全に接続する仕組み

であり、Azureネットワーク設計の重要な要素になる。
