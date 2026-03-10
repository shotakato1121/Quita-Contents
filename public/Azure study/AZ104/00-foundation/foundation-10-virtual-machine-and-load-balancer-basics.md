---
title: AZ-104 学習ログ Day8–9：Azure Virtual Machine と Load Balancer を理解する
tags:
  - Azure
  - VM
  - loadbalancer
  - 学習記録
  - AZ104
private: false
updated_at: '2026-03-10T21:30:30+09:00'
id: 097aaffcac89306e619f
organization_url_name: null
slide: false
ignorePublish: false
---

# はじめに

AZ-104取得に向けた学習ログ。

これまでの学習：

- Day1：Azureの基本構造（Tenant / Subscription / Resource Group）
- Day2：RBAC
- Day3：Azure Storage
- Day4：Virtual Network
- Day5：Network Security Group
- Day6：VNet Peering
- Day7：Private Endpoint / Service Endpoint

今回は **Compute領域の基礎**として

- Azure Virtual Machine
- Load Balancer

を整理する。

---

# Azure Virtual Machine（VM）

Azure VMは

> クラウド上で動作する仮想サーバー（IaaS）

オンプレミスのサーバーと比較すると、次の部分がAzureによって提供される。

| 項目 | 管理主体 |
|---|---|
物理サーバー | Azure |
OS | ユーザー |
アプリケーション | ユーザー |

---

# VMの構成要素

VMは単体では存在せず、複数のリソースと連携して動作する。

主な構成要素
VM
├ Disk
├ NIC
├ VNet / Subnet
└ Public IP


| リソース | 役割 |
|---|---|
Disk | OSやデータを保存 |
NIC | ネットワーク接続 |
VNet / Subnet | 仮想ネットワーク |
Public IP | インターネットアクセス |

---

# VMサイズ

VMにはサイズ（SKU）があり、性能を決定する。

例
Standard_B2s
Standard_D4s_v5


VMサイズが決めるもの

- CPU
- メモリ
- ネットワーク性能

---

# 可用性の確保

VMが1台だけの場合
VM停止 → サービス停止
となる。

そのためAzureでは複数VMを使った可用性設計が重要になる。

---

# Availability Set

Availability Setは

> 同一データセンター内でVMを分散する仕組み

Azureは次の単位でVMを分散する。

| 概念 | 意味 |
|---|---|
Fault Domain | 物理ラック |
Update Domain | メンテナンス単位 |

イメージ
Availability Set
├ VM1
└ VM2

これによりラック障害やメンテナンスの影響を軽減できる。

---

# Availability Zone

Availability Zoneは

> 同一リージョン内の異なるデータセンターにVMを配置する仕組み

例
Japan East
├ Zone1
├ Zone2
└ Zone3


Availability Setよりも **障害耐性が高い構成**になる。

---

# Virtual Machine Scale Set

アクセス数が時間帯によって変化する場合、VMを固定台数にすると効率が悪い。

例
昼：アクセス100
夜：アクセス10


この問題を解決するのが

> Virtual Machine Scale Set

VMを

- 自動追加
- 自動削減

できる仕組み。

---

# Azure Load Balancer

複数VMにトラフィックを分散するために使用する。

基本構成
Internet
↓
Load Balancer
↓
VM1
VM2

---

# Load Balancerの主要要素

## Frontend IP

ロードバランサーの入口となるIP。

| 種類 | 用途 |
|---|---|
Public IP | インターネット公開 |
Private IP | 内部通信 |

---

## Backend Pool

トラフィックを振り分ける対象VM。

Backend Pool
├ VM1
└ VM2


---

## Health Probe

VMの状態を確認する仕組み。

- 正常なVM → トラフィック送信
- 異常なVM → トラフィック停止

---

## Load Balancing Rule

どのポートの通信をどのVMへ送るかを定義する。

例
Frontend Port 80
↓
Backend Port 80


---

# Public Load Balancer と Internal Load Balancer

Azure Load Balancerには2種類ある。

| 種類 | 用途 |
|---|---|
Public Load Balancer | インターネット公開 |
Internal Load Balancer | VNet内部通信 |

---

# 今日の学び

- Azure VMはクラウド上の仮想サーバー
- 可用性を高めるには複数VMが必要
- Availability Setはラック単位の分散
- Availability Zoneはデータセンター単位の分散
- Load Balancerはトラフィックを複数VMへ分散する

---

# 次に学ぶこと

次は **Application Gateway** を学習予定。

Application Gatewayは

> L7（HTTPレベル）のロードバランサー

であり、AzureのWebアーキテクチャで重要な役割を持つ。
