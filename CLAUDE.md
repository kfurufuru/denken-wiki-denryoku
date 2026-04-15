# 電験3種 電力Wiki — 運用方針

> 個人学習用。正確性 > 網羅性 > 読みやすさ。

---

## Step 1: 業務の言語化（全工数の80%）

新しいテーマページを書くとき、自分が実際にやっていること：

1. `docs/kakomon/by-field.md` で対象テーマの出題数・難易度分布を確認する
2. 参考書（教科書）で設備の全体構成を確認する
3. 繰り返し出る「計算の型」を1〜3個に絞る
4. 「なぜその構造なのか」を1行で言語化する（🧠直感アナロジー）
5. 計算例を1問だけ解いてから公式を書く（先に公式を書かない）
6. 落とし穴（🕳️）は必ず自分が一度ミスした箇所から取る

---

## CLAUDE.md の役割（経営方針）

- **何を作るか**: 電力科目「設備×公式×過去問」クロスリファレンス。合格に必要な情報を最短ルートで引ける状態にする
- **何を作らない**: thumbnail / slide-builder / seminar / SNS投稿 — 個人学習Wikiには不要
- **品質基準**: 数値・単位・公式は必ず `fact-check` スキルを経由してから ✅ マークを付ける

---

## ページ構造の標準形（`docs/themes/*.md`）

`docs/themes/suiryoku.md` を黄金テンプレートとして使う。

```
---
tags: [分野, サブテーマ, 頻度]
difficulty: ★★☆
version: vX.X
related_themes: [関連テーマ名]
---

# ⚡ テーマ名

> 1行の本質説明

!!! info "バージョン情報"

---

## 🧠 直感的理解
  - アナロジー（他の概念との対比）
  - !!! tip "5秒で思い出す"

## 🏭 設備を歩く
  - Mermaid graph LR で設備フロー
  - 主要機器テーブル

## ⚖️ 類似設備・方式の比較表

## 🔍 主要公式
  - 公式 → 記号テーブル → 手順 → 注意点（!!! danger）→ 例題

## 🕳️ 落とし穴・頻出ミス

## 📊 過去問出題実績
  - by-field.md の該当テーマと内容を同期

## ⚡ 5秒で思い出す（速攻暗記）

---

*vX.X — 確認ステータス: ✅確認済 / ⚠️未確認*
```

---

## 絵文字マーカー（`docs/reference/emoji-legend.md` 準拠）

| 絵文字 | 意味 |
|--------|------|
| 🧠 | 直感的理解・記憶すべきアナロジー |
| 🏭 | 設備構成・現場の視点 |
| ⚖️ | 比較表 |
| 🔍 | 公式の意味マップ |
| 🛤️ | 解法パターン |
| 🕳️ | 落とし穴・頻出ミス |
| 📝 | 正誤判定の急所 |
| 🎯 | 重要ポイント |
| ⚡ | 5秒で思い出す |
| 📊 | 出題実績 |

**勝手に追加しない。** 新しい絵文字が必要な場合は `emoji-legend.md` を先に更新する。

---

## 参照データ（スキルが必ず読むファイル）

| ファイル | 役割 |
|----------|------|
| `docs/reference/numbers.md` | 頻出数値（落差・電圧区分・係数） |
| `docs/reference/glossary.md` | 用語定義（誤記防止の正解リスト） |
| `docs/reference/calc-patterns.md` | 計算パターン1〜5（公式の書き方の基準） |
| `docs/kakomon/by-field.md` | 分野別出題数・難易度（優先度の根拠） |
| `data/atoms.csv` | 公式・過去問・落とし穴の最小単位 |

---

## スキル一覧（`.claude/skills/` 配下、各100〜300行）

| スキル | 何をするか |
|--------|-----------|
| `theme-writer` | `docs/themes/` の新規ページ or 不足セクションを標準形で生成 |
| `fact-check` | .md の数値・単位・公式を `numbers.md`・`glossary.md` と照合し指摘リストを出す |
| `kakomon-ingest` | 過去問1問を `data/atoms.csv` に1行追加する |
| `calc-pattern-writer` | `calc-patterns.md` に新しい計算パターンを追記する |
| `formula-ingest` | 公式を `data/atoms.csv`（type=formula）に追加する |
| `gap-finder` | `data/atoms.csv` と `docs/themes/` を比較し、未カバーの頻出論点を列挙する |

---

## データフロー

```
[収集]                [制作]               [品質]       [分析]
kakomon-ingest   →   theme-writer    →   fact-check  →  gap-finder
formula-ingest   →   calc-pattern-writer              ↓
                              ↓                   atoms.csv に
data/atoms.csv  →  data/pipeline.csv  →  docs/themes/*.md   フィードバック
                                              (= outputs)
```

---

## 出力禁止事項

- 参考書未照合の数値を `✅` にする
- `docs/themes/` 以外への新規 .md 作成（`reference/` は既存ファイルの**編集**のみ）
- `mkdocs.yml` の変更（構造・テーマ設定は固定）
- 新しい絵文字マーカーの追加（`emoji-legend.md` を先に更新しない限り）

---

## 確認ステータスの運用

- `✅ 確認済み` — 参考書・教科書と照合済み
- `⚠️ 未確認` — 内容確認が必要。参考書を正として使用すること

新規生成したコンテンツは原則 `⚠️ 未確認` でコミットし、目視確認後に `✅` に変更する。

---

*管理者: Furutachi | 更新: 2026-04-15*
