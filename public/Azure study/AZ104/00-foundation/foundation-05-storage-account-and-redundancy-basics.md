---
title: AZ-104 学習ログ Day3：Azure Storage の基本を整理する
tags:
  - Azure
  - Cloud
  - Storage
  - 学習記録
  - AZ104
private: false
updated_at: '2026-03-05T21:52:29+09:00'
id: a794a8b477035dacd4b2
organization_url_name: null
slide: false
ignorePublish: false
---

# はじめに

AZ-104取得に向けた学習ログ。

Day1では Azure の基本構造（Tenant / Subscription / Resource Group）  
Day2では RBAC（アクセス制御）を整理した。

今回は **Azure Storage** を学習する。

ストレージはAZ-104で出題頻度が高く、  
Azureアーキテクチャの基礎となるサービス。

---

# Azure Storage の種類

Azureでは主に次のストレージサービスがある。

| ストレージ | 用途 |
|---|---|
| Blob Storage | 非構造データ |
| File Storage | ファイル共有 |
| Disk Storage | 仮想マシンのディスク |
| Table Storage | NoSQLデータ |
| Queue Storage | メッセージキュー |

AZ-104では特に以下の3つが重要。
Blob
File
Disk


---

# Blob Storage

Blob Storageは **オブジェクトストレージ**。

主に次のようなデータを保存する。

- 画像
- 動画
- ログ
- バックアップ
- JSONファイル

特徴：

- 非構造データ
- HTTP/HTTPSアクセス
- 大容量データ向け

---

# File Storage

Azure File Storageは

> クラウド版ファイルサーバー

として利用できる。

アクセスプロトコル：

- SMB
- NFS

用途：

- VM間でのファイル共有
- 既存ファイルサーバーの移行
- アプリの共有フォルダ

---

# Disk Storage

Disk Storageは

> 仮想マシンのディスク

VMの構造は以下。
VM
├ OS Disk
└ Data Disk


- OS Disk：OSがインストールされる
- Data Disk：アプリデータ保存

---

# Storage Account

Azure Storageは **Storage Account の中に作成される**。

構造：
Storage Account
├ Blob
├ File
├ Queue
└ Table


Storage Accountは

- リージョン
- セキュリティ
- 冗長構成

などの設定を管理する単位。

---

# 冗長構成（Redundancy）

Azure Storageには複数の冗長構成がある。

| 冗長構成 | 内容 |
|---|---|
| LRS | 同一データセンター内で3コピー |
| ZRS | 同一リージョンの複数ゾーンで冗長 |
| GRS | 別リージョンにもコピー |
| RA-GRS | セカンダリリージョンから読み取り可能 |

災害対策を強化するほど **コストは高くなる**。

---

# アクセス層（Blob）

Blob Storageにはアクセス頻度に応じた層がある。

| 層 | 特徴 |
|---|---|
| Hot | 頻繁にアクセス |
| Cool | 低頻度アクセス |
| Archive | 長期保存 |

特徴：

- Archiveはストレージコストが低い
- ただし取り出し時に時間がかかる

---

# ストレージの使い分け

用途に応じてストレージを選択する。

| 用途 | ストレージ |
|---|---|
VMのOS | Disk |
VM間ファイル共有 | File |
画像 / 動画 | Blob |
NoSQLデータ | Table |

---

# 今日の学び

- Azure Storageには複数の種類がある
- Storage Accountが管理単位
- 冗長構成で可用性が変わる
- Blobにはアクセス層がある

---

# 次に学ぶこと

次は **Azure Network（VNet）** を学習予定。

Azureではすべてのリソースがネットワーク上で通信するため、  
VNetの理解は非常に重要。
