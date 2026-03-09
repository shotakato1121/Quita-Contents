---
title: AZ-104 学習ログ Day7：Service Endpoint と Private Endpoint を理解する
tags:
  - Network
  - Azure
  - ServiceEndpoint
  - PrivateEndpoint
  - AZ104
private: false
updated_at: '2026-03-09T22:01:44+09:00'
id: 9fb1e8d81fad73e58c9d
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
- Day6：VNet Peering

今回は **PaaSサービスへの安全な接続方法**である

- Service Endpoint
- Private Endpoint

を整理する。

---

# PaaSサービスへの通常接続

AzureのVMからPaaSサービスに接続する場合、通常は次のような通信になる。
VM
↓
Public Endpoint
↓
Azure Storage / Azure SQL / Key Vault


例えばAzure Storageに接続する場合、VMは次のようなDNS名を使用する。

mystorageaccount.blob.core.windows.net


DNSがこの名前を **Public IPアドレス**に解決し、通信が行われる。

---

# Service Endpoint

Service Endpointは

> VNetからPaaSのPublic Endpointへのアクセスを制限する仕組み

Subnetに対して有効化する。
VNet
└ Subnet
└ VM
↓
Public Endpoint
↓
PaaS


特徴

- Public Endpointはそのまま使用する
- VNet/Subnetからのアクセスのみ許可できる
- Azureバックボーンを経由して通信する

---

# Private Endpoint

Private Endpointは

> PaaSサービスをVNet内のPrivate IPで利用できるようにする仕組み

Subnet内に作成され、実体は **NIC**として作られる。
VNet
├ VM
└ Private Endpoint (Private IP)
↓
PaaS


特徴

- Private IPが割り当てられる
- VMはPaaSのDNS名で接続する
- DNSの名前解決がPrivate IPに変わる

---

# DNSの役割

Private EndpointではDNSの設定が重要になる。

通常
mystorageaccount.blob.core.windows.net
↓
Public IP


Private Endpointを作成すると
mystorageaccount.blob.core.windows.net
↓
Private IP

に名前解決される。

その結果
VM
↓
Private IP
↓
Private Endpoint
↓
Storage


という通信になる。

---

# Service Endpoint と Private Endpoint の違い

| 観点 | Service Endpoint | Private Endpoint |
|---|---|---|
接続先 | Public IP | Private IP |
DNS | 変更なし | Private IPに解決 |
通信経路 | Azureバックボーン | VNet内部 |
セキュリティ | 中 | 強い |

---

# どちらを使うべきか

一般的には

- **より高いセキュリティが必要**
- **Public Endpointを使用したくない**

場合は

> Private Endpoint

が選択される。

---

# 今日の学び

- Service EndpointはPublic Endpointを利用したままアクセス制御する仕組み
- Private EndpointはPrivate IPでPaaSに接続する仕組み
- Private EndpointではDNSの名前解決が重要
- Private Endpointの方がよりセキュアな接続方法

---

# 次に学ぶこと

Azureネットワークの基礎が一通り理解できたため、次は

- Virtual Machine
- Availability Set
- Scale Set

などの **Compute領域**を学習予定。
