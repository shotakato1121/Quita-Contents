---
title: AZ-104 学習ログ Day4：RBAC（Role Based Access Control）の基本
tags:
  - Azure
  - RBAC
  - accesscontrol
  - AZ104
  - 学習ログ
private: false
updated_at: '2026-03-17T20:41:47+09:00'
id: 6b3042d39e289e0d024b
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day4：RBAC（Role Based Access Control）の基本

## はじめに
Day1〜Day3で Azure の境界設計を整理した。ここからは「誰が・どこに・何をできるか」を管理する RBAC を改めてまとめる。

### これまでに学習した内容
- 管理境界（Subscription / Resource Group / Region / Resource）
- Management Group と RBAC スコープ設計
- 可用性・観測性の考え方

## 本文
### RBAC とは
RBAC は Azure リソースへのアクセス権限を管理する仕組み。構成要素は次の3つ。

| 要素 | 内容 |
|---|---|
| Security Principal | ユーザー / グループ / アプリケーション |
| Role | どの操作が可能か |
| Scope | どこに対して操作できるか |

この3つの組み合わせを Role Assignment と呼ぶ。

### RBAC のスコープ
RBAC は Azure の階層構造の中で設定できる。

- Management Group
- Subscription
- Resource Group
- Resource

上位スコープで付与した権限は下位に継承されるため、必要最小限の範囲で設定するのが原則。

### 代表的な Built-in Role
よく使うロールの特徴を整理する。

- Owner：すべての操作 + 権限付与が可能
- Contributor：リソース操作は可能だが権限付与は不可
- Reader：閲覧のみ

### カスタムロール
Built-in Role で要件を満たせない場合は Custom Role を作成する。例えば「VM の起動・停止は可能だが削除は不可」といった細かい制御に使う。

### RBAC 設計の原則
- 最小権限：必要な範囲に最も近いスコープを選ぶ
- 管理効率：同じ権限を複数リソースに付与するなら Resource Group 単位が扱いやすい

## まとめ
- RBAC は「Security Principal + Role + Scope」で構成される
- 権限はスコープで継承されるため、最小範囲で付与する
- 実務では Resource Group スコープがバランスが良い

## 次に学ぶこと
次は Azure Storage の基本を整理する。
