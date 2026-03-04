# AZ104 Notes Structure

## フォルダ構成

- `00-foundation/`
  - AZ104に入る前の基礎整理
  - 境界設計・スコープ設計・可用性/観測性
- `10-design/`
  - 設計テーマ別ノート
  - ガバナンス境界から締切保証設計まで

## 読み順

1. `00-foundation/foundation-01-subscription-rg-region-resource.md`
2. `00-foundation/foundation-02-management-hierarchy-and-rbac-scope.md`
3. `00-foundation/foundation-03-boundary-availability-observability.md`
4. `10-design/01-rbac-and-policy-control-boundary.md`
5. `10-design/02-control-plane-vs-data-plane-cost-risk.md`
6. `10-design/03-governance-limit-and-runtime-control-layers.md`
7. `10-design/04-static-vs-dynamic-control-3d-model.md`
8. `10-design/05-continuity-and-cost-guardrails.md`
9. `10-design/06-deadline-risk-redefinition.md`
10. `10-design/07-deadline-guarantee-line-implementation.md`

## 今回の見直し方針

- タイトル粒度を統一（基礎編N / 設計テーマ）
- 重複していた「基礎概念」「プレーン説明」を記事ごとに役割分担
- ルート直下のファイルを整理し、目的別フォルダへ分割
