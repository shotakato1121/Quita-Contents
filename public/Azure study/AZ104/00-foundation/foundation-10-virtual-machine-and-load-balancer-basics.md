---
title: "AZ-104 学習ログ Day10：Azure Virtual Machine と Load Balancer の基本"
tags: [Azure, AZ104, 学習ログ, VM, LoadBalancer]
private: false
updated_at: '2026-03-10T21:30:30+09:00'
id: 097aaffcac89306e619f
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day10：Azure Virtual Machine と Load Balancer の基本

## はじめに
Compute 領域の基礎として、Azure Virtual Machine と Load Balancer をまとめる。

### これまでに学習した内容
- Azure ネットワーク（VNet / NSG / Private Endpoint など）
- 境界設計と可用性の考え方

## 本文
### Azure Virtual Machine（VM）とは
Azure VM はクラウド上で動作する仮想サーバー（IaaS）。

| 項目 | 管理主体 |
|---|---|
| 物理サーバー | Azure |
| OS | ユーザー |
| アプリケーション | ユーザー |

### VM の構成要素
VM は単体では存在せず、複数のリソースと連携して動作する。

```
VM
├ Disk
├ NIC
├ VNet / Subnet
└ Public IP（必要な場合）
```

### VM サイズ
VM にはサイズ（SKU）があり、CPU・メモリ・ネットワーク性能が決まる。

### 可用性の確保
VM が 1 台だけだと停止＝サービス停止になりやすい。そこで複数 VM で冗長化する。

#### Availability Set
同一データセンター内で VM を分散する仕組み。Fault Domain（物理ラック）と Update Domain（メンテナンス単位）に分散される。

#### Availability Zone
同一リージョン内の異なるデータセンターに VM を配置する仕組みで、Availability Set より高い障害耐性を持つ。

#### Virtual Machine Scale Set
アクセス数の変動に合わせて VM を自動的に増減できる仕組み。

### Azure Load Balancer
複数 VM にトラフィックを分散する L4 ロードバランサー。

```
Internet
↓
Load Balancer
↓
VM1 / VM2
```

### Load Balancer の主要要素
| 要素 | 役割 |
|---|---|
| Frontend IP | 入口 IP（Public / Private） |
| Backend Pool | 振り分け先の VM |
| Health Probe | VM の状態確認 |
| Load Balancing Rule | ポート振り分けルール |

### Public と Internal
| 種類 | 用途 |
|---|---|
| Public Load Balancer | インターネット公開 |
| Internal Load Balancer | VNet 内部通信 |

## まとめ
- Azure VM はクラウド上の仮想サーバー
- 可用性向上には Availability Set / Zone / Scale Set を使う
- Load Balancer は L4 でトラフィックを分散する

## 次に学ぶこと
次は Application Gateway / Traffic Manager / Front Door など、上位レイヤーのトラフィック制御を整理する。
