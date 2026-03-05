---
title: AZ-104 学習ログ Day2：RBAC（Role Based Access Control）を理解する
tags:
  - Azure
  - Cloud
  - RBAC
  - 学習記録
  - AZ104
private: false
updated_at: '2026-03-05T21:26:17+09:00'
id: 6b3042d39e289e0d024b
organization_url_name: null
slide: false
ignorePublish: false
---

# はじめに

AZ-104取得に向けた学習ログ。

Day1では Azure の基本構造（Tenant / Subscription / Resource Group）を整理した。

Day2では **Azureのアクセス制御の仕組みである RBAC** を学ぶ。

クラウド環境では

> 誰が、どのリソースを、どこまで操作できるのか

を適切に管理することが重要になる。

Azureではこれを **RBAC（Role Based Access Control）** で管理する。

---

# RBACとは

RBACとは

> Azureリソースへのアクセス権限を管理する仕組み

RBACは次の3つの要素で構成される。
Security Principal
＋
Role
＋
Scope


| 要素 | 内容 |
|---|---|
| Security Principal | ユーザー / グループ / アプリケーション |
| Role | どの操作が可能か |
| Scope | どこに対して操作できるか |

この3つの組み合わせを **Role Assignment** と呼ぶ。

---

# RBACのスコープ

RBACは Azure の階層構造の中で設定できる。
Management Group
Subscription
Resource Group
Resource


特徴：

- 上位スコープに設定すると **下位に継承される**
- 必要最小限の範囲で設定するのが原則

例：
Subscription に権限付与
↓
Resource Group
↓
Resource


---

# 代表的な Built-in Role

Azureにはあらかじめ定義されたロールが存在する。

## Owner

特徴：

- すべてのリソース操作が可能
- RBACの権限付与も可能

主な用途：

- Azure環境の管理者

---

## Contributor

特徴：

- すべてのリソース操作が可能
- **RBAC権限付与はできない**

主な用途：

- 開発者
- インフラ担当者

---

## Reader

特徴：

- リソースの閲覧のみ可能
- 変更不可

主な用途：

- 監査
- 運用監視

---

# カスタムロール

Built-in Roleでは要件を満たせない場合は  
**Custom Role** を作成する。

例：
VMの起動・停止は可能
VMの削除は不可


このような細かい権限設定が必要な場合に利用する。

---

# RBAC設計の原則

Azureでは次の2つの原則で権限を設計する。

## 最小権限の原則

必要最小限の範囲で権限を付与する。

例：
Tenant
Management Group
Subscription
Resource Group


必要な範囲に最も近いスコープを選択する。

---

## 管理効率

同じ権限を複数リソースに付与する場合は  
**Resource Group単位で付与する**

---

# 設計問題（AZ-104でよく出るパターン）

構造：
Subscription
├ Resource Group A
└ Resource Group B


要件：

- 開発チームに **Aのリソースを操作させたい**
- **Bには触れさせたくない**

最適なRBACスコープ：

> Resource Group A

理由：

- Subscription → 他アプリに影響
- Resource → 設定数が多すぎる
- Resource Group → 最小範囲かつ管理効率が良い

---

# 今日の学び

- RBACは「誰が・どこに・何をできるか」を管理する仕組み
- RBACは **Security Principal + Role + Scope** で構成される
- 権限はスコープで継承される
- 権限設計は **最小権限 × 管理効率**

---

# 次に学ぶこと

次は **Azure Storage** を学ぶ予定。

AZ-104ではストレージ領域が特に出題される。

- Blob Storage
- File Storage
- Disk Storage
- 冗長構成（LRS / ZRS / GRS / RA-GRS）

