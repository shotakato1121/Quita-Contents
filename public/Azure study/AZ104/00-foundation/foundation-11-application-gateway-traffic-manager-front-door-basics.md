---
title: AZ-104 学習ログ Day10–11：Application Gateway / Traffic Manager / Front Door を理解する
tags:
  - Azure
  - ApplicationGateway
  - FrontDoor
  - LoadBalancing
private: false
updated_at: '2026-03-11T21:32:18+09:00'
id: 8750add42450db207602
organization_url_name: null
slide: false
ignorePublish: false
---

# はじめに

AZ-104取得に向けた学習ログ。

これまでに

- VNet
- Subnet
- NSG
- Peering
- Private Endpoint
- VM
- Load Balancer

などAzureの基礎構成を学習してきた。

今回は **トラフィック制御の上位レイヤー**として

- Application Gateway
- Azure DNS
- Traffic Manager
- Azure Front Door

を整理する。

---

# Application Gateway

Application Gatewayは

> L7（HTTP/HTTPS）のロードバランサー

Load Balancer（L4）とは違い、HTTPレベルの情報を使ってトラフィックを制御できる。

基本構成
Internet
↓
Application Gateway
↓
VM


---

## Application Gatewayでできること

### URLベースルーティング

URLによってバックエンドを振り分けられる。

例
example.com/images → VM1
example.com/api → VM2


これはLoad Balancerでは実現できない。

---

### Web Application Firewall（WAF）

Application GatewayにはWAF機能があり、Webアプリケーション攻撃を防御できる。

代表例

- SQL Injection
- Cross Site Scripting (XSS)

---

### Application Gatewayの構成要素

| 要素 | 役割 |
|---|---|
Frontend | 入口IP |
Listener | HTTP/HTTPSの受付 |
Rule | ルーティングルール |
Backend Pool | 振り分け先 |

---

# Azure DNS

DNSは

> ドメイン名をIPアドレスに変換する仕組み

例
example.com → 20.10.1.5


Azure DNSは

> DNSゾーンとDNSレコードをAzureで管理するサービス

---

# Traffic Manager

Traffic Managerは

> DNSベースのトラフィック分散サービス

複数リージョンにサービスを配置したときに、どのリージョンへ接続するかを決める。

例
Japan East
Japan West


Traffic ManagerはDNS応答で
どちらのIPを返すか
を決定する。

---

## Traffic Managerのルーティング方法

代表的なルーティング方式

| 方式 | 内容 |
|---|---|
Priority | 優先リージョンを使用 |
Performance | ユーザーに近いリージョン |
Weighted | 重み付き分散 |

---

# Azure Front Door

Front Doorは

> グローバルなL7ロードバランサー

HTTP/HTTPSトラフィックをAzureのエッジで受け取り、最適なバックエンドへルーティングする。

構成イメージ
User
↓
Front Door
↓
Backend


特徴

- グローバル負荷分散
- URLルーティング
- WAF
- CDN機能

---

# Traffic Manager と Front Door の違い

| サービス | 仕組み |
|---|---|
Traffic Manager | DNSで接続先を決定 |
Front Door | HTTP/HTTPSトラフィックを受けてルーティング |

---

# Azureトラフィック制御の全体像

Azureではトラフィック制御を階層で整理できる。
DNS
↓
Traffic Manager
↓
Front Door
↓
Application Gateway
↓
Load Balancer
↓
VM


それぞれの役割

| レイヤー | サービス |
|---|---|
DNS | Azure DNS |
Global routing | Traffic Manager / Front Door |
L7 routing | Application Gateway |
L4 load balancing | Load Balancer |

---

# まとめ

今回の学習で理解したポイント

- Application GatewayはL7ロードバランサー
- URLベースルーティングが可能
- Traffic ManagerはDNSベースの分散
- Front DoorはグローバルL7ルーティング

Azureのトラフィック制御は

DNS → Global routing → Regional routing → VM

という階層構造になっている。

---

# 次に学ぶこと

次は **Azure Monitor / Log Analytics** を学習予定。

クラウドでは
構築
↓
運用
↓
監視
が重要になるため、監視基盤の理解が必要になる。
