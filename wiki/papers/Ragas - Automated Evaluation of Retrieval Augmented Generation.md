# Ragas: Automated Evaluation of Retrieval Augmented Generation

## 來源資訊

- 作者：Shahul Es、Jithin James、Luis Espinosa-Anke、Steven Schockaert
- 年份：2023（arXiv 初版；本專案所附檔案為 2025 年更新的 v2）
- 原文連結：[arXiv:2309.15217](https://arxiv.org/abs/2309.15217)
- 原始檔案：`raw/papers/2309.15217v2.pdf`

## 白話摘要

這篇論文提出 Ragas，一套不需要標準答案也能自動檢查 RAG 系統的評估方法。它把問題拆成三個面向：找到的內容是否聚焦、回答是否真正回應問題，以及回答中的主張是否能由找到的內容支持；但這些分數本身仍由 LLM 判斷，是評估代理而非絕對真相。

## 核心概念與術語

### Faithfulness（忠實度）

回答中的主張能否從提供的上下文推導出來。它關心回答是否有證據支持，不等同於外部世界中的絕對正確性。

### Answer relevance（回答相關性）

回答是否直接回應原始問題，並避免不完整或多餘內容；論文明確指出這項指標不評估事實正確性。

### Context relevance（上下文相關性）

檢索到的上下文是否聚焦於回答問題所需的資訊，並盡量少包含無關內容。

## 這篇在簡報中回答的問題

- 怎麼分辨「找錯資料」與「找到資料但回答超出證據」？
- 回答看似合理時，如何檢查每個主張是否有上下文支持？
- 為什麼檢索、生成與回答問題本身需要分開評估？
- 沒有人工標準答案時，能否做快速自動檢查？
- 自動評分是否能取代人工核對？
- RAG 階段：主要對應 **評估**；同時連結 **檢索**與**生成**。

## 原文依據

### Ragas 將 RAG 評估拆成三個面向

- 重點：論文聚焦 faithfulness、answer relevance 與 context relevance，並以 LLM 自動評估。
- 位置：PDF p. 3；§3。
- 證據界線：這三項是論文選定的核心面向，不代表已涵蓋延遲、成本、安全、完整性或所有實務品質需求。
- 相關頁面：[[../topics/評估]]。

### Faithfulness 的計算方式

- 重點：先把答案拆成多個主張，再由 LLM 判斷每個主張能否從上下文推導；分數為受支持主張數除以總主張數。
- 位置：PDF p. 3；§3，Faithfulness。
- 證據界線：它衡量相對於給定上下文的支持程度；若上下文本身錯誤，忠實回答仍可能不符合現實。
- 相關頁面：[[../topics/生成]]、[[../topics/評估]]。

### Answer relevance 不評估事實性

- 重點：論文以答案生成可能問題，再比較這些問題和原問題的 embedding cosine similarity；不完整或多餘答案會受罰。
- 位置：PDF p. 3；§3，Answer relevance；Equation 1。
- 證據界線：論文明確說這項評估不考慮 factuality，因此高相關性不能證明答案正確或有證據。
- 相關頁面：[[../topics/評估]]。

### Context relevance 衡量上下文是否聚焦

- 重點：LLM 從上下文抽出回答問題所需的句子，分數為抽取句數除以上下文總句數。
- 位置：PDF p. 3–4；§3，Context relevance；Equation 2。
- 證據界線：這是上下文聚焦程度的代理指標，不能完整取代傳統檢索召回率或確認是否漏掉必要來源。
- 相關頁面：[[../topics/檢索]]、[[../topics/評估]]。

### WikiEval 的驗證結果

- 重點：WikiEval 使用 50 個與 2022 年後事件有關的 Wikipedia 頁面，問題及部分比較答案由 ChatGPT 協助生成，再由兩位人工標註者比較。
- 位置：PDF p. 4；§4。
- 重點：在 pairwise comparison accuracy 中，Ragas 對 faithfulness、answer relevance、context relevance 與人工偏好的符合率分別為 0.95、0.78、0.70。
- 位置：PDF p. 5；§5；Table 1。
- 證據界線：這是小型、人工建構資料集上的成對比較準確率，不是三項指標在所有 RAG 系統上的通用可靠度。Context relevance 最難評估，尤其上下文較長時。

## 實際案例或實驗結果

### 教學用餐廳訂位對應

- 引用板橋店規回答信義店問題：主要暴露檢索／上下文相關性問題。
- 正確找到「七人須電話聯絡」，卻回答「晚上七點還有位」：暴露忠實度問題，因空位主張沒有上下文支持。
- 只回答「請電話聯絡」卻漏掉使用者問的空位：可能涉及回答相關性或完整性。

這是 **Wiki 教學類比**。正式資料 ID 與測試輸入須等案例提案獲准後建立。

## 限制與適用範圍

- Ragas 是 reference-free 評估代理，不是外部事實查核，也不能證明答案符合現實。
- 論文實作以 `gpt-3.5-turbo-16k` 作為評估 LLM，answer relevance 使用 `text-embedding-ada-002`。位置：PDF p. 3；§3。
- LLM 評分可能受模型、提示、輸出格式及答案呈現順序影響；論文的相關研究也指出 LLM 評估器可能有偏差。位置：PDF p. 2；§2。
- WikiEval 僅有 50 個 Wikipedia 頁面，且問題和對照答案部分由 ChatGPT 生成。位置：PDF p. 4；§4。
- Table 1 衡量的是和兩位標註者偏好的成對一致率，不是分數校準、跨語言穩定性或真實部署錯誤率。
- Context relevance 在實驗中最難，LLM 對較長上下文選取關鍵句時容易失敗。位置：PDF p. 5；§5。
- 論文中的公式與 2023 初版 Ragas 定義應和後續軟體版本區分；本 Wiki 只把論文作為研究證據。

## 衝突與未定論

這篇把前幾篇指出的失敗拆成可檢查面向：DPR 與 Lost in the Middle 關注是否找到並有效使用資料；RAG 論文指出生成器可能超出檢索內容；Ragas 則提供 reference-free 的自動評估代理。

> [!warning] 未定論
> - 自動 LLM 評分可加快迭代，但不能取代簡報核心主張的人工原文核對。
> - 高 faithfulness 只代表符合給定上下文；若上下文錯誤，答案仍可能錯誤。
> - 正式案例應同時保留規則式資料 ID 核對與 Ragas 類型的語意評估。

## 相關頁面

- [[../topics/RAG 入門總覽]]
- [[../topics/餐廳訂位流程]]
- [[../topics/檢索]]
- [[../topics/生成]]
- [[../topics/評估]]
- [[../術語表]]
- [[../簡報大綱]]
