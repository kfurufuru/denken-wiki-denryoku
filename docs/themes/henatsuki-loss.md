---
tags: [変圧器, 全日効率, 鉄損, 銅損, 年間損失電力量, 更新経済性, アモルファス, トップランナー, B問題対策, 高頻度]
difficulty: ★★★
version: v1.0
related_themes: [変圧器（基礎ハブ）, 配電線路, 電力系統・需給運用]
---

# 変圧器損失・効率（深掘り）— 全日効率・年間損失・更新経済性

!!! success "🎯 このページの 3 大公式"
    本ページで身に付ける核は次の 3 つ：

    1. **銅損の負荷率二乗則**：$P_c(\alpha) = \alpha^2 \, P_{c,full}$ — 負荷率 0.5 で銅損は **1/4 倍**、定格 1.0 で $P_{c,full}$
    2. **全日効率**：$\eta_{day} = \dfrac{\text{出力電力量}}{\text{出力電力量} + \text{鉄損電力量} + \text{銅損電力量}}$ — 24h 積分で評価（鉄損 24h 一定／銅損は時間帯別 $\alpha^2$）
    3. **年間損失電力量**：$W_{loss,\,year} = (\text{1 日損失}) \times 365$ — 単価を掛けて年間コスト換算 → 更新経済性

    この 3 つで R04下問12 を含む施設管理 B 問題の損失計算がほぼ網羅できる。

!!! warning "📖 読む前に：本ページは深掘りページです"
    本ページは **[変圧器（基礎ハブ）](henatsuki.md)** の §4 損失・効率セクション（鉄損・銅損の分類／瞬時効率／最大効率条件）を読んだ前提で書かれています。

    記号体系（$S_n, P_i, P_{c,full}, \alpha, \cos\theta$）も基礎ハブと共通。基礎が曖昧な方はまず基礎ハブを通読してから本ページに戻ってください。

!!! note "🗺️ 棲み分けマップ"
    **[変圧器（基礎ハブ）](henatsuki.md)**：巻数比・等価回路・損失分類・効率の基本・最大効率条件・並行運転・電圧変動率の **全体俯瞰と代表解法**。

    **本ページ＝変圧器損失・効率（深掘り）**：全日効率の本格計算・年間損失電力量・更新経済性評価（法規 R04下問12 など B 問題対策）の **深掘り**。

    **使い分け**：基礎ハブ＝瞬時値・基本暗記／本ページ＝時間積分・更新判断・施設管理 B 問題。

!!! note "📊 試験対策メタ"
    **頻出度**: 🔥🔥（電力＋法規 B 問題で年1回前後）／**重要度**: A（計算問題で安定得点源）／**直近出題**: R04下 問12（法規 施設管理・更新による損失差）

    **本ページが扱う論点**：全日効率／年間損失電力量／更新経済性評価／アモルファス変圧器・トップランナー規制／R04下問12 個別解説。**扱わない論点**（基礎ハブ参照）：巻数比・等価回路換算・瞬時効率・最大効率条件・並行運転・電圧変動率。

> 鉄損は **電圧があれば 24h 流れ続ける**、銅損は **負荷率の二乗で振れる**。この 2 つの性質を時間積分すると「年間損失電力量」が出る。更新で鉄損を半減できれば、稼働率の低い変圧器ほど年間効果が大きい。これが本ページの一行要約。

| 項目 | 内容 |
|------|------|
| 主題 | 変圧器の全日効率・年間損失電力量・更新経済性評価 |
| 前提知識 | [変圧器（基礎ハブ）](henatsuki.md) の §4 損失・効率／§5 解法パターン①② |
| 関連科目 | **電力**（変電・効率計算）・**法規**（施設管理 B 問題）・**機械**（変圧器章の基礎物理） |
| 制度背景 | **省エネ法（エネルギーの使用の合理化等に関する法律）**・**トップランナー制度**・**経済産業省告示**（電験 3 種の条文暗記としては直接問われないが、R04下問12 の「省エネ基準達成率」「基準エネルギー消費効率」はこの制度から派生する数値） |

---

## 1. なぜ「全日効率」を別概念として扱うか

瞬時効率 $\eta = P_{out}/(P_{out}+P_i+P_c)$ は **負荷率 α が固定** の前提で、ある瞬間の効率を表す。実プラントの変圧器は 1 日のうち昼夜・休日・季節で負荷率が大きく変動するため、**24 時間ぶん積分した「全日効率」** で評価しないと、設備設計や更新判断を誤る。

**3 行で本質**：

- 鉄損 $P_i$ は **電圧があれば 24h ずっと一定**（無負荷損）→ 1 日で $24 P_i$ [Wh]
- 銅損 $P_c$ は **負荷率の二乗** に比例 → 時間別の負荷率パターンを掛けて積分
- 全日効率 = 1 日の出力電力量 ÷（1 日の出力電力量 ＋ 1 日の鉄損 ＋ 1 日の銅損）

!!! warning "瞬時効率最大の負荷率 ≠ 全日効率最大の負荷率"
    瞬時効率は $P_i=\alpha^2 P_c$ で最大化（[基礎ハブの解法パターン②](henatsuki.md) 参照）。全日効率は 24h の負荷パターンに依存するため、軽負荷時間が長い変圧器では **鉄損を小さくした機種**（アモルファスなど）が有利になる。この差異が出題の核心。

---

## 2. 全日効率の本格計算

### 2.1 定義式

$$\eta_{day} = \frac{\displaystyle \sum_k P_{out,k}\,t_k}{\displaystyle \sum_k P_{out,k}\,t_k \;+\; P_i \cdot 24 \;+\; \sum_k \alpha_k^2 P_{c,full}\,t_k} \times 100 \quad [\%]$$

- $P_{out,k} = S_n \times \alpha_k \times \cos\theta$：時間帯 $k$ の出力 [W]
- $S_n$：**定格容量 [V·A]**（皮相）— 例：500 kV·A、100 kV·A 等
- $\alpha_k$：時間帯 $k$ の負荷率（0〜1・**皮相基準** $\alpha = S/S_n$）
- $\cos\theta$：負荷力率
- $t_k$：時間帯 $k$ の時間 [h]、$\sum t_k = 24$ h
- $P_i$：鉄損 [W]（一定）
- $P_{c,full}$：定格時の銅損 [W]

