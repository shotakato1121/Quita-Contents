---
title: 基礎編2：Management Group と RBAC スコープ設計
tags:
  - Azure
  - 初心者
  - インフラ
  - AZ104
  - クラウド設計
private: false
updated_at: '2026-03-04T22:28:43+09:00'
id: 33a7ee9b2ecf5ecd0e9b
organization_url_name: null
slide: false
ignorePublish: false
---

# はじめに

基礎編1で整理した「管理境界」を、
今回は組織レベルの階層と権限スコープへ拡張する。

この記事の焦点は次の2つ。

- Management Groupを使うべき条件
- RBACスコープをどこに置くべきか

---

# 1. Azureの管理階層

管理階層は次の順で並ぶ。

- Management Group（任意）
- Subscription
- Resource Group
- Resource

Regionはこの階層に含まれず、各Resourceの属性。

---

# 2. Management Groupを使う条件

Management Groupは「常に必要」ではない。

有効なケースは以下。

- Subscriptionが複数あり、共通ポリシーを強制したい
- 組織横断で権限モデルを統一したい
- 監査対象を組織単位で束ねたい

小規模環境でSubscriptionが少ないなら、
先にSubscription直下で運用を固めた方が簡潔。

---

# 3. RBACスコープの選び方

原則は「最小権限 + 運用コスト最小化」。

- Resource単位：最小権限だが管理コストが高い
- Resource Group単位：最も実務で使いやすい
- Subscription単位：広すぎるため限定的に使う
- Management Group単位：組織統制向け

実務上の基本は `Resource Group`。

---

# 4. よくあるアンチパターン

- とりあえず Subscription に Contributor を付与する
- Resource単位で細かく付けすぎて運用不能になる
- 権限境界と運用責務が一致していない

これらは事故時の影響範囲拡大と、
権限棚卸し不能を招きやすい。

---

# 5. 判断テンプレート

スコープ判断で迷ったら、次の質問を使う。

1. 影響を許容できる最大範囲はどこか
2. 同じ権限を何個のリソースに適用する必要があるか
3. 3か月後に棚卸し可能な粒度か

3つとも満たす最小スコープを選ぶ。

---

# まとめ

- Management Groupは「複数Subscriptionの統制」が必要なときに使う
- RBACは最小権限だけでなく運用可能性で決める
- 標準解は Resource Group スコープ

次は、ネットワーク境界と可用性・観測性を含む
設計の実装寄り論点に進む。
