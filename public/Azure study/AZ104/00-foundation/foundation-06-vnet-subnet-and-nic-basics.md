---
title: AZ-104 学習ログ Day4：Azure Virtual Network（VNet）と Subnet の基本
tags:
  - Azure
  - Cloud
  - 学習記録
  - vnet
  - AZ104
private: false
updated_at: '2026-03-06T22:17:58+09:00'
id: 93fd4e87beac3f0d6903
organization_url_name: null
slide: false
ignorePublish: false
---

# はじめに

AZ-104取得に向けた学習ログ。

Day1では Azure の基本構造（Tenant / Subscription / Resource Group）
Day2では RBAC（アクセス制御）
Day3では Azure Storage を整理した。

今回は **Azure Network の基礎である VNet と Subnet** を学ぶ。

Azureではほぼすべてのリソースがネットワーク上で通信するため、
VNetの理解は運用設計の前提になる。

---

# VNetとは

VNet（Virtual Network）は、

> Azure上に構成するプライベートネットワーク

オンプレミスでいう社内LANに近い役割を持つ。

VNet内には、VM・Database・App Service などを配置できる。
同じVNet内のリソースは、プライベートIPで相互通信できる。

---

# VNetで押さえる要素

| 要素 | 役割 |
|---|---|
| Address Space | VNet全体のIP範囲を定義する |
| Subnet | 役割ごとにネットワークを分割する |
| NIC | VMなどのリソースをVNetへ接続する |
| NSG | 通信を許可/拒否するルールを適用する |

AZ-104では、これらを個別に覚えるより
「どの単位で分離・制御するか」をセットで理解するのが重要。

---

# Subnetの役割

Subnetは、VNetを論理的に分割する単位。

主な目的は次の3つ。

- セキュリティ境界を分ける
- 通信制御（NSG）の適用単位を分ける
- 運用責務や変更頻度の異なる層を分ける

例：
VNet
├ Web Subnet
├ App Subnet
└ DB Subnet

Web/App/DBを分けることで、
許可する通信方向やポートを明確に管理しやすくなる。

---

# アドレス空間の考え方

VNet作成時はまず Address Space（CIDR）を定義する。

例：
10.0.0.0/16

この範囲から Subnet を切り出して使う。

例：
VNet 10.0.0.0/16
├ Subnet-Web 10.0.1.0/24
└ Subnet-App 10.0.2.0/24

設計時は、将来の拡張を見越して
最初に余裕を持ったアドレス設計にしておくのが基本。

---

# Subnet間通信

同一VNet内のSubnet間は、

> デフォルトで相互通信可能

ただし実運用では、必要通信だけを許可するように
NSGやルート設計で通信範囲を絞る。

「通信できる状態を前提に、どこまで制限するか」を
明示的に設計するのがポイント。

---

# NICとIPアドレス

Azure VMは NIC（Network Interface）を通じてVNetへ接続される。

NICで管理される代表的な項目は以下。

- プライベートIP（VNet内通信）
- パブリックIP（インターネット公開時のみ）
- NSG関連付け

VM単体ではなく、NICがネットワーク設定の実体になる点を押さえる。

---

# 設計でよくある注意点

- オンプレミス接続予定があるのに、重複したCIDRを使う
- Subnetを用途で分けず、後からNSG設計が複雑になる
- パブリックIPを安易に付与して公開面を広げる

VNet設計は後からの修正コストが高いため、
最初に「境界」「接続先」「将来拡張」をまとめて決める方が安全。

---

# 今日の学び

- VNetはAzure上のプライベートネットワーク基盤
- Subnetはセキュリティと運用責務を分離する単位
- Address Spaceは将来拡張を見越して設計する
- 同一VNet内はデフォルト通信可、運用では明示的に制限する
- VMのネットワーク設定はNICが中心

---

# 次に学ぶこと

次は **NSG（Network Security Group）** を学習予定。

NSGのルール評価順序とスコープを理解すると、
VNet設計を実運用レベルに落とし込みやすくなる。
