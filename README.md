# Introduction to Probability — 互動式自學筆記

> Personal interactive study notes for Blitzstein & Hwang's *Introduction to Probability* (2nd ed.)

這是一份**個人學習用**的互動式 HTML 筆記,把 Blitzstein & Hwang《Introduction to Probability》(2nd ed., CRC Press, 2019)的每一個小節做成一個可以滾動閱讀、回答問題、看視覺化的單頁 HTML。

📖 線上閱讀: https://jimmy-hola.github.io/probability-notes/Blitzstein/
(GitHub Pages 啟用後生效)

---

## 著作權與引用聲明 / Copyright & Attribution

**Source book (原書):**
> Blitzstein, Joseph K., and Jessica Hwang. *Introduction to Probability*. 2nd ed., Chapman and Hall/CRC, 2019. ISBN 978-1138369917.

本專案的 HTML 內容**改編自上述著作**,部分章節包含書中的:
- **直接引文(direct quotations)** — 在 HTML 中以 `.bookq` 區塊呈現,並標註頁碼來源(`SOURCE: §X.X ¶N, p.XX`)
- **觀念與編排結構** — 嚴格依照原書的章節編排與論述順序
- **書中使用的例題、記號、術語** — 例如 §2.1 的「下雨 R + 烏雲 C」例子直接取自書中 p.45

**著作財產權歸屬:** 原書內容(包含定義、定理、例題、論述、術語)的著作權屬於 Joseph K. Blitzstein、Jessica Hwang 與出版社 Chapman and Hall/CRC,本專案不主張任何書面內容的著作權。

**本專案的性質:** 此為個人非商業學習筆記,符合教育目的之合理使用(fair use)原則:
- 引用量少(每節僅引用書中幾句關鍵句,非整章複製)
- 高度轉化性(加入互動、引導問題、視覺化 — 非單純轉貼)
- 非商業用途(個人學習,無營利)
- 不取代原書(實際上引導讀者購買原書深入閱讀)

**強烈推薦購買原書:** 本筆記不能取代閱讀完整的原書 — 它只是把某些段落變得「更可感」的輔助工具。原書有完整的證明、例題、練習題、與許多本筆記未涵蓋的章節。

- 📚 [Amazon](https://www.amazon.com/Introduction-Probability-Chapman-Statistical-Science/dp/1138369918)
- 📚 [CRC Press 官方](https://www.routledge.com/Introduction-to-Probability-Second-Edition/Blitzstein-Hwang/p/book/9781138369917)
- 🌐 作者官方網站(含 PDF、影片、額外資源): [stat110.net](https://projects.iq.harvard.edu/stat110)

如果原書作者或出版社認為本專案的任何部分逾越合理使用範圍,請[開 issue](https://github.com/jimmy-hola/probability-notes/issues) 告知,我會立即移除相關內容。

---

## 授權 / License

| 內容類別 | 著作權狀態 |
|---|---|
| **互動 HTML / CSS / JS 程式碼** | 我自己撰寫,以 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh-hant) 釋出(姓名標示-非商業性-相同方式分享) |
| **書中引文與改編論述** | 著作權屬於原書作者與出版社 — 本專案僅以教育目的之合理使用引用 |
| **設計參考檔 `Blitzstein/example/bayes-theorem.html`** | 內容改編自 [3Blue1Brown — Bayes' theorem](https://www.3blue1brown.com/lessons/bayes-theorem)(Grant Sanderson) |

---

## 專案結構

```
.
├── CLAUDE.md                    # AI 協作說明 + 完整 SOP
├── Blitzstein/
│   ├── index.html               # 行動裝置友善的導覽首頁
│   ├── example/
│   │   └── bayes-theorem.html   # 設計參考檔(3b1b 風格)
│   └── chXX/
│       └── X-Y.html             # 每節一檔
```

---

## 進度

詳見 [`CLAUDE.md`](./CLAUDE.md) 第 7 節。

目前完成:**§2.1 The importance of thinking conditionally**

---

## 致謝

- **Joseph K. Blitzstein & Jessica Hwang** — 寫出這本清晰、有 story-proof 精神的好書
- **Grant Sanderson (3Blue1Brown)** — 互動式教學設計的靈感來源
- **Anthropic Claude** — 協助執行互動 HTML 的撰寫

— *jimmylion,2026*
