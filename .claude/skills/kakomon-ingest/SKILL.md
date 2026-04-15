# kakomon-ingest

電験3種 電力科目の過去問1問を `data/atoms.csv` に1行追加する。出典: 電験王（denken-ou.com）。

---

## 使い方

```
/kakomon-ingest <年度> <問番号>
例: /kakomon-ingest R07下 問1
例: /kakomon-ingest R06上 問15
```

複数問をまとめて追加する場合：
```
/kakomon-ingest --batch R07下 問1,問2,問3,問15
```

---

## 事前に必ず読むファイル

1. `data/atoms.csv` — 既存データを確認（重複チェック用）
2. `docs/kakomon/by-field.md` — タイトル・問題タイプ・難易度の正確な値を取得
3. `docs/kakomon/by-year.md` — 年度・問番号の対応確認

---

## atoms.csv のスキーマ

```csv
id,type,field,subfield,title,formula,unit,source,year,q_no,difficulty,verified
```

| 列 | 説明 | 例 |
|----|------|---|
| `id` | 連番（A0001〜、既存の最大値+1） | A0042 |
| `type` | `kakomon` / `formula` / `pitfall` / `number` / `diagram` | kakomon |
| `field` | 大分野（発電 / 変電 / 送電 / 配電 / 電気材料） | 発電 |
| `subfield` | 中分野（by-field.md のセクション名） | 水力 |
| `title` | by-field.md のタイトル列をそのまま転記 | 水力発電所の落差分類 |
| `formula` | 主要公式（計算問題のみ、空欄可） | P=9.8QHη |
| `unit` | 公式の出力単位（計算問題のみ、空欄可） | kW |
| `source` | 出典（固定: `電験王`） | 電験王 |
| `year` | 試験年度（by-field.md 表記に合わせる） | R07下 |
| `q_no` | 問番号（`問1`〜`問18` など） | 問1 |
| `difficulty` | 難易度（by-field.md の ★表記をそのまま） | ★★☆☆☆ |
| `verified` | 確認ステータス（原則 `⚠️`） | ⚠️ |

---

## 処理手順

1. `data/atoms.csv` の末尾行を読み、現在の最大 id（`A????`）を確認する
2. `docs/kakomon/by-field.md` から対象の行（年度×問番号）を検索する
3. 行が存在しない場合: `by-year.md` を確認し、それでも見当たらない場合はユーザーに通知して終了
4. field と subfield を決定する（by-field.md のセクション見出しから取る）
5. 計算問題（問題タイプが「計算」）の場合: `calc-patterns.md` と照合し、主要公式を `formula` 列に入れる
6. 重複チェック: 同じ `year × q_no` の行が既にあれば追加しない（ユーザーに通知）
7. 1行を CSV 形式で `data/atoms.csv` の末尾に追加する

---

## 出力例

追加する行をユーザーに確認表示してから書き込む：

```
追加予定:
  id: A0043
  type: kakomon
  field: 発電
  subfield: 水力
  title: 水力発電所の落差分類
  formula: （穴埋め問題のため空欄）
  source: 電験王
  year: R07下
  q_no: 問1
  difficulty: ★★☆☆☆
  verified: ⚠️

data/atoms.csv に追記してよいですか？ [y/N]
```

ユーザーが `y` を返したら追記する。

---

## pitfall / formula を同時に登録する場合

問題を読んで「この問題は典型的な落とし穴を含む」と判断した場合、atoms に2行追加する：

```csv
A0043,kakomon,発電,水力,水力発電所の落差分類,,, 電験王,R07下,問1,★★☆☆☆,⚠️
A0044,pitfall,発電,水力,有効落差（H）と総落差を混同しない,,, —,,,, ⚠️
```

---

## バッチ処理の注意

`--batch` の場合も1行ずつ確認表示してから追記する（まとめて確認 → まとめて書き込み も可）。

---

## 連携

- 追記後、`data/pipeline.csv` の関連 draft の `atoms_used` 列を更新する
- `gap-finder` スキルは `data/atoms.csv` の蓄積をもとにカバレッジを分析する