!!! note "負荷率は皮相 [kV·A] 基準"
    変圧器の定格は皮相電力 $S_n$ [V·A] で与えられる。負荷率も皮相基準で、有効電力 $P_{out}$ [W] から負荷率を出すときは **力率で割って皮相に戻す**：$\alpha = P_{out}/(S_n \cos\theta)$。これを忘れて $P_{out}/S_n$ で計算すると力率分だけズレる（§7 R04下問12 (b) の罠①参照）。

### 2.2 解法フロー

1. **時間別の負荷率と時間** を表に整理
2. **出力電力量** $\sum P_{out,k} t_k$ を集計 [Wh]
3. **鉄損総量** $24 P_i$ [Wh]（負荷率に依らず一定）
4. **銅損総量** $\sum \alpha_k^2 P_{c,full} t_k$ [Wh]
5. 定義式に代入

### 2.3 計算例（時間別負荷パターン）

#### ビジュアル：1 日の損失構成

<div><svg viewBox="0 0 880 380" xmlns="http://www.w3.org/2000/svg" width="100%" preserveAspectRatio="xMidYMid meet" role="img" aria-label="1日の出力と損失の時間別階段グラフ">
<defs>
<filter id="shLoss" x="-20%" y="-20%" width="140%" height="140%"><feDropShadow dx="0" dy="2" stdDeviation="2" flood-opacity="0.15"/></filter>
<linearGradient id="gLoad" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="#bbdefb"/><stop offset="100%" stop-color="#64b5f6"/></linearGradient>
<linearGradient id="gCu" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="#a5d6a7"/><stop offset="100%" stop-color="#66bb6a"/></linearGradient>
</defs>
<text x="440" y="24" text-anchor="middle" font-size="15" font-weight="700" fill="#212121">1日の出力と損失（鉄損は24h一定・銅損は負荷率²で振れる）</text>
<text x="440" y="44" text-anchor="middle" font-size="11" fill="#666">定格容量 100 kV·A・力率 1.0・鉄損 Pᵢ=500 W・定格銅損 Pc,full=1500 W</text>
<line x1="100" y1="320" x2="800" y2="320" stroke="#424242" stroke-width="1.5"/>
<line x1="100" y1="80" x2="100" y2="320" stroke="#424242" stroke-width="1.5"/>
<text x="100" y="340" text-anchor="middle" font-size="11" fill="#424242">0h</text>
<text x="333" y="340" text-anchor="middle" font-size="11" fill="#424242">8h</text>
<text x="624" y="340" text-anchor="middle" font-size="11" fill="#424242">18h</text>
<text x="800" y="340" text-anchor="middle" font-size="11" fill="#424242">24h</text>
<text x="450" y="358" text-anchor="middle" font-size="12" font-weight="700" fill="#424242">時間 [h]</text>
<text x="62" y="103" text-anchor="end" font-size="11" fill="#1565c0">100</text>
<text x="62" y="199" text-anchor="end" font-size="11" fill="#1565c0">60</text>
<text x="62" y="276" text-anchor="end" font-size="11" fill="#1565c0">20</text>
<text x="62" y="320" text-anchor="end" font-size="11" fill="#1565c0">0</text>
<text x="36" y="200" text-anchor="middle" font-size="12" font-weight="700" fill="#1565c0" transform="rotate(-90 36 200)">出力 [kW]</text>
<rect x="100" y="280" width="233" height="40" fill="url(#gLoad)" stroke="#1976d2" stroke-width="1.5" filter="url(#shLoss)"/>
<text x="216" y="306" text-anchor="middle" font-size="12" font-weight="700" fill="#0d47a1">深夜 20 kW × 8h</text>
<rect x="333" y="200" width="291" height="120" fill="url(#gLoad)" stroke="#1976d2" stroke-width="1.5" filter="url(#shLoss)"/>
<text x="478" y="264" text-anchor="middle" font-size="12" font-weight="700" fill="#0d47a1">朝夕 60 kW × 10h</text>
<rect x="624" y="100" width="176" height="220" fill="url(#gLoad)" stroke="#1976d2" stroke-width="1.5" filter="url(#shLoss)"/>
<text x="712" y="210" text-anchor="middle" font-size="12" font-weight="700" fill="#0d47a1">昼間 100 kW × 6h</text>
<line x1="100" y1="316" x2="800" y2="316" stroke="#d32f2f" stroke-width="2.2" stroke-dasharray="6,3"/>
<text x="450" y="80" text-anchor="middle" font-size="11" font-weight="700" fill="#d32f2f">━━ 鉄損 Pᵢ=500W（負荷率に依らず 24h 一定）</text>
<text x="450" y="376" text-anchor="middle" font-size="10" fill="#666">青の階段＝出力 / 赤の点線＝鉄損 / 緑＝銅損（時間帯別 60→540→1500 W）</text>
<rect x="820" y="280" width="56" height="36" fill="url(#gCu)" stroke="#2e7d32" stroke-width="1"/>
<text x="848" y="298" text-anchor="middle" font-size="9" font-weight="700" fill="#1b5e20">銅損</text>
<text x="848" y="312" text-anchor="middle" font-size="9" font-weight="700" fill="#1b5e20">60W</text>
<rect x="820" y="240" width="56" height="36" fill="url(#gCu)" stroke="#2e7d32" stroke-width="1"/>
<text x="848" y="258" text-anchor="middle" font-size="9" font-weight="700" fill="#1b5e20">銅損</text>
<text x="848" y="272" text-anchor="middle" font-size="9" font-weight="700" fill="#1b5e20">540W</text>
<rect x="820" y="200" width="56" height="36" fill="url(#gCu)" stroke="#2e7d32" stroke-width="1"/>
<text x="848" y="218" text-anchor="middle" font-size="9" font-weight="700" fill="#1b5e20">銅損</text>
<text x="848" y="232" text-anchor="middle" font-size="9" font-weight="700" fill="#1b5e20">1500W</text>
<rect x="100" y="100" width="280" height="78" rx="6" fill="#fffde7" stroke="#f9a825" stroke-width="1.2"/>
<text x="240" y="120" text-anchor="middle" font-size="11" font-weight="700" fill="#e65100">▼ 1 日の損失総量（§2.3 計算例）</text>
<text x="240" y="138" text-anchor="middle" font-size="10" fill="#bf360c">鉄損 = 500 × 24 = 12 kWh（24h 一定）</text>
<text x="240" y="154" text-anchor="middle" font-size="10" fill="#1b5e20">銅損 = 60×8 + 540×10 + 1500×6 = 14.88 kWh</text>
<text x="240" y="170" text-anchor="middle" font-size="10" fill="#1565c0">出力電力量 = 1360 kWh → η_day ≈ 98.06 %</text>
</svg></div>

