# CLAUDE.md — Blitzstein & Hwang 互動式自學專案

> 任何新開的 Claude Code session 進到這個資料夾,**第一件事讀完這份檔案**,再開始工作。

---

## 1. 專案目標(What we're doing)

把 **Blitzstein & Hwang《Introduction to Probability》**(PDF 在資料夾根目錄)
的每一個**小節**(例如 §2.1、§2.2…)做成一個**互動式 HTML 學習頁**。

**核心精神:** 讀完一個 HTML = 讀完原書那一節 + 多了引導問題與視覺直覺。
讀完 HTML 再翻原書,應該能立刻認出「對,就是這節」,而非「這是另一個版本」。

**章末的 `Exercises` 與 `R` 兩節不做。**

---

## 2. 使用者(jimmylion)的學習狀況與偏好

- **背景:** 已自學完第一章 + 寫完約 80% 章末練習題,從 §2.1 開始做互動頁
- **程度定位:** 「有基礎想深入」 — 重點在 *story proof*、為什麼這樣定義、與其他結果的連結
- **語言:** **繁體中文**正文 / **英文**保留數學符號、變數、定理名、術語(prior, posterior, conditioning…)
- **節奏:** **一次只做一個小節**。使用者說「下一節」才繼續,不要自作主張連做。
- **不要再做的事:** 不需要事前提案敘事腳本,直接製作即可

---

## 3. 嚴格的內容規則(這是最重要的一條,違反就重寫)

HTML 是**原書內容的忠實互動化**,不是「我重新設計一個教學體驗」。具體:

1. **不能加書裡沒有的例子。** 書中 §2.1 用「下雨 R + 烏雲 C」,我就用這個 — 不能把 3b1b 的 Steve 塞進來,也不能編一個「醫療檢測」的例子,除非書中真的有。
2. **不能改書的章節編排。** 書怎麼鋪陳就怎麼鋪陳。順序、強調、術語引入時機都跟著書走。
2a. **忠實 vs 敘事的裁決規則(C 原則)。** 敘事「形式」學 `example` 的 3b1b 風格,但內容與編排忠於原書。當書序與流暢敘事衝突時,依下列判準裁決:
   - **錨點不可動。** 書中以粗體、置中、或獨立宣告形式突出的句子(定義、定理、關鍵 mantra)是「認得出這節」的錨點。它們的**出現順序**要跟書一致,地位要對等(用 `.bookq` 引用)。**多個錨點彼此的相對順序也鎖死** — 書是 D1→D2,HTML 就不能做成 D2→D1。
   - **路可以重鋪。** 純解釋性、鋪陳性的段落可為直覺微調順序(例如把書中較晚的例子提前養直覺),**但該站 `.src-tag` 必須標出它真正對應書中哪一段**,讓讀者翻書能對上。
   - **煞車:重排不能逼出新內容。** 重排前自問:這個例子提前後,是否需要用到尚未出現的 notation 或概念?若是,**保持書序**,不要硬搬,也不要自行補書中沒有的橋接說明。
   - **一句話:** 重排的是「怎麼把讀者帶到錨點」,不是錨點本身的位置。
3. **核心句、關鍵詞、定義必須照原書。** 包含 notation、英文術語、書中粗體或置中突出的句子,在 HTML 裡要保留同等地位(可用 `.bookq` 區塊直接引用,標 `SOURCE` tag)。
4. **每一站要能溯源到書中段落。** HTML 的每個 stage 內部要用 `<span class="src-tag">p.XX ¶N</span>` 之類標記告訴讀者「這站對應書中哪段」。
5. **互動 = 純粹的 additive layer。** 蘇格拉底提問、滑桿、視覺化、gating 都是為了讓書中那段「更可感」,不能取代或繞過書中的論述。
6. **不強加視覺互動。** 若書中該節**沒有插圖**,不要硬塞 Canvas / 滑桿 / 動畫。引導問題、reflection、reveal 是 OK 的(屬於閱讀引導,不是視覺化)。**只有書中有圖示或圖解的地方,才加視覺互動。**
7. **站數視內容多寡決定。** §2.1 只有 4 段 → 4 站 + Hero + Finale。長一點的節可能 6–8 站。不要套固定模板。
8. **過長節維持一節一檔。** 站數由「錨點數量 + 必要鋪陳」決定,不套固定數字,也不設硬上限。一節再長也維持單一 HTML 檔,**不拆成 `2-7a` / `2-7b`**(整套命名、進度、驗收都建立在「一節一檔」上;scroll-as-story 形式裡「滾很長」不是缺點)。但若展開後站數偏多(粗估超過 8–9 站、讀起來像爬樓梯),先檢查是不是把解釋性段落各自切成一站了 —— **錨點才需要獨立的站,鋪陳併入鄰近錨點那一站。**

**驗收標準:** 讀完 HTML → 翻開 PDF 對應幾頁 → 應該感覺「對,就是這節,只是書是靜態文字,我剛才是動態走過」。

---

## 4. 工作流程(每個小節依序執行)

