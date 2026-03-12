---
title: AZ-104 学習ログ Day1：Subscription / Resource Group / Region / Resource の使い分け
tags:
  - Azure
  - Subscription
  - AZ104
  - 学習ログ
  - Azure基礎
private: false
updated_at: '2026-03-12T22:05:23+09:00'
id: f071652bc660487aedec
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day1：Subscription / Resource Group / Region / Resource の使い分け

## はじめに
Azureの学習を始めるとき、サービス名より先に「管理の境界をどう切るか」を整理しておくと迷いが減る。今回は Subscription / Resource Group / Region / Resource の4要素を、運用設計の視点でまとめる。

## 本文
### Subscription
Subscription は Azure 運用の大きな管理境界で、主に次の役割を持つ。

- 課金の集計単位
- 権限付与の大きなスコープ
- 運用責任の分離単位

実務では「部署単位」だけでなく、「本番/開発」「事業ドメイン」で分けることも多い。

### Resource Group
Resource Group はリソースの運用単位。基本は次のルールで切る。

- 同じライフサイクルで変更・削除するものをまとめる
- 同じ運用チームが扱うものをまとめる

「サービス種別」で分けると、運用でまとめて扱えない構成になりやすいので注意する。

### Region
Region は管理階層ではなく、配置場所の選択軸。選定時に見るべき観点は次のとおり。

- レイテンシ
- 可用性/災害耐性
- 法規制・データ所在
- コスト

Region は後からの変更コストが大きいため、最初に要件から逆算して決める。

### Resource
Resource は VM や Storage などの実体。個別サービス名を覚えるだけでなく、「どの境界（Subscription / Resource Group / Region）で管理するか」とセットで考える。

### 4要素を決める順番
迷ったときは次の順で決めると崩れにくい。

1. 事業責任と予算責任から Subscription を切る
2. 運用単位とライフサイクルから Resource Group を切る
3. 可用性と規制要件から Region を選ぶ
4. 最後に Resource を配置する

## まとめ
- Subscription：責任と課金の境界
- Resource Group：運用とライフサイクルの境界
- Region：地理・可用性・規制の境界
- Resource：実装の最小単位

## 次に学ぶこと
次は、これらの境界を組織全体に広げるための Management Group と RBAC スコープ設計を整理する。
