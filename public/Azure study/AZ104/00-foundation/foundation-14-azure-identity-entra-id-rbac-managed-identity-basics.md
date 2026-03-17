---
title: AZ-104 学習ログ Day14：Azure Identity（Entra ID / RBAC / Managed Identity）
tags:
  - Azure
  - RBAC
  - AZ104
  - 学習ログ
  - EntraID
private: false
updated_at: '2026-03-17T21:25:32+09:00'
id: 9c03c191733e46baf558
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day14：Azure Identity（Entra ID / RBAC / Managed Identity）

## はじめに
Azure のアクセス制御の中核となる Identity 領域を整理する。

### これまでに学習した内容
- Network / Compute / Load Balancing
- Monitoring / Disaster Recovery

## 本文
### 認証と認可
| 概念 | 意味 |
|---|---|
| 認証（Authentication） | あなたは誰か |
| 認可（Authorization） | 何ができるか |

### Azure AD（Microsoft Entra ID）
Azure AD（現 Microsoft Entra ID）は Azure の ID 管理基盤。

- ユーザー / グループ / アプリの管理
- サインインと認証の提供

### セキュリティプリンシパル
Azure でアクセス主体として扱われる ID。

- ユーザー
- グループ
- サービスプリンシパル
- Managed Identity

### RBAC（Role Based Access Control）
「誰が」「何に」「何ができるか」を定義する仕組み。

- 構成要素：セキュリティプリンシパル + ロール + スコープ
- 代表ロール：Reader / Contributor / Owner

### Service Principal
アプリケーション用の ID。自動処理や CI/CD で利用する。

### Managed Identity
Azure リソース専用の ID。秘密情報を持たずに認証できる。

- 自動作成 / 削除
- シークレット管理不要
- Azure が管理

### Service Principal と Managed Identity の違い
| 項目 | Service Principal | Managed Identity |
|---|---|---|
| 作成 | 手動 | 自動 |
| 用途 | アプリ | Azure リソース |
| 管理 | 自分で管理 | Azure が管理 |

### 認証フローのイメージ
例：VM から Storage へアクセスする場合。

```
VM
↓
Managed Identity
↓
トークン取得
↓
Storage
```

### 使い分け
| 要件 | 使用する仕組み |
|---|---|
| ユーザー管理 | Entra ID |
| 権限管理 | RBAC |
| アプリ認証 | Service Principal |
| Azure リソース認証 | Managed Identity |

## まとめ
- Entra ID は Azure の ID 管理基盤
- RBAC で権限（ロール）とスコープを管理する
- Service Principal はアプリ用、Managed Identity は Azure リソース用

## 次に学ぶこと
基礎は一通り整理できたので、次は模擬問題で知識を定着させる。
