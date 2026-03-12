---
title: "AZ-104 学習ログ Day6：VNet / Subnet / NIC の基本"
tags: [Azure, AZ104, 学習ログ, VNet, Network]
private: false
updated_at: '2026-03-06T22:17:58+09:00'
id: 93fd4e87beac3f0d6903
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day6：VNet / Subnet / NIC の基本

## はじめに
Azure ではほぼすべてのリソースがネットワーク上で通信する。今回は VNet / Subnet / NIC を中心に、ネットワークの基礎構成を整理する。

### これまでに学習した内容
- Azure の管理境界と RBAC
- Azure Storage の基本

## 本文
### VNet とは
VNet（Virtual Network）は Azure 上に構成するプライベートネットワーク。オンプレミスでいう社内 LAN に近い役割を持つ。

### VNet の要素
| 要素 | 役割 |
|---|---|
| Address Space | VNet 全体の IP 範囲を定義 |
| Subnet | 役割ごとにネットワークを分割 |
| NIC | VM などのリソースを VNet へ接続 |
| NSG | 通信を許可/拒否するルールを適用 |

### アドレス空間の考え方
VNet 作成時はまず CIDR を定義する。将来の拡張を見越して余裕を持つのが基本。

```
VNet 10.0.0.0/16
├ Subnet-Web 10.0.1.0/24
└ Subnet-App 10.0.2.0/24
```

### Subnet の役割
Subnet は VNet を論理的に分割する単位。

- セキュリティ境界を分ける
- NSG の適用単位を分ける
- 変更頻度や責務の異なる層を分離する

### Subnet 間通信
同一 VNet 内の Subnet 間はデフォルトで相互通信可能。実運用では NSG やルート設計で必要通信だけを許可する。

### NIC と IP アドレス
Azure VM は NIC（Network Interface）を通じて VNet に接続される。NIC がネットワーク設定の実体であり、主に次を管理する。

- プライベート IP
- パブリック IP（必要な場合のみ）
- NSG の関連付け

### 設計でよくある注意点
- オンプレミス接続予定があるのに CIDR が重複する
- Subnet を用途で分けず、後から NSG 設計が複雑になる
- パブリック IP を安易に付与して公開面が広がる

## まとめ
- VNet は Azure 上のプライベートネットワーク基盤
- Subnet はセキュリティと運用責務を分離する単位
- NIC が VM のネットワーク設定の中心になる
- アドレス設計は将来拡張を見越す

## 次に学ぶこと
次は NSG（Network Security Group）のルール設計を整理する。
