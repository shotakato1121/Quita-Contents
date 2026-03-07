---
title: AZ-104 学習ログ Day5：Network Security Group（NSG）を理解する
tags:
  - Network
  - Azure
  - 学習記録
  - NSG
  - AZ104
private: false
updated_at: '2026-03-07T10:41:07+09:00'
id: dc2c95e8c431e8d8ed83
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

今回は **Azureネットワークの通信制御を行う NSG（Network Security Group）** を整理する。

---

# NSGとは

NSG（Network Security Group）は

> Azureネットワークの通信を制御する仕組み

ファイアウォールに近い役割を持つ。

NSGでは

- 通信の許可
- 通信の拒否

をルールとして定義できる。

---

# NSGで定義できるルール

NSGのルールは次の要素で構成される。

| 要素 | 内容 |
|---|---|
| Source | 送信元 |
| Destination | 宛先 |
| Port | ポート番号 |
| Protocol | TCP / UDP など |
| Action | Allow / Deny |

つまり

誰が
どこへ
どのポートで
通信できるか

を制御する。

---

# NSGはどこに適用できるか

NSGは次の場所に適用できる。
Subnet
NIC

構造イメージ：
VNet
└ Subnet
└ VM
└ NIC


- Subnet：ネットワーク単位で通信制御
- NIC：特定VMのみ通信制御

一般的には

> Subnet単位で制御することが多い

---

# Inbound / Outbound

NSGでは通信方向を指定できる。

| 方向 | 意味 |
|---|---|
| Inbound | 外部から内部への通信 |
| Outbound | 内部から外部への通信 |

例：
Internet → Web
Inbound

Web → DB
Outbound

---

# Priority（優先順位）

NSGルールには **Priority** がある。

ルールは

> 数字が小さい順に評価される

例：
Priority 100 Allow HTTP
Priority 200 Deny All

この場合

> HTTP通信は許可される

---

# Defaultルール

NSGには最初からデフォルトルールが存在する。

代表的なもの：

| 通信 | デフォルト |
|---|---|
| VNet内通信 | Allow |
| Internet → VM | Deny |
| VM → Internet | Allow |

つまり

- 同じVNet内のVMは通信可能
- 外部からの通信は基本拒否

---

# SubnetとNIC両方にNSGがある場合

NSGが
Subnet
NIC

両方に設定されている場合、

> 両方のルールを通過する必要がある

例：

Subnet NSG
Allow HTTP

NIC NSG
Deny HTTP


この場合

> HTTP通信は拒否される

---

# 今日の学び

- NSGはAzureの通信制御（ファイアウォール）
- NSGはSubnetまたはNICに適用できる
- ルールはPriority順に評価される
- SubnetとNIC両方のNSGが適用される

---

# 次に学ぶこと

次は **VNet Peering** を学習予定。

VNet Peeringは

> 複数のVNetを接続する仕組み

Azureネットワークを理解する上で重要な概念。
