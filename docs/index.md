# 電験3種 電力Wiki

> 電力科目 — 設備×公式×過去問クロスリファレンス

## このWikiの目的

設備の**動作原理を理解**し、計算と知識の両方を攻略する。

```
発電所 → 変電所 → 送電線路 → 配電線路 → 需要家
  ⚡          🔄          ⚡           🔌          🏭
```

電力科目は「設備がなぜその構造なのか」を理解すれば、計算も知識問題も解ける。

---

## 🔌 設備系統で探す

<div class="grid cards" markdown>

- ⚡ **[発電](themes/index.md#hatsuden)**

    ---

    水力・火力・原子力・新エネルギー。出力計算・熱効率が頻出。

    代表テーマ: [水力発電](themes/suiryoku.md) / [火力発電](themes/karyoku.md)

- 🔄 **[変電](themes/index.md#henden)**

    ---

    変圧器・調相設備・保護継電器。損失計算・効率が頻出。

    代表テーマ: [変圧器](themes/henatsuki.md) / [保護継電器](themes/hogo-keiden.md)

- 🗼 **[送電](themes/index.md#souden)**

    ---

    架空線・地中ケーブル・電圧降下。線路定数・安定度計算が頻出。

    代表テーマ: [架空送電線路](themes/kakuu-souden.md) / [地中電線路](themes/chichuu-souden.md)

- 🔌 **[配電](themes/index.md#haiden)**

    ---

    配電方式・電圧降下・力率改善。出題数 **No.1 85問**。最優先。

    代表テーマ: [配電線路](themes/haiden.md) / [頻出計算パターン集](reference/calc-patterns.md)

</div>

---

## 📊 出題頻度 TOP5 テーマ

| 順位 | テーマ | 出題数(22年分) | 優先度 |
|------|--------|--------------|--------|
| 1 | [配電線路](themes/haiden.md) | 85問 | 🔴 最優先 |
| 2 | 送電（[架空](themes/kakuu-souden.md)＋[地中](themes/chichuu-souden.md)） | 68問 | 🔴 最優先 |
| 3 | [火力発電](themes/karyoku.md) | 60問 | 🔴 最優先 |
| 4 | 変電（[変圧器](themes/henatsuki.md)・[開閉装置](themes/kaihei-hogo.md)） | 54問 | 🔴 最優先 |
| 5 | [水力発電](themes/suiryoku.md) | 37問 | 🔴 最優先 |

出題数はH18〜R7下期の22年分集計（出典: 電験王）。分野の内訳は[分野別一覧](kakomon/by-field.md)を参照。

---

## クイックアクセス

| カテゴリ | リンク |
|---------|-------|
| 🔍 テーマ別で探す | [テーマ一覧](themes/index.md) |
| 📝 過去問から探す | [過去問マッピング](kakomon/index.md) |
| 🔢 計算パターンを確認 | [頻出計算パターン集](reference/calc-patterns.md) |
| 📋 数値を暗記する | [頻出数値暗記シート](reference/numbers.md) |

---

## 🎯 ページの読み方

各テーマページは「直感的理解 → 設備を歩く → 比較表 → 公式マップ → 解法パターン → 引っかけ → 正誤判定 → 出題実績」の共通構成。詳細は[標準セクション構成ガイド](reference/emoji-legend.md)を参照。

---

## 関連システム

| システム | 役割 |
|---------|------|
| 📗 [法規Wiki](https://kfurufuru.github.io/denken-wiki/) | 条文×過去問 知識リファレンス |
| 📘 [理論Wiki](https://kfurufuru.github.io/denken-wiki-riron/) | 公式×直感×過去問 |
| 📊 [学習進捗](https://kfurufuru.github.io/denken3-study/) | 過去問の達成率・管理 |

---

## 🎯 学習ガイド

### 初学者（0からスタート）
1. **水力・火力発電**から始める — 出力・熱効率の計算公式を最初に固める
2. **変圧器**の損失・効率計算をマスターする
3. **送電・配電**の電圧降下・電力損失計算を仕上げる

### 直前期（試験3ヶ月前〜）
1. [頻出計算パターン集](reference/calc-patterns.md) を繰り返し読む
2. [頻出数値暗記シート](reference/numbers.md) で数値を固める
3. [過去問マッピング](kakomon/index.md) で苦手テーマの問題を集中演習

### 本番直前（1週間前〜）
- 絵文字マーカー **⚡ 5秒で思い出す** のセクションだけをスキャン
- 落とし穴（🕳️）を再確認

---

*管理者: Furutachi | 最終更新: 2026-04-03 | v0.7*