**読み解き**：青の階段が **出力**（深夜→朝夕→昼間で 20→60→100 kW）、赤の点線が **鉄損 500 W（24h 一定）**、緑の薄い帯が **銅損 60→540→1500 W（負荷率²で大きく振れる）**。鉄損は「面積 = 一定値 × 24h」、銅損は「時間帯ごとに高さが負荷率²で変わる」面積積分になる。右上の黄色ボックスが §2.3 計算例の最終値。

---

定格容量 $S_n = 100$ kV·A、力率 $\cos\theta = 1.0$、鉄損 $P_i = 500$ W、定格銅損 $P_{c,full} = 1500$ W の変圧器を、次の負荷パターンで運転する（力率 1.0 のため $P_{out} = S_n \alpha$ で W と V·A が偶然一致するケース）：

| 時間帯 | 時間 $t_k$ [h] | 負荷率 $\alpha_k$ | 出力 $P_{out,k}$ [kW] |
|---|---:|---:|---:|
| 深夜（軽負荷） | 8 | 0.2 | 20 |
| 朝夕（中負荷） | 10 | 0.6 | 60 |
| 昼間（重負荷） | 6 | 1.0 | 100 |

**ステップ 1：出力電力量**

$$\sum P_{out,k} t_k = 20 \times 8 + 60 \times 10 + 100 \times 6 = 160 + 600 + 600 = 1360 \text{ kWh}$$

**ステップ 2：鉄損総量**

$$24 P_i = 24 \times 500 = 12{,}000 \text{ Wh} = 12 \text{ kWh}$$

**ステップ 3：銅損総量**

$$\sum \alpha_k^2 P_{c,full} t_k = (0.2^2 \times 8 + 0.6^2 \times 10 + 1.0^2 \times 6) \times 1500$$

$$= (0.32 + 3.6 + 6.0) \times 1500 = 9.92 \times 1500 = 14{,}880 \text{ Wh} \approx 14.88 \text{ kWh}$$

**ステップ 4：全日効率**

$$\eta_{day} = \frac{1360}{1360 + 12 + 14.88} \times 100 = \frac{1360}{1386.88} \times 100 \approx 98.06 \%$$

!!! tip "計算チェック"
    - 鉄損 12 kWh は時間が長い深夜帯にも一定で支配的になりがち
    - 銅損 14.88 kWh は昼間 6h で 9 kWh を稼ぐ（負荷率 1.0 × 6h × 1.5 kW）
    - 軽負荷の深夜が長い設備では鉄損比率が上がる → アモルファス変圧器の利得が大きい

---

## 3. 年間損失電力量と電気代換算

### 3.1 年間損失電力量

1 日の損失を 365 日に拡張する。負荷パターンが季節で変わらないと仮定すると：

$$W_{loss,year} = (24 P_i + \sum \alpha_k^2 P_{c,full} t_k) \times 365 \quad [\text{Wh/年}]$$

上記計算例なら $W_{loss,year} = (12 + 14.88) \times 365 = 9{,}811$ kWh/年。

### 3.2 電気代換算

電力量単価 $C$ [円/kWh] を掛ければ年間電気代の損失額。

$$\text{年間損失額} = W_{loss,year} \times C \quad [\text{円/年}]$$

例：$C = 20$ 円/kWh なら $9{,}811 \times 20 \approx 196{,}000$ 円/年。

---

## 4. 更新経済性評価（旧機 → 新機）

### 4.1 損失差額の出し方

旧機（添字 old）から新機（添字 new）に更新した場合の年間損失削減：

$$\Delta W_{year} = \{(24 P_{i,old} + \sum \alpha_k^2 P_{c(full),old}\,t_k) - (24 P_{i,new} + \sum \alpha_k^2 P_{c(full),new}\,t_k)\} \times 365$$

### 4.2 単純回収年（ペイバック）

更新投資額 $I$ [円]、年間損失削減額 $\Delta W_{year} \times C$ [円/年] のとき：

$$\text{単純回収年} = \frac{I}{\Delta W_{year} \times C} \quad [\text{年}]$$

!!! warning "鉄損改善は「24h × 365日」で効く"
    新機で鉄損が半分になれば、その効果は $\Delta P_i \times 8760$ h で年間に効く（負荷率に無関係）。軽負荷時間が長い変圧器ほど鉄損改善のインパクトが大きい。

### 4.3 アモルファス変圧器とトップランナー規制

#### 鉄心材料の比較

| 項目 | 珪素鋼板（従来） | アモルファス | 備考 |
|---|---|---|---|
| 結晶構造 | 結晶質（規則的に配列） | 非晶質（ランダム配列） | アモルファスは磁区の向き転換が容易 |
| ヒステリシス損 | 基準（1.0） | **約 1/3** | 軽負荷時間が長いほど効果絶大 |
| 渦電流損 | 板厚 0.35 mm 級で抑制 | 板厚 25 μm 級でさらに抑制 | アモルファスは薄帯製造（10 倍以上薄い） |
| 占積率 | 高い（製造容易） | やや低い（薄帯巻きが必要） | サイズはやや大型化する傾向 |
| 製造コスト | 標準 | 1.3〜1.5 倍 | 高めだが鉄損削減で長期回収可 |
| 騒音 | 標準 | やや大きめ | 磁歪が大きい — 居住地近接は留意 |
| 主用途 | 産業用大型・特殊用途 | 配電用変圧器（柱上・地上） | 軽負荷率が長時間の用途で優位 |

!!! note "なぜアモルファスは軽負荷で有利か"
    軽負荷の長時間運転では銅損より鉄損が支配的になる（§2.3 計算例でも鉄損 12 kWh／銅損 14.88 kWh と拮抗）。鉄損を 1/3 にできれば全日損失で大きな差が出る。逆に高負荷で 24h 稼働する産業用大型変圧器では銅損が支配的で、アモルファスの優位性は相対的に小さくなる。

#### 図解：BH 曲線で見る鉄損の差（ヒステリシス損 = ループ面積）

