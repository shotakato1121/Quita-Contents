---
title: AZ-104 学習ログ Day2：Management Group と RBAC スコープ設計
tags:
  - Azure
  - RBAC
  - AZ104
  - 学習ログ
  - Azure基礎
private: false
updated_at: '2026-03-12T22:05:23+09:00'
id: 33a7ee9b2ecf5ecd0e9b
organization_url_name: null
slide: false
ignorePublish: false
---

# AZ-104 学習ログ Day2：Management Group と RBAC スコープ設計

## はじめに
Day1で整理した「管理境界」を、今回は組織レベルの階層と権限スコープへ拡張する。

### これまでに学習した内容
- Subscription / Resource Group / Region / Resource の役割
- 境界は「運用と責任の切り分け」として決める

## 本文
### Azure の管理階層
管理階層は次の順で並ぶ。Region は階層ではなく、各 Resource の配置属性。

- Management Group（任意）
- Subscription
- Resource Group
- Resource

### Management Group を使う条件
Management Group は「常に必要」ではない。次のようなときに有効。

- Subscription が複数あり、共通ポリシーを強制したい
- 組織横断で権限モデルを統一したい
- 監査対象を組織単位で束ねたい

小規模で Subscription が少ない場合は、まず Subscription 直下で運用を固めた方が簡潔。

### RBAC スコープの選び方
原則は「最小権限 + 運用コスト最小化」。

- Resource 単位：最小権限だが管理コストが高い
- Resource Group 単位：実務で最も使いやすい
- Subscription 単位：広すぎるため限定的に使う
- Management Group 単位：組織統制向け

実務の標準は Resource Group スコープになりやすい。

### よくあるアンチパターン
- とりあえず Subscription に Contributor を付与する
- Resource 単位で細かく付けすぎて運用不能になる
- 権限境界と運用責務が一致していない

これらは事故時の影響範囲拡大や権限棚卸しの困難さにつながる。

### 判断テンプレート
スコープ判断で迷ったら、次の質問を使う。

1. 影響を許容できる最大範囲はどこか
2. 同じ権限を何個のリソースに適用する必要があるか
3. 3か月後に棚卸し可能な粒度か

3つとも満たす最小スコープを選ぶ。

## まとめ
- Management Group は「複数 Subscription の統制」が必要なときに使う
- RBAC は最小権限だけでなく運用可能性で決める
- 標準解は Resource Group スコープ

## 次に学ぶこと
次は、ネットワーク境界と可用性・観測性を含む設計の考え方を整理する。
