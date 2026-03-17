---
title: AZ-104 学習ログ Day13：Azure Backup / Site Recovery の基本
tags:
  - Azure
  - backup
  - disasterRecovery
  - AZ104
  - 学習ログ
private: false
updated_at: '2026-03-17T20:41:58+09:00'
id: 6879899a6a64b3aa2570
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day13：Azure Backup / Site Recovery の基本

## はじめに
監視の次は、障害対策として Azure Backup と Azure Site Recovery を整理する。

### これまでに学習した内容
- Azure Monitor（Metrics / Logs / Alert）
- 可用性設計（RTO / RPO）

## 本文
### Azure Backup
Azure Backup は Azure リソースのバックアップを取得・保持するサービス。誤削除や論理障害への備えとして使う。

### Recovery Services Vault
バックアップやレプリケーションを管理するコンテナ。対象リソースの設定や保持期間などをここで管理する。

### バックアップの種類（代表例）
| 対象 | 例 |
|---|---|
| VM | 仮想マシンのバックアップ |
| ファイル | Azure File / 共有フォルダ |
| データベース | Azure SQL など |

### Azure Site Recovery（ASR）
Site Recovery は災害対策（DR）のためのサービス。リージョン障害などを想定して、別リージョンへレプリケーションし、フェイルオーバーを行う。

### Azure Backup と Site Recovery の違い
| 観点 | Azure Backup | Site Recovery |
|---|---|---|
| 目的 | データ保護 / 誤削除対策 | 災害対策 / 事業継続 |
| 方式 | バックアップ取得 | ほぼリアルタイム複製 |
| 主な対象 | データ / VM | VM / 重要システム |

### 使い分けのイメージ
- 誤削除・論理障害対策：Azure Backup
- リージョン障害対策：Site Recovery

## まとめ
- Azure Backup はバックアップ取得と復旧を担う
- Site Recovery は DR（災害対策）でフェイルオーバーを担う
- 目的に応じて使い分ける

## 次に学ぶこと
ひと通り基礎を整理できたので、次は模擬問題や実際の設計ケースで知識を定着させる。