<div><svg viewBox="0 0 760 360" xmlns="http://www.w3.org/2000/svg" width="100%" preserveAspectRatio="xMidYMid meet" role="img" aria-label="アモルファスと珪素鋼板のBH曲線比較">
<text x="380" y="24" text-anchor="middle" font-size="15" font-weight="700" fill="#212121">BH 曲線（ヒステリシスループ）で見る鉄損</text>
<text x="380" y="44" text-anchor="middle" font-size="11" fill="#666">ループ内側の面積 = 1 サイクルで失うエネルギー（ヒステリシス損）</text>
<text x="190" y="68" text-anchor="middle" font-size="13" font-weight="700" fill="#1565c0">珪素鋼板（従来）</text>
<line x1="60" y1="200" x2="320" y2="200" stroke="#424242" stroke-width="1"/>
<line x1="190" y1="80" x2="190" y2="320" stroke="#424242" stroke-width="1"/>
<text x="318" y="216" text-anchor="end" font-size="10" fill="#666">H</text>
<text x="200" y="92" text-anchor="start" font-size="10" fill="#666">B</text>
<path d="M 90 256 Q 100 200 130 160 Q 170 100 250 110 Q 280 130 290 144 Q 280 200 250 240 Q 210 300 130 290 Q 100 270 90 256 Z" fill="#bbdefb" fill-opacity="0.5" stroke="#1565c0" stroke-width="2"/>
<text x="190" y="338" text-anchor="middle" font-size="11" font-weight="700" fill="#0d47a1">面積大 → ヒステリシス損 大</text>
<text x="190" y="354" text-anchor="middle" font-size="10" fill="#0d47a1">（基準 1.0）</text>
<text x="570" y="68" text-anchor="middle" font-size="13" font-weight="700" fill="#2e7d32">アモルファス（非晶質）</text>
<line x1="440" y1="200" x2="700" y2="200" stroke="#424242" stroke-width="1"/>
<line x1="570" y1="80" x2="570" y2="320" stroke="#424242" stroke-width="1"/>
<text x="698" y="216" text-anchor="end" font-size="10" fill="#666">H</text>
<text x="580" y="92" text-anchor="start" font-size="10" fill="#666">B</text>
<path d="M 530 230 Q 540 200 555 175 Q 580 120 620 115 Q 635 135 640 156 Q 635 200 620 225 Q 595 280 555 285 Q 540 270 530 230 Z" fill="#c8e6c9" fill-opacity="0.5" stroke="#2e7d32" stroke-width="2"/>
<text x="570" y="338" text-anchor="middle" font-size="11" font-weight="700" fill="#1b5e20">面積小 → ヒステリシス損 約 1/3</text>
<text x="570" y="354" text-anchor="middle" font-size="10" fill="#1b5e20">（細長く狭いループ）</text>
<rect x="330" y="120" width="100" height="120" rx="8" fill="#fff8e1" stroke="#f57c00" stroke-width="1.5"/>
<text x="380" y="140" text-anchor="middle" font-size="11" font-weight="700" fill="#bf360c">なぜ違う？</text>
<text x="380" y="158" text-anchor="middle" font-size="9" fill="#bf360c">珪素鋼板：</text>
<text x="380" y="172" text-anchor="middle" font-size="9" fill="#bf360c">結晶質で磁区</text>
<text x="380" y="184" text-anchor="middle" font-size="9" fill="#bf360c">向き転換に</text>
<text x="380" y="196" text-anchor="middle" font-size="9" fill="#bf360c">大きなエネルギー</text>
<text x="380" y="216" text-anchor="middle" font-size="9" fill="#1b5e20">アモルファス：</text>
<text x="380" y="228" text-anchor="middle" font-size="9" fill="#1b5e20">非晶質で容易</text>
</svg></div>

**読み解き**：左の青いループ（珪素鋼板）と右の緑のループ（アモルファス）。**ループの内側の面積がヒステリシス損 1 サイクルぶんに相当**。アモルファスは磁区構造が非晶質のため磁化方向の転換に要するエネルギーが小さく、ループが細長く狭くなる。結果、ヒステリシス損が約 1/3（実機では 1/3〜1/4 程度）。これに渦電流損の差（薄帯化で抑制）も加わり、鉄損総量で大幅な差が出る。

#### トップランナー規制の経緯

- **2002 年**：省エネ法（エネルギーの使用の合理化等に関する法律）にトップランナー方式導入
- **2006 年**：**第 1 次判断基準**（500 kV·A 以下の配電用油入変圧器が中心）
- **2014 年**：**第 2 次判断基準**（モールド変圧器も対象に・効率基準を強化）
- **R04 下問12 出題当時（2022 年）**：第 2 次基準が適用中。「省エネ基準達成率 140 %」のような派生型出題が増加
- **2026 年度**：**第 3 次判断基準** の目標年度。**油入変圧器・モールド変圧器ともに第 3 次判断基準へ移行**。対象機種拡大・効率基準のさらなる強化

#### 基準負荷率（容量で分かれる）

トップランナー変圧器のエネルギー消費効率評価では、**容量により基準負荷率が異なる**：

| 定格容量 | 基準負荷率 | 評価式の銅損項 | 適用例 |
|---|---:|---|---|
| **500 kV·A 以下**（境界値の 500 を含む） | **40 %** | $W_{c40} = 0.4^2 \times W_{c,full} = 0.16\, W_{c,full}$ | 柱上変圧器・配電用変圧器の大半 |
| **500 kV·A 超**（500 を超える 501 kV·A 以上） | **50 %** | $W_{c50} = 0.5^2 \times W_{c,full} = 0.25\, W_{c,full}$ | 大容量配電用・産業用変圧器 |

**判定式**：$\text{省エネ基準達成率}[\%] = \dfrac{\text{基準エネルギー消費効率}}{W_i + W_{c,\text{基準負荷率}}} \times 100$

!!! warning "境界値「500 kV·A」は **以下** に含まれる"
    500 kV·A ちょうどの機器は **「以下」のグループ＝負荷率 40 % 評価**。これが「以下」と「超」の典型的な区別ポイント。R04 下問12 の対象機（500 kV·A）はちょうど境界値だが「以下」の枠に入るため 40 % 評価が適用される。問題文に「○○ kV·A 以下」「○○ kV·A 超」「○○ kV·A 以上」「○○ kV·A 未満」の表現があったら境界値を含むかどうか必ず判定する。

!!! tip "R04下 問12 の試験上の意味づけ"
    本問の変圧器は **500 kV·A**（境界値・**以下グループ**）。基準負荷率は **40 %**。設問 (a) で 1,250 W を $W_i + W_{c40}$ で割って 140 % を出すロジックは、まさに「500 kV·A 以下機の基準負荷率 40 %」というルールを暗黙の前提にしている。容量が 501 kV·A 以上だったら 50 % 評価になり、$W_{c50}$（0.25 倍）を使うため答えの数値が変わる。