```
1. 用 pdftotext 讀該節原文
   → cd /tmp && pdftotext -layout "<PDF 路徑>" full.txt
   → grep -n "<該節英文標題>" full.txt 找起點
   → sed -n 'A,Bp' full.txt 讀那幾段
2. 心中規劃 stages — 不需要寫提案給使用者
   → 每個 stage 對應書中的段落/小節
   → 哪些地方需要引導問題(reflection / multi-choice / fill-in)
   → 哪些地方書中有圖 → 才設計視覺化
3. 直接寫單一 HTML 檔
   → 路徑:Blitzstein/chXX/X-Y.html(zero-padded ch)
   → 沿用 example/bayes-theorem.html 的設計 DNA(見第 5 節)
4. 簡短回報給使用者(站數、對應段落、加了哪些互動)
5. 使用者開檔驗證 → 給回饋 → 等他說「下一節」
```

---

## 5. 設計 DNA(沿用 `Blitzstein/example/bayes-theorem.html`)

**這是設計參考檔,永遠不要修改。** 它是 3blue1brown Bayes' theorem 文章的忠實互動化,使用者把它當作我所有產出的品質基準。

### 視覺
- **暗色主題** + radial gradient + grain overlay
- **字體三件套(Google Fonts):**
  - Headings — `Newsreader` serif
  - Mono / labels / notation — `Spline Sans Mono`
  - Body — `Noto Sans TC`
- **語意色系統(每節按主題調整):**
  - 例:§2.1 的色:`--belief: #c9a227`(金,代表信念/機率)+ `--evi: #d4663a`(橘,代表證據/條件)
  - 例:§2.2 可考慮 `--A: 金`、`--B: 藍`、`--A∩B: 綠`(配合 pebble world 例子)
- **頂部進度條** + **右側站點圓點**(`#rail` / `#dots`)

### 結構
- 單頁滾動式敘事(scroll-as-story)
- Hero(eyebrow + serif h1 + hero-quote + scroll hint)
- Stages(每站:stage-tag → h2 + `.src-tag` → 段落 → 互動卡)
- Finale(recap + 通往下一節)

### 互動模式(按需挑選)
| 類型 | 何時用 | 元件 |
|---|---|---|
| 引用書中原話 | 書中粗體 / 置中句 / 關鍵宣告 | `.bookq` + `SOURCE` 標記 |
| 多選題 | 有明確對錯的驗證 | `.q .opts .opt` + `.feedback` |
| 反思 + reveal | 開放性思考、無標準答案 | `.q.reflect` + `textarea` + `[data-reveal]` 按鈕 |
| Gated 內容 | 答完才看後續 | `.gated[data-gate]` |
| 漸進式記號揭示 | 一連串符號逐行出現 | `.notation .nrow[style="--i:N"]` |
| 視覺化(僅當書有圖) | Canvas / 滑桿 / SVG | 視情況設計 |

### 技術
- **單一自含 HTML 檔**,無 build、無 npm
- **無 MathJax**(沿用 example 風格)。數學記號用 `<code>` 樣式或 Unicode(∩, ∪, ∈, ≤, Σ, ∞ 等);若公式複雜到 `<code>` 醜,**才**個別加 MathJax CDN
  - **切換觸發點:** 進入隨機變數章節(PMF/PDF、求和上下標、組合數、積分)後,Unicode 會開始醜。屆時若一節內 `<code>` 公式超過 3–4 處,**直接整頁載 MathJax**,不要逐式糾結。
- LocalStorage 可存:勾選狀態、展開過的 details(視需要)
- 響應式:flex/grid + max-width 720px wrap

### CSS 樣式速查
- `.bookq` — 直接引用書中原文(金色左邊線 + 微亮金背景 + `SOURCE` tag)
- `.src-tag` — h2 旁邊小標記書中頁碼段落
- `.mantra` — 大字置中 italic 收尾句
- `.notation` — 漸進顯示的符號表格
- `code` — inline 數學記號(Spline Mono + 微金背景 + nowrap)

---

## 6. 檔案結構

```
~/Documents/claude 學習/
├── CLAUDE.md                              ← 你在讀的這份
├── Introduction to Probability ...pdf     ← 原書
└── Blitzstein/
    ├── example/
    │   └── bayes-theorem.html             ← 設計 DNA 參考檔,永遠不要改
    ├── ch02/
    │   ├── 2-1.html                       ← §2.1 完成版
    │   └── 2-2-draft.html                 ← 反面教材,勿沿用(詳見第 9 節第 5 條)
    ├── ch03/                              ← 之後依此類推
    │   └── ...
    └── ...
```

**命名規則:** `ch` + zero-padded 章號 / `X-Y.html`(章-節,半形 dash)。

---

## 7. 當前進度(每完成一節就更新這節)

