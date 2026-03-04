---
title: 基礎編1：Subscription / Resource Group / Region / Resource の使い分け
tags:
  - Azure
  - 初心者
  - インフラ
  - AZ104
  - クラウド設計
private: false
updated_at: '2026-03-04T22:28:43+09:00'
id: f071652bc660487aedec
organization_url_name: null
slide: false
ignorePublish: false
---

# はじめに

Azure学習の最初の論点は、サービス名より先に
「管理の境界をどう切るか」を理解することだった。

この記事では、次の4要素だけに絞って整理する。

- Subscription
- Resource Group
- Region
- Resource

---

# 1. Subscription

Subscriptionは、Azure運用における主要な管理境界。

主な役割は以下。

- 課金の集計単位
- 権限付与の大きなスコープ
- 運用責任の分離単位

実務では「部署単位」だけでなく、
「本番/開発」や「事業ドメイン」で分けることも多い。

---

# 2. Resource Group

Resource Groupは、リソースの運用単位。

基本は次のルールで切る。

- 同じライフサイクルで変更・削除するものをまとめる
- 同じ運用チームが扱うものをまとめる

よくある誤りは「サービス種別」で分けること。
運用でまとめて扱えない構成になりやすい。

---

# 3. Region

Regionは管理階層ではなく、配置場所の選択軸。

選定時に見るべき観点は次の4つ。

- レイテンシ
- 可用性/災害耐性
- 法規制・データ所在
- コスト

Regionは後で修正コストが大きいため、
最初に業務要件から逆算して決める。

---

# 4. Resource

ResourceはVM、Storage、DBなどの実体。

設計上は「個別サービス」ではなく、
「どの境界（Subscription/RG/Region）で管理するか」とセットで見る。

---

# 5. 4要素をまとめて決める順番

迷ったときは次の順で決めると崩れにくい。

1. 事業責任と予算責任から Subscription を切る
2. 運用単位とライフサイクルから Resource Group を切る
3. 可用性と規制要件から Region を選ぶ
4. 最後に Resource を配置する

---

# まとめ

4要素は用語暗記より「境界設計」として理解した方が使いやすい。

- Subscription：責任と課金の境界
- Resource Group：運用とライフサイクルの境界
- Region：地理・可用性・規制の境界
- Resource：実装の最小単位

次は、これらの境界を組織全体に広げる
Management Group / RBACスコープ設計を整理する。
