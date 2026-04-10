---
type: review
created: 2026-04-10
topic: 六模型 wiki 品質盲測比較
source: Aitken2020 (AVF patency RCT, JASN)
---

# 六款 AI 模型寫同一篇腎臟科 Wiki：品質盲測

## 測試設計

同一篇論文（Aitken 2020, JASN — AVF 區域麻醉 vs 局部麻醉 RCT, N=126），餵給六款模型，要求產出「腎臟專科考試導向 wiki」，格式規範相同（禁 LaTeX、需含 Exam Logic / Textbook Ref / Key Trials）。各模型獨立運作，互不參照。

---

## 模型一覽

| 模型 | 類型 | Token 消耗 | 生成時間 | 成本 |
|---|---|---|---|---|
| **Gemma 4 8B** (Q4_K_M) | 本地 ollama | 0（免費） | 41 秒 | $0 |
| **Gemma 4 31B** (Q4_K_M) | 本地 ollama | 0（免費） | 189 秒 | $0 |
| **Codex (GPT-5.4)** | OpenAI API | 21,176 | 253 秒 | ~$0.15 |
| **Claude Opus 4.6** | Anthropic API | 32,967 | 88 秒 | ~$0.50 |
| **Claude Sonnet 4.6** | Anthropic API | 25,121 | 60 秒 | ~$0.10 |
| **Claude Haiku 4.5** | Anthropic API | 65,730 | 32 秒 | ~$0.03 |

---

## 品質比較

### 1. 資料準確度

| 指標 | Gemma 8B | Gemma 31B | Codex | Opus | Sonnet | Haiku |
|---|---|---|---|---|---|---|
| N=126 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Primary patency 79% vs 59% | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Functional patency 68% vs 49% | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| P-values (P=0.02, P<0.01) | ❌ 漏掉 | ✅ | ✅ | ✅ | ✅ | ✅ |
| OR + 95% CI | ❌ 無 CI | ✅ | ✅ | ✅ | ✅ | ✅ |
| Fragility index = 2 | ❌ 未提 | ❌ 未提 | ✅ | ✅ | ✅ | ✅ |
| RCF vs BCF 亞組 | ❌ 未提 | ❌ 未提 | ✅ | ✅ | ✅ | ✅ |
| 成本效益 ICER | ✅ 概述 | ✅ 概述 | ✅ | ✅ | ✅ | ✅ |
| Logistic regression OR 0.35 | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| Late maturation (n=24) | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |

### 2. 臨床深度

| 面向 | Gemma 8B | Gemma 31B | Codex | Opus | Sonnet | Haiku |
|---|---|---|---|---|---|---|
| 機轉解釋 | 基本 | 基本 | 簡潔 | 完整流程圖 | 分步驟 | 詳細 |
| Distractor 分析 | 列出 3 個 | 列出 + 為何錯 | 簡要 | 5 題 + 表格 | 5 題 Q&A | 5 個考試角度 |
| 亞組解讀 | ❌ | ❌ | ✅ 點到 | ✅ 生物學解釋 | ✅ 機轉連結 | ✅ 比例效應 |
| NNT 計算 | ❌ | ❌ | ❌ | ✅ (≈5) | ❌ | ❌ |
| Fragility index 教學 | ❌ | ❌ | ✅ 一句 | ✅ 定義 + 考試意義 | ✅ 獨立段落 | ✅ 解釋 |
| Causal reasoning (Hernán) | ❌ | ❌ | ❌ | ✅ 四項檢核 | ❌ | ❌ |
| 臨床 bottom line | 一般 | 一般 | ✅ | ✅ NNT + 建議 | ✅ pearls | ✅ implementation |

### 3. 格式合規

| 規範 | Gemma 8B | Gemma 31B | Codex | Opus | Sonnet | Haiku |
|---|---|---|---|---|---|---|
| LaTeX ban | ❌ 2處 | ❌ 3處 | ✅ | ✅ | ✅ | ✅ |
| Topic-based H1 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| ## Exam Logic | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| ## Textbook Ref | ❌ 無章節號 | ❌ 無章節號 | ✅ 有章節號 | ✅ 有章節號+內容 | ✅ 有描述 | ✅ 有章節號 |
| ## Key Trials | ✅ 1篇 | ✅ 1篇 | ✅ 1篇 | ✅ 3篇 | ✅ 4篇 | ✅ 4篇 |
| YAML frontmatter | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

### 4. 輸出效率

| 模型 | 字數 | 行數 | 資訊密度 |
|---|---|---|---|
| Gemma 8B | ~2,100 | 57 | 低（有 filler） |
| Gemma 31B | ~1,800 | 39 | 中 |
| Codex | ~1,600 | 37 | 高（極簡） |
| Opus | ~4,500 | 130 | 極高（最完整） |
| Sonnet | ~3,800 | 152 | 高（結構清晰） |
| Haiku | ~4,200 | 167 | 高（最長但全面） |

---

## 綜合排名

| 排名 | 模型 | 強項 | 弱項 |
|---|---|---|---|
| 🥇 | **Opus 4.6** | 唯一做到 causal reasoning checklist、NNT、fragility 教學、5 題考題 + distractor 表。臨床推理最深 | 最貴（~$0.50），token 最多 |
| 🥈 | **Sonnet 4.6** | 結構最清晰、Q&A 格式好、clinical pearls 實用、性價比最高 | 無 NNT、無 causal check |
| 🥉 | **Haiku 4.5** | 最快（32s）、全面度接近 Sonnet、含 implementation 段落 | Token 異常高（65K）、教科書版本過舊（Nissenson 4e, Daugirdas 5e） |
| 4 | **Codex (GPT-5.4)** | 最精簡高效、章節號最具體 | 過於壓縮、無機轉圖、無亞組解釋 |
| 5 | **Gemma 4 31B** | 免費、P-values 正確、比 8B 好 | 漏 fragility index、無亞組、LaTeX violation |
| 6 | **Gemma 4 8B** | 免費、最快 | 漏 P-values、漏 CI、LaTeX violation、臨床深度不足 |

---

## 結論

1. **品質天花板 = Opus**：causal reasoning、fragility 解讀、NNT 計算 — 只有 Opus 做到全套。適合高品質 wiki 產出。
2. **性價比冠軍 = Sonnet**：品質接近 Opus 的 80%，成本只有 1/5。適合批量產出。
3. **免費方案 = Gemma 31B**：堪用但需 post-processing（LaTeX 替換、補 fragility、補亞組）。適合初稿 + 人工/AI 審核。
4. **Gemma 8B 不推薦用於醫學 wiki**：遺漏太多關鍵數據。
5. **Codex = 快速精簡摘要**：適合考前速查卡，不適合完整 wiki。
6. **Haiku 需注意教科書版本**：引用了過舊的版本號，可能誤導。

### 最佳工作流建議

```
Gemma 31B (免費批量初稿)
  → Sonnet (審核 + 補齊)
  → Opus (抽樣 editorial review)
```

這個三層流水線兼顧成本與品質，符合 nephrology-wiki 的 multi-author model。
