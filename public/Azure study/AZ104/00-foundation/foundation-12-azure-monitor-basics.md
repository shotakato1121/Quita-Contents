---
title: "AZ-104 学習ログ Day12：Azure Monitor の基本"
tags: [Azure, AZ104, 学習ログ, AzureMonitor, Monitoring]
private: false
updated_at: null
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day12：Azure Monitor の基本

## はじめに
Azure の運用・監視の中心となる Azure Monitor を整理する。

### これまでに学習した内容
- Compute とトラフィック制御（VM / Load Balancer / Application Gateway など）
- 境界設計と可用性の考え方

## 本文
### Azure Monitor とは
Azure リソースを監視するためのサービス。状態の可視化と異常検知に使う。

### 監視データの種類
Azure Monitor では主に 2 種類のデータを扱う。

| 種類 | 内容 |
|---|---|
| Metrics | CPU 使用率などの数値データ |
| Logs | イベントやエラーログ |

### Metrics
数値データの監視に向いており、リアルタイム性が高い。

- CPU 使用率
- メモリ使用率
- ディスク IO

### Logs
イベントデータの分析に向いている。

- VM 再起動
- エラーイベント
- セキュリティログ

### Log Analytics
ログの分析には Log Analytics Workspace を使う。

- ログ保存
- ログ検索
- ログ分析

ログ検索には KQL（Kusto Query Language）を使う。

### Alert
条件に基づいて通知する仕組み。例：CPU 使用率 > 90%。

## まとめ
- Azure Monitor は Azure の監視基盤
- Metrics と Logs を用途に応じて使い分ける
- Log Analytics と Alert で分析・通知を実現する

## 次に学ぶこと
次は Azure Backup と Site Recovery を整理し、障害対策の全体像をまとめる。