!!! warning "規制値の改定タイミングに注意"
    トップランナー基準は **施行年で具体的数値が変わる**。本ページの整理は 2026 年時点の運用解釈。最新の基準値は経済産業省告示で確認すべき。試験問題は出題時点の規制値を前提とするので、問題文に明示された値（本問なら基準エネルギー消費効率 1,250 W・達成率 140 %）をそのまま使う。

!!! note "なぜアモルファスが軽負荷で有利か"
    軽負荷の長時間運転では銅損より鉄損が支配的になる。鉄損を大幅に下げるアモルファスは、配電用変圧器（負荷率 0.2〜0.4 が長時間）で効果絶大。逆に高負荷で 24h 稼働する産業用大型変圧器では銅損が支配的で、アモルファスの優位性は相対的に小さくなる。

---

## 5. 公式マップ（追加分）

| 公式 | 式 | 単位 | 使う場面 |
|---|---|---|---|
| 全日効率 | $\eta_{day} = \dfrac{\sum P_{out,k} t_k}{\sum P_{out,k} t_k + 24 P_i + \sum \alpha_k^2 P_{c,full} t_k}$ | [%] | 時間帯別負荷率が与えられた効率評価 |
| 1 日鉄損総量 | $24 P_i$ | [Wh] | 鉄損は時間に対し一定 |
| 1 日銅損総量 | $\sum \alpha_k^2 P_{c,full} t_k$ | [Wh] | 時間帯別の負荷率二乗を積分 |
| 年間損失電力量 | $(24 P_i + \sum \alpha_k^2 P_{c,full} t_k) \times 365$ | [Wh/年] | 季節変動なしの仮定 |
| 年間損失額 | $W_{loss,year} \times C$ | [円/年] | $C$ は電力量単価 [円/kWh] |
| 更新による削減 | $\Delta W_{year} = W_{loss,old} - W_{loss,new}$ | [Wh/年] | 旧機・新機の損失差 |
| 単純回収年 | $I / (\Delta W_{year} \times C)$ | [年] | $I$ は投資額 [円] |

---

## 6. 解法パターン

### パターン①：時間別負荷率から全日効率を求める

**問題のキーワード**：「1 日の負荷曲線」「全日効率」「軽負荷○h、重負荷○h」

