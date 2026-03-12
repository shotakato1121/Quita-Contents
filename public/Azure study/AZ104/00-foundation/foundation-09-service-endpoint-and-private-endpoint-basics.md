---
title: AZ-104 学習ログ Day9：Service Endpoint と Private Endpoint の基本
tags:
  - Network
  - Azure
  - PrivateEndpoint
  - AZ104
  - 学習ログ
private: false
updated_at: '2026-03-12T22:05:23+09:00'
id: 9fb1e8d81fad73e58c9d
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day9：Service Endpoint と Private Endpoint の基本

## はじめに
PaaS サービスへの安全な接続方法として、Service Endpoint と Private Endpoint を整理する。

### これまでに学習した内容
- VNet Peering の基本
- NSG による通信制御

## 本文
### PaaS への通常接続
VM から PaaS に接続する場合、通常は Public Endpoint を使う。

```
VM
↓
Public Endpoint
↓
Azure Storage / Azure SQL / Key Vault
```

DNS 名は Public IP に解決される。

### Service Endpoint
Service Endpoint は「VNet / Subnet からのアクセスだけを許可する」仕組み。

- Public Endpoint はそのまま利用
- 対象は Subnet 単位
- 通信は Azure バックボーンを経由

### Private Endpoint
Private Endpoint は PaaS を VNet 内の Private IP で利用できるようにする仕組み。Subnet 内に NIC として作成される。

```
VNet
├ VM
└ Private Endpoint (Private IP)
↓
PaaS
```

### DNS の役割
Private Endpoint では DNS が重要。通常は Public IP に解決される名前が、Private IP に解決されるように設定する。

### Service Endpoint と Private Endpoint の違い
| 観点 | Service Endpoint | Private Endpoint |
|---|---|---|
| 接続先 | Public IP | Private IP |
| DNS | 変更なし | Private IP に解決 |
| 通信経路 | Azure バックボーン | VNet 内部 |
| セキュリティ | 中 | 高 |

### どちらを使うべきか
より高いセキュリティが必要で Public Endpoint を使いたくない場合は Private Endpoint が選択されることが多い。

## まとめ
- Service Endpoint は Public Endpoint を使いながらアクセス制御する
- Private Endpoint は Private IP で PaaS に接続する
- Private Endpoint では DNS 設計が重要

## 次に学ぶこと
次は Compute 領域として Azure Virtual Machine と Load Balancer の基礎を整理する。