| 章 | 節 | 標題 | 狀態 | 檔案 |
|---|---|---|---|---|
| 2 | 2.1 | The importance of thinking conditionally | ✅ 完成 | `Blitzstein/ch02/2-1.html` |
| 2 | 2.2 | Definition and intuition | ✅ 完成 | `Blitzstein/ch02/2-2.html` |
| 2 | 2.3 | Bayes' rule and the law of total probability | ✅ 完成 | `Blitzstein/ch02/2-3.html` |
| 2 | 2.4 | Conditional probabilities are probabilities | ⏳ 下一個 | |
| 2 | 2.5 | Independence of events | – | |
| 2 | 2.6 | Coherency of Bayes' rule | – | |
| 2 | 2.7 | Conditioning as a problem-solving tool | – | |
| 2 | 2.8 | Pitfalls and paradoxes | – | |

**第二章後續:** 2.10 R、2.11 Exercises **一律不做**。2.9 Recap **預設做**(對複習有用)。

> **Recap 的性質是回顧而非引入。** 做法以**串連整章已出現的錨點、呈現它們之間的連結**為主(呼應書中 recap 段落怎麼收束),不需要再為 recap 設計新的蘇格拉底提問或視覺化,除非書中 recap 本身有圖。它是把整章已走過的錨點重新串成一條線,不是又一個獨立教學單元。

---

## 8. 技術環境前置

- **作業系統:** macOS(Apple Silicon, `/opt/homebrew`)
- **必裝工具:** `brew install poppler` → 提供 `pdftotext` `pdfinfo` `pdftoppm`
- **PDF 路徑:** `~/Documents/claude 學習/Introduction to Probability by Joseph K. Blitzstein, Jessica Hwang (z-lib.org).pdf`(636 頁,書中 §2.1 在書頁 p.45)
- 任何新環境(換電腦)首次使用時要重跑:`brew install poppler`

---

## 9. 已踩過的雷(避免重蹈)

1. **❌ 靠記憶寫,不讀 PDF** → 結果把 §2.1、§2.2、§2.3 內容混在一起、章節編排錯誤
   **✅ 修正:** 每節都必須先 `pdftotext` 讀原文
2. **❌ 用「6 個固定區塊」(學習目標 / 蘇格拉底 / 視覺化 / 原則 / 自我檢驗 / checklist)** → 太教科書,失去敘事
   **✅ 修正:** Stages 對應書中段落,站數與互動視內容而定
3. **❌ 強加視覺化(6×6 pebble grid 在 §2.1)** → 書中那節沒圖,硬塞顯得多餘
   **✅ 修正:** 只有書中有圖示時才加視覺化
4. **❌ 用 `$...$` LaTeX 但沒載 MathJax** → 顯示成原始文字
   **✅ 修正:** 用 `<code>...</code>` 或 Unicode 數學符號;複雜公式才考慮加 MathJax
5. **❌ `2-2-draft.html` 是早期記錯章節 + 用舊模板的產物** → 它是**反面教材,不是參考檔**。
   **✅ 修正:** 做 2.2 時從頭來,**唯一的設計參考是 `example/bayes-theorem.html`**,不要沿用 draft 的任何結構。

---

## 10. 多 session / 多電腦工作流(重要)

### 真相來源(Source of Truth)
**GitHub repository 是這個專案的家**:https://github.com/Jimmy-hola/probability-notes

- 任何電腦、任何 session 都從 GitHub `git clone` / `git pull` 取得最新狀態
- Google Drive 已退役(只當第二層備份,可選)
- PDF 原書檔案**不在 git 裡**(`.gitignore` 排除),需獨立放在工作電腦上

### 進度同步協定(處理多 session/多電腦的不一致)

**每個新 session 開頭,AI 必須先做這三件事:**

1. `git pull` — 拿到最新狀態
2. 讀 §7 進度表
3. `ls Blitzstein/ch??/` — 確認檔案系統實際狀態
4. **若進度表與檔案系統不一致 → 以檔案系統為準**,並更新進度表

**每完成一節後,AI 必須做這三件事(同一個 commit 內):**

1. 更新本檔(§7 進度表)— 該節改 ✅,下一節改 ⏳
2. 更新 `Blitzstein/index.html` — 該卡片改 `badge-done` 並啟用連結;下一節改 `badge-next`
3. `git add -A && git commit -m "Add §X.Y"`(commit 但**先不 push**)
4. 等使用者驗證滿意 → 使用者說「推一下」/「push」/「推上去」→ 才 `git push`

### 換電腦快速啟動

```bash
# 第一次在新電腦(包含公司電腦):
git clone https://github.com/Jimmy-hola/probability-notes.git
cd probability-notes
brew install poppler   # macOS;其他系統用對應 PDF 工具
# 把 PDF 放進這個資料夾(從原電腦複製或 Drive 抓)
```

之後告訴 Claude:「**繼續做下一節**」 — 他會 `git pull` → 讀 CLAUDE.md → 掃資料夾 → 推斷下一節 → 開工。

### 給未來 Claude 的開場 SOP

新 session 進來,**第一條訊息**應該回:

> 「我先 `git pull`,然後讀 CLAUDE.md + 掃 `Blitzstein/ch??/`,確認最新進度後再開始。」

實際執行:`git pull && ls Blitzstein/ch*/` → 對照 §7 → 必要時更新 → 開始做下一節。

如果新的 Claude 沒有照這個 SOP 走,就把這份檔案的網址丟給他、要求他重讀。
