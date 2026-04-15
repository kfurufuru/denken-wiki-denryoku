# formula-ingest

公式1件を `data/atoms.csv` に `type=formula` の行として追加する。`kakomon-ingest` が過去問を扱うのに対し、こちらは**教科書由来の公式・定数・数値**を登録する。

---

## 使い方

```
/formula-ingest <公式名>
例: /formula-ingest 比速度の定義式
例: /formula-ingest 電力損失の計算式
例: /formula-ingest 送電効率
```

複数まとめて登録：
```
/formula-ingest --batch 比速度,充電電流,フェランチ効果の近似式
```

---

## 事前に必ず読むファイル

1. `data/atoms.csv` — 既存 formula 行を確認（重複チェック）
2. `docs/reference/calc-patterns.md` — 既存パターンと重複しないか確認
3. `docs/reference/numbers.md` — 係数・定数の値の正確さを確認
4. `docs/reference/glossary.md` — 記号・変数名の正確な表記を確認

---

## atoms.csv への登録仕様

```csv
id,type,field,subfield,title,formula,unit,source,year,q_no,difficulty,verified
```

formula 行の各列：

| 列 | 値 |
|----|---|
| `id` | 既存の最大値 + 1（A0001〜の連番） |
| `type` | `formula`（固定） |
| `field` | 大分野（発電 / 変電 / 送電 / 配電 / 電気材料） |
| `subfield` | 中分野（水力 / 火力 / 変圧器 / 架空線路 など） |
| `title` | 公式の日本語名（「○○の計算式」「○○の定義」形式） |
| `formula` | 数式（ASCII で記述。例: `P=9.8QHη`） |
| `unit` | 公式の主要出力量の単位（例: `kW`、`%`、`V`） |
| `source` | 参照元（`教科書`・`電技`・`JIS` など） |
| `year` | 空欄 |
| `q_no` | 空欄 |
| `difficulty` | 空欄 |
| `verified` | `⚠️`（登録時は原則未確認） |

---

## 処理手順

1. `data/atoms.csv` の末尾を読み、現在の最大 id を取得する
2. 同じ `title` または `formula` の行が既にあれば追加しない（ユーザーに通知）
3. `calc-patterns.md` に同じ公式が既にある場合は登録を促さず、「既に calc-patterns.md パターンX に記載あり」と通知する
4. 追加する行をユーザーに確認表示してから書き込む

確認表示例：
```
追加予定:
  id: A0031
  type: formula
  field: 発電
  subfield: 水力
  title: 比速度の定義式
  formula: ns=n×√P/H^(5/4)
  unit: —
  source: 教科書
  verified: ⚠️

data/atoms.csv に追記してよいですか？ [y/N]
```

---

## number タイプの登録

公式ではなく**暗記すべき定数・数値境界**の場合は `type=number` で登録する（同スキルで対応）：

```
/formula-ingest --type number 力率改善後の必要コンデンサ容量の係数
```

`number` 行の場合、`formula` 列に値（例: `9.8`）、`unit` 列に単位（例: `kN/m³`）を入れる。

---

## 登録後の手順

1. 登録した公式が `docs/themes/` のどのページで使われるか確認する
2. 該当ページの「🔍 主要公式」セクションに記載がなければ `theme-writer` で補完する
3. 計算パターンとして独立させるべき内容なら `calc-pattern-writer` も実行する
