---
title: "AZ-104 学習ログ Day11：Application Gateway / Traffic Manager / Front Door"
tags: [Azure, AZ104, 学習ログ, ApplicationGateway, FrontDoor]
private: false
updated_at: '2026-03-11T21:32:18+09:00'
id: 8750add42450db207602
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day11：Application Gateway / Traffic Manager / Front Door

## はじめに
トラフィック制御の上位レイヤーとして、Application Gateway / Traffic Manager / Front Door を整理する。あわせて Azure DNS の役割も簡潔に確認する。

### これまでに学習した内容
- Azure VM と Load Balancer
- VNet / NSG などのネットワーク基礎

## 本文
### Application Gateway
Application Gateway は L7（HTTP/HTTPS）のロードバランサー。L4 の Load Balancer と違い、HTTP レベルの情報でルーティングできる。

できることの例：

- URL ベースルーティング
- Web Application Firewall（WAF）

主な構成要素：

| 要素 | 役割 |
|---|---|
| Frontend | 入口 IP |
| Listener | HTTP/HTTPS の受付 |
| Rule | ルーティングルール |
| Backend Pool | 振り分け先 |

### Azure DNS
DNS はドメイン名を IP アドレスに変換する仕組み。Azure DNS は DNS ゾーンと DNS レコードを Azure で管理するサービス。

### Traffic Manager
Traffic Manager は DNS ベースのトラフィック分散サービス。どのリージョンへ接続するかを DNS 応答で決定する。

代表的なルーティング方式：

| 方式 | 内容 |
|---|---|
| Priority | 優先リージョンを使用 |
| Performance | ユーザーに近いリージョン |
| Weighted | 重み付き分散 |

### Front Door
Front Door はグローバルな L7 ロードバランサー。HTTP/HTTPS トラフィックを Azure のエッジで受け取り、最適なバックエンドへルーティングする。

特徴：

- グローバル負荷分散
- URL ルーティング
- WAF
- CDN 機能

### Traffic Manager と Front Door の違い
| サービス | 仕組み |
|---|---|
| Traffic Manager | DNS 応答で接続先を決定 |
| Front Door | HTTP/HTTPS を受けてルーティング |

### トラフィック制御の全体像
Azure ではトラフィック制御を階層で整理できる。

```
DNS
↓
Traffic Manager / Front Door
↓
Application Gateway
↓
Load Balancer
↓
VM
```

## まとめ
- Application Gateway は L7 ロードバランサー
- Traffic Manager は DNS ベースの分散
- Front Door はグローバル L7 ルーティング
- レイヤーを意識すると役割が整理しやすい

## 次に学ぶこと
次は Azure Monitor を中心に監視の基礎を整理する。
