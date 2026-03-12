---
title: AZ-104 学習ログ Day5：Azure Storage の基本
tags:
  - Azure
  - Storage
  - AzureStorage
  - AZ104
  - 学習ログ
private: false
updated_at: '2026-03-12T22:05:23+09:00'
id: a794a8b477035dacd4b2
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day5：Azure Storage の基本

## はじめに
ストレージは AZ-104 で出題頻度が高く、Azure アーキテクチャの基礎となるサービス。今回は Azure Storage の種類と設計観点を整理する。

### これまでに学習した内容
- 管理境界と RBAC の基礎
- 可用性・観測性の考え方

## 本文
### Azure Storage の種類
Azure では主に次のストレージサービスがある。

| ストレージ | 用途 |
|---|---|
| Blob Storage | 非構造データ（画像・動画・ログなど） |
| File Storage | ファイル共有（SMB / NFS） |
| Disk Storage | 仮想マシンのディスク |
| Table Storage | NoSQL データ |
| Queue Storage | メッセージキュー |

AZ-104 では特に Blob / File / Disk の理解が重要。

### Storage Account
Azure Storage は Storage Account の中に作成される。

```
Storage Account
├ Blob
├ File
├ Queue
└ Table
```

Storage Account はリージョンやセキュリティ、冗長構成などの設定を管理する単位。

### Blob Storage
Blob Storage はオブジェクトストレージで、非構造データの保存に向く。

- 画像・動画・ログ・バックアップなど
- HTTP/HTTPS でアクセス可能

### File Storage
Azure File Storage はクラウド版のファイルサーバーとして使える。

- SMB / NFS に対応
- 既存ファイルサーバーの移行や VM 間共有で利用

### Disk Storage
Disk Storage は VM の OS ディスクやデータディスクとして使う。

```
VM
├ OS Disk
└ Data Disk
```

### 冗長構成（Redundancy）
Azure Storage には複数の冗長構成がある。災害対策を強化するほどコストは高くなる。

| 冗長構成 | 内容 |
|---|---|
| LRS | 同一データセンター内で3コピー |
| ZRS | 同一リージョンの複数ゾーンで冗長 |
| GRS | 別リージョンにもコピー |
| RA-GRS | セカンダリリージョンから読み取り可能 |

### アクセス層（Blob）
Blob Storage にはアクセス頻度に応じた層がある。

| 層 | 特徴 |
|---|---|
| Hot | 頻繁にアクセス |
| Cool | 低頻度アクセス |
| Archive | 長期保存（取り出しに時間） |

### 使い分けの目安
| 用途 | ストレージ |
|---|---|
| VM の OS / データ | Disk |
| VM 間ファイル共有 | File |
| 画像 / 動画 / ログ | Blob |
| NoSQL データ | Table |

## まとめ
- Azure Storage は Storage Account を単位に管理する
- Blob / File / Disk を用途に応じて使い分ける
- 冗長構成とアクセス層で可用性とコストを調整できる

## 次に学ぶこと
次は Azure Network の基礎である VNet / Subnet を整理する。