→ 詳細手順は [セクション 2.2 解法フロー](#22) の 5 ステップを参照。計算例は [セクション 2.3](#23) 参照（最終値 η_day ≈ 98.06 %）。

### パターン②：年間損失電力量と年間電気代

**問題のキーワード**：「年間損失」「年間電力料金」「○円/kWh」

**手順**：
1. 1 日の総損失を §2 の手順で求める
2. 365 倍して年間値（季節変動なしの仮定）
3. 電力量単価 $C$ を掛けて円換算

### パターン③：更新による損失差額・回収年

**問題のキーワード**：「旧変圧器を新変圧器に更新」「鉄損 ○ W → ○ W」「投資額○円」「何年で回収」

**手順**：
1. 旧機・新機それぞれの年間損失電力量を §3.1 で計算
2. 差額 $\Delta W_{year}$ を求める
3. 単価を掛けて年間削減額
4. 投資額 ÷ 年間削減額 = 単純回収年

---

## 7. R04下 問12 個別解説

!!! success "🎯 結論カード（先に答えだけ覚える）"
    **正答**：
    - 設問 (a) 更新後の負荷損 → **(5) 4,640 W**
    - 設問 (b) 損失比率 $W_2/W_1$ → **(3) 65 %**

    **最大の罠**：本機は 500 kV·A → **「以下」グループなので基準負荷率 40 % 評価**（$\times 0.16$ を掛ける／割る）

    **二番目の罠**：300 kW は **有効電力** なので、力率 0.8 で割って **皮相 375 kV·A** に直してから $\alpha = 375/500 = 0.75$ を出す。kW のまま 300/500 = 0.6 とすると間違い。

    詳細解法・選択肢ごとの誤答理由は以下のステップを参照。

!!! note "出典区分"
    **一次ソース（公式）**：[一般財団法人 電気技術者試験センター](https://www.shiken.or.jp/)公表の R04 年度下期 第三種電気主任技術者試験 法規科目 問12（出題：2022 年 9 月／配点：B 問題）。

    **参考解説サイト（解説照合用）**：[電験王（denken-ou.com）](https://denken-ou.com/houkir4-2-12/)・[やくとく（yaku-tik.com）](https://yaku-tik.com/denken/r4s-h12/) — 正答 (a)(5)・(b)(3) を 2 サイトで一致確認（2026-05-16）。問題文・選択肢は試験センター公表問題を正本とする。

### 共通条件

| 項目 | 旧変圧器 | 新変圧器 |
|---|---:|---:|
| 定格容量 | 500 kV·A | 500 kV·A |
| 無負荷損 $W_i$ | 500 W | 150 W |
| 負荷損（定格通電時）$W_c$ | 6,700 W | **(a) で求める** |
| 省エネ基準達成率 | — | **140 %** |
| 基準エネルギー消費効率 | — | 1,250 W |

電圧・周波数は更新前後で同じ。電圧変動による無負荷損への影響は無視。

#### 図解：R04下問12 解法フロー

<div><svg viewBox="0 0 800 420" xmlns="http://www.w3.org/2000/svg" width="100%" preserveAspectRatio="xMidYMid meet" role="img" aria-label="R04下問12の解法フローチャート">
<defs>
<filter id="shE" x="-20%" y="-20%" width="140%" height="140%"><feDropShadow dx="0" dy="2" stdDeviation="2" flood-opacity="0.15"/></filter>
<linearGradient id="gCond" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="#fff9c4"/><stop offset="100%" stop-color="#fff176"/></linearGradient>
<linearGradient id="gStepA" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="#bbdefb"/><stop offset="100%" stop-color="#90caf9"/></linearGradient>
<linearGradient id="gStepB" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="#c8e6c9"/><stop offset="100%" stop-color="#a5d6a7"/></linearGradient>
<linearGradient id="gAns" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stop-color="#ffe0b2"/><stop offset="100%" stop-color="#ffcc80"/></linearGradient>
</defs>
<text x="400" y="24" text-anchor="middle" font-size="15" font-weight="700" fill="#212121">R04下 問12 解法フロー（左：設問(a) ／ 右：設問(b)）</text>
<rect x="60" y="48" width="680" height="56" rx="8" fill="url(#gCond)" stroke="#f9a825" stroke-width="1.5" filter="url(#shE)"/>
<text x="400" y="68" text-anchor="middle" font-size="12" font-weight="700" fill="#bf8e00">▼ 共通条件</text>
<text x="400" y="86" text-anchor="middle" font-size="11" fill="#5d4037">500 kV·A・旧 Wᵢ=500W／Wc=6700W・新 Wᵢ=150W／達成率140%・基準効率 1250W</text>
<rect x="60" y="128" width="340" height="50" rx="8" fill="url(#gStepA)" stroke="#1565c0" stroke-width="1.5" filter="url(#shE)"/>
<text x="230" y="148" text-anchor="middle" font-size="12" font-weight="700" fill="#0d47a1">設問 (a) — 更新後の負荷損 Wc'</text>
<text x="230" y="166" text-anchor="middle" font-size="10" fill="#0d47a1">ステップ 1：達成率の定義式で逆算</text>
<rect x="60" y="190" width="340" height="50" rx="6" fill="#e3f2fd" stroke="#1976d2" stroke-width="1"/>
<text x="230" y="210" text-anchor="middle" font-size="10" font-weight="700" fill="#0d47a1">1250 / 1.40 = 892.86 W = Wᵢ + Wc40</text>
<text x="230" y="226" text-anchor="middle" font-size="10" fill="#0d47a1">→ Wc40 = 892.86 − 150 = 742.86 W</text>
<line x1="230" y1="240" x2="230" y2="260" stroke="#1565c0" stroke-width="2"/>
<polygon points="225,258 235,258 230,268" fill="#1565c0"/>
<rect x="60" y="270" width="340" height="50" rx="6" fill="#e3f2fd" stroke="#1976d2" stroke-width="1"/>
<text x="230" y="290" text-anchor="middle" font-size="10" font-weight="700" fill="#0d47a1">ステップ 2：負荷率 40% の二乗で定格戻し</text>
<text x="230" y="306" text-anchor="middle" font-size="10" fill="#0d47a1">Wc,full' = 742.86 / 0.16 ≈ 4,643 W</text>
<rect x="60" y="332" width="340" height="60" rx="8" fill="url(#gAns)" stroke="#e65100" stroke-width="2" filter="url(#shE)"/>
<text x="230" y="356" text-anchor="middle" font-size="13" font-weight="700" fill="#bf360c">▶ 正答 (a)：(5) 4,640 W</text>
<text x="230" y="376" text-anchor="middle" font-size="10" fill="#bf360c">罠：負荷率 40% 評価を忘れない（×0.16）</text>
<rect x="420" y="128" width="320" height="50" rx="8" fill="url(#gStepB)" stroke="#2e7d32" stroke-width="1.5" filter="url(#shE)"/>
<text x="580" y="148" text-anchor="middle" font-size="12" font-weight="700" fill="#1b5e20">設問 (b) — 損失比率 W₂/W₁</text>
<text x="580" y="166" text-anchor="middle" font-size="10" fill="#1b5e20">ステップ 1：300 kW を皮相に変換</text>
<rect x="420" y="190" width="320" height="50" rx="6" fill="#e8f5e9" stroke="#388e3c" stroke-width="1"/>
<text x="580" y="210" text-anchor="middle" font-size="10" font-weight="700" fill="#1b5e20">S = 300 / 0.8 = 375 kV·A</text>
<text x="580" y="226" text-anchor="middle" font-size="10" fill="#1b5e20">→ α = 375 / 500 = 0.75（罠①：kW で割らない）</text>
<line x1="580" y1="240" x2="580" y2="260" stroke="#2e7d32" stroke-width="2"/>
<polygon points="575,258 585,258 580,268" fill="#2e7d32"/>
<rect x="420" y="270" width="320" height="50" rx="6" fill="#e8f5e9" stroke="#388e3c" stroke-width="1"/>
<text x="580" y="290" text-anchor="middle" font-size="10" font-weight="700" fill="#1b5e20">ステップ 2：W = Wᵢ + α²·Wc,full</text>
<text x="580" y="306" text-anchor="middle" font-size="10" fill="#1b5e20">W₁ = 500 + 0.5625×6700 = 4,269 W</text>
<rect x="420" y="332" width="320" height="60" rx="8" fill="url(#gAns)" stroke="#e65100" stroke-width="2" filter="url(#shE)"/>
<text x="580" y="350" text-anchor="middle" font-size="11" font-weight="700" fill="#bf360c">W₂ = 150 + 0.5625×4640 = 2,760 W</text>
<text x="580" y="368" text-anchor="middle" font-size="13" font-weight="700" fill="#bf360c">▶ 正答 (b)：W₂/W₁ ≈ 64.7% → (3) 65%</text>
<text x="580" y="384" text-anchor="middle" font-size="9" fill="#bf360c">罠②：銅損は α² 比例（×0.5625）</text>
<line x1="230" y1="104" x2="230" y2="128" stroke="#f9a825" stroke-width="2"/>
<polygon points="225,126 235,126 230,134" fill="#f9a825"/>
<line x1="580" y1="104" x2="580" y2="128" stroke="#f9a825" stroke-width="2"/>
<polygon points="575,126 585,126 580,134" fill="#f9a825"/>
</svg></div>

**読み解き**：左ルートが (a) の解法、右ルートが (b) の解法。共通条件（黄色）からそれぞれ 2 ステップで橙色の正答ボックスに到達する。**両ルートの罠**：(a) は「負荷率 40 % 評価」を忘れない（×0.16）、(b) は「皮相基準で負荷率算定」して「銅損は $\alpha^2$ 比例」（×0.5625）。

### 設問 (a)：更新後の負荷損（定格通電時）

> 更新後の変圧器の負荷損（定格電流通電時）の値 [W] として、最も近いものを次の (1)〜(5) のうちから一つ選べ。
>
> (1) 1,860　(2) 2,450　(3) 3,080　(4) 3,820　(5) 4,640

**正答**：**(5) 4,640 W**

**解法ステップ**：

1. 省エネ基準達成率の定義式（負荷率 40 % 時の損失で評価される規格）：

    $$\text{省エネ基準達成率} [\%] = \frac{\text{基準エネルギー消費効率}}{W_i + W_{c40}} \times 100$$

    ここで $W_{c40}$ は **負荷率 40 % 時の銅損** = $0.4^2 \times W_{c,full} = 0.16\, W_{c,full}$。

2. 140 % と 1,250 W を代入して、更新後の $W_i + W_{c40}$ を逆算：

    $$W_i + W_{c40} = \frac{1{,}250}{1.40} \approx 892.86 \text{ W}$$

3. 更新後の $W_i = 150$ W を引いて $W_{c40}$ を求める：

    $$W_{c40} = 892.86 - 150 = 742.86 \text{ W}$$

4. 負荷損は **負荷電流（負荷率）の二乗** に比例するため、定格通電時の負荷損は $W_{c40} / 0.16$：

    $$W_{c,full}' = \frac{742.86}{0.16} \approx 4{,}643 \text{ W} \;\to\; \text{選択肢 (5) 4,640 W}$$

### 設問 (b)：更新前後の損失比率 $W_2 / W_1$

> 出力電圧が定格状態で、300 kW・遅れ力率 0.8 の負荷が接続されたとき、更新前後の変圧器の損失について、$W_2$（更新後）の $W_1$（更新前）に対する比率 [%] として、最も近いものを次の (1)〜(5) のうちから一つ選べ。
>
> (1) 45　(2) 54　(3) 65　(4) 78　(5) 85

**正答**：**(3) 65 %**

**解法ステップ**：

1. 負荷の **皮相電力** を求める（変圧器の負荷率は皮相基準）：

    $$S = \frac{P_{out}}{\cos\theta} = \frac{300}{0.8} = 375 \text{ kV·A}$$

2. 負荷率 $\alpha$：

    $$\alpha = \frac{S}{S_{rated}} = \frac{375}{500} = 0.75$$

3. 旧変圧器の損失 $W_1 = W_i + \alpha^2 W_{c,full}$：

    $$W_1 = 500 + 0.75^2 \times 6{,}700 = 500 + 0.5625 \times 6{,}700 = 500 + 3{,}768.75 = 4{,}268.75 \text{ W}$$

4. 新変圧器の損失 $W_2 = W_i' + \alpha^2 W_{c,full}'$（(a) で求めた 4,640 W を使用）：

    $$W_2 = 150 + 0.75^2 \times 4{,}640 = 150 + 0.5625 \times 4{,}640 = 150 + 2{,}610 = 2{,}760 \text{ W}$$

5. 比率：

    $$\frac{W_2}{W_1} = \frac{2{,}760}{4{,}268.75} \approx 0.6466 \to \text{選択肢 (3) 65 \%}$$

### ひっかけポイント

!!! warning "罠①：負荷率を「kW / 定格 kV·A」で計算する"
    変圧器の負荷率は **皮相 [kV·A] ベース**。問題文の 300 kW は有効電力なので、まず力率で割って皮相 375 kV·A に直してから 500 で割る。kW のまま 300/500 = 0.6 とすると間違い。

!!! warning "罠②：省エネ基準は「40 % 負荷時」評価を忘れる"
    トップランナー規制は **負荷率 40 %** での損失で評価する。設問 (a) では達成率の分母 $W_i + W_{c40}$ の $W_{c40}$ が 40 % 負荷時の銅損であり、定格通電時の銅損とは違う。$0.16$ を掛け忘れる／割り忘れると桁が違う答えになる。

!!! warning "罠③：銅損を負荷率の一次で計算する"
    銅損は $\alpha^2 W_{c,full}$。負荷率 0.75 のとき銅損は **0.5625 倍** であり 0.75 倍ではない。

!!! warning "罠④：無負荷損が更新で大きく減ったことを軽視する"
    本問では $W_i$ が 500 W → 150 W（70 % 減）。負荷率 0.75 と高めでも、新機の損失合計に占める無負荷損の比率は小さいため銅損改善の効果が支配的だが、軽負荷時はこの無負荷損減が効く。「鉄損改善は時間で効く」ことを忘れない。

### 選択肢ごとの誤答理由（設問 (b)）

| 選択肢 | 値 | 想定される誤計算 |
|---|---:|---|
| (1) 45 % | 0.45 | $\alpha$ を 0.6（kW 割り）で計算した／無負荷損を 0 とした |
| (2) 54 % | 0.54 | $\alpha$ を 0.6 で計算しつつ無負荷損も加えた |
| **(3) 65 %** | 0.65 | **正答**：$\alpha = 0.75$（皮相換算）＋ $\alpha^2$ ＋無負荷損も加算 |
| (4) 78 % | 0.78 | 銅損を $\alpha$ の一次で計算 |
| (5) 85 % | 0.85 | 無負荷損の改善（500→150）を考慮し忘れ |

### 学習要点

- **施設管理 B 問題のド定番計算**：「定格・損失データ＋負荷条件 → 負荷率算定 → $W = W_i + \alpha^2 W_{c,full}$ で集計 → 比率／差額／回収年」のパターン
- **省エネ基準達成率の式**は本問のような派生型で問われやすい。負荷率 40 % 評価という前提が問題文に書かれず暗黙化されている派生型に注意
- 本問は損失の **比率** を問うており、年間損失電力量・電気代換算までは要求されていない。回収年計算まで問う派生型が出ても上記 §3〜§4 の延長で対応可能

---

## 8. 引っかけパターン

!!! warning "引っかけ①：軽負荷時間が長いのに鉄損を軽視する"
    深夜・休日が長い設備で鉄損を見落とすと、年間損失の半分以上を取りこぼす。「鉄損は無負荷でもかかる損失」を忘れない。

!!! warning "引っかけ②：銅損を負荷率の一次（×α）で計算する"
    銅損は $\alpha^2 P_{c,full}$。負荷率 0.5 のとき銅損は **1/4**（半分ではない）。直感に反するため必ず二乗を意識する。

!!! warning "引っかけ③：「最大効率になる負荷率」と「全日効率最大になる負荷パターン」を混同"
    瞬時効率最大は $P_i = \alpha^2 P_c$（[基礎ハブの解法パターン②](henatsuki.md)）。全日効率最大は **24h の負荷パターン全体** で評価する別概念。軽負荷時間が長ければ鉄損の小さい機種が有利。

!!! warning "引っかけ④：年間値を 365 倍するのを忘れる"
    1 日の損失と年間損失で桁が 2 桁以上違う。「年間電気代」「年間損失」を求める問題で 365 倍を忘れると、選択肢の桁を取り違える。

---

## 9. 自問ブロック（Recall 想起練習）

理解度をセルフチェックする。各設問の答えを口頭で言ってから折りたたみを開く（[denken-wiki 学習UI規約](https://kfurufuru.github.io/denken-hoki-wiki/) の `denken_check` 連携キー：`denken_check::henatsuki-loss::q1` 〜 `q5`）。

??? question "Q1：なぜ鉄損は負荷率に依らないのか？"
    鉄損は印加電圧と周波数で決まる磁束密度の変化に起因する（ヒステリシス損＋渦電流損）。負荷電流が変わっても一次電圧が一定なら磁束密度も一定。よって鉄損は変わらない。これが「無負荷損」とも呼ばれる理由。

??? question "Q2：なぜ銅損は負荷率の二乗に比例するのか？"
    銅損は $I^2 R$。電流 $I$ が負荷率 $\alpha$ に比例（$I = \alpha I_{rated}$）するから、$P_c(\alpha) = (\alpha I_{rated})^2 R = \alpha^2 P_{c,full}$。二乗の根源は「電力 = 電流の二乗 × 抵抗」のジュール熱式。

??? question "Q3：瞬時効率最大の条件は何か？ なぜそれで最大になるか？"
    $P_i = \alpha^2 P_{c,full}$、すなわち鉄損 = 銅損 のとき効率最大。効率式 $\eta(\alpha)$ を $\alpha$ で微分して 0 を解くと得られる。直感的には固定損（鉄損）と変動損（銅損）が等しいとき全損失に対する出力割合が最大化される。

??? question "Q4：全日効率と瞬時効率の違いは？"
    瞬時効率は **特定の負荷率 1 点** での効率値。全日効率は **24h の負荷パターン全体** を積分した効率で、鉄損は時間ぶん常時かかり銅損は負荷率二乗で振れる。軽負荷時間が長い設備では鉄損の小さい機種（アモルファスなど）が有利。

??? question "Q5：更新で損失が減る効果はどう年額に換算するか？"
    旧機・新機それぞれの年間損失電力量 $W_{loss,year}$ を計算し、差額 $\Delta W_{year}$ を取る。電力量単価 $C$ [円/kWh] を掛けて年間削減額。投資額 ÷ 年間削減額 = 単純回収年。鉄損改善は 24h × 365日 = 8760h ぶん効く点が重要。

---

## 10. 出題実績（損失・効率・更新経済性 関連）

!!! note "論点別ソート（Interleaving 配慮）"
    変圧器の損失・効率を直接扱う出題を **鉄損／銅損／効率／全日効率／経済性** に分類して列挙。年度横断学習用。

| 論点 | 年度 | 問 | 科目 | 内容 | 難易度 |
|---|---|---|---|---|---|
| 鉄損材料 | R05上 | 14 | 電力 | アモルファス鉄心の特徴 | ★★☆ |
| 鉄損材料 | H30 | 14 | 電力 | 変圧器に使用される鉄心材料 | ★★☆ |
| 鉄損材料 | H27 | 14 | 電力 | 鉄心材料の特徴 | ★★☆ |
| 効率（瞬時）| H28 | 6 | 電力 | 変圧器の容量・効率 | ★★☆ |
| 経済性 | **R04下** | **12** | **法規** | **変圧器更新による損失の変化（本ページ §7）** | **★★☆** |
| 経済性 | R04上 | 12 | 法規 | 柱上変圧器・需要率と容量 | ★★☆ |
| 経済性 | H26 | 12 | 法規 | 変圧器容量算定 | ★★★ |
| 損失（線路）| R05下 | 13 | 電力 | 単相 2 線式・3 線式の電力損失 | ★★★ |

!!! tip "R08 出題予測"
    R03 以降「変圧器の効率・最大効率の単独計算」が少なく、関連計算は遮断器定格や並行運転に組み込まれる傾向（[基礎ハブの出題実績](henatsuki.md) 参照）。R08 では **全日効率／年間損失／更新経済性** の派生型が法規 B 問題で再出題される可能性が高い。

---

## 11. 関連ページ

- [変圧器（基礎ハブ）](henatsuki.md) — 巻数比・等価回路・損失分類・最大効率条件など基礎全般
- [配電線路](haiden.md) — 配電変圧器の運用環境
- [電力系統・需給運用](denryoku-keitou.md) — 系統内の変圧器運用と需要率
- [電気材料](denki-zairyou.md) — アモルファス・珪素鋼板・絶縁油

---

## 監修ログ

- **作成日**：2026-05-16
- **一次ソース**：[一般財団法人 電気技術者試験センター](https://www.shiken.or.jp/) 公表の第三種電気主任技術者試験過去問（R04 下期 法規 問12）・省エネ法（エネルギーの使用の合理化等に関する法律）トップランナー基準・経済産業省告示
- **隣接 wiki**：[変圧器（基礎ハブ）](henatsuki.md)（損失/効率セクションの記号体系 $P_i, P_{c,full}, S_n, \alpha, \eta_{day}$ と整合）
- **参考解説サイト（照合用）**：電験王 ([denken-ou.com](https://denken-ou.com/houkir4-2-12/))・やくとく ([yaku-tik.com](https://yaku-tik.com/denken/r4s-h12/)) — 正答 (a)(5)・(b)(3) 一致確認（2026-05-16）
- **検証手段**：全日効率・年間損失・R04下問12 (a)(b) の数値例を電卓再計算 → 隣接 henatsuki.md と記号体系整合確認

## 更新履歴

- **v1.3**（2026-05-16）：導線整理。ページ名を「変圧器損失・効率（深掘り）」に簡潔化・冒頭に「読む前に：基礎ハブ前提」warning 追加・棲み分けマップを「扱う／扱わない論点」明示型に強化・nav 表記を「変圧器（基礎ハブ）／変圧器損失・効率（深掘り）」に統一。
- **v1.2**（2026-05-16）：ChatGPT レビュー反映。$\varepsilon_r = P_c/S_n$ 表記修正・効率式を $S_n$ ベースに統一・出典表記を試験センター公式に修正・トップランナー第3次基準（2026年度）追記・並行運転条件を位相変位／結線方式／%R:%X比 まで補強・「不可能 → 実用的でない」表現調整。
- **v1.1**（2026-05-16）：階段グラフ SVG・棲み分けマップ・アモルファス比較表・トップランナー経緯・§6 重複削減を追加。
- **v1.0**（2026-05-16）：新規作成。henatsuki.md の損失・効率セクションの深掘り版として発足。法規 R04下 問12 対策の入口を兼ねる。
