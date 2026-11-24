# Wiki 索引

本頁是「從餐廳訂位看懂 RAG」知識庫的內容入口。新增或更新頁面時，應同步維護此索引。

## 入門與流程

- [RAG 入門總覽](<topics/RAG 入門總覽.md>)：從零開始認識 RAG 的用途與整體流程。
- [餐廳訂位流程](<topics/餐廳訂位流程.md>)：以餐廳客服機器人串起 RAG 的各個步驟。

## RAG 核心階段

- [檢索](topics/檢索.md)：AI 如何從餐廳資料中找到可能相關的內容。
- [生成](topics/生成.md)：模型如何根據找到的內容組織答案。
- [評估](topics/評估.md)：如何判斷檢索結果與最終回答是否可靠。

## 學習與產出

- [術語表](術語表.md)：面向 AI 初學者的中英術語解釋。
- [簡報大綱](簡報大綱.md)：以論文證據支撐的簡報結構。
- [簡報逐頁稿](簡報逐頁稿.md)：經確認的 13 頁畫面文字、講解重點、視覺安排與引用配置。
- [故障注入測試](故障注入測試.md)：記錄錯分店與虛構空位兩項人為錯誤、回退節點及複查結果。

## 案例來源

- [餐廳訂位模擬資料](../examples/restaurant-booking.md)：經核准的自編教學示例，含固定資料 ID、主測試問題及證據邊界。

## 論文筆記

- [Dense Passage Retrieval for Open-Domain Question Answering](<papers/Dense Passage Retrieval for Open-Domain Question Answering.md>)：DPR 的架構、檢索實驗、與 BM25 的差異及適用限制。
- [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](<papers/Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks.md>)：RAG 的檢索與生成架構、參數式／非參數式記憶、生成效果與限制。
- [Lost in the Middle - How Language Models Use Long Contexts](<papers/Lost in the Middle - How Language Models Use Long Contexts.md>)：長上下文中的資訊位置效應、更多文件的取捨及位置穩定性評估。
- [Ragas - Automated Evaluation of Retrieval Augmented Generation](<papers/Ragas - Automated Evaluation of Retrieval Augmented Generation.md>)：忠實度、回答相關性、上下文相關性的自動評估方法與限制。
- [SELF-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection](<papers/SELF-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection.md>)：按需檢索、反思標記、批判引導生成及其實驗限制。

進度：已匯入 5／5 篇主要論文。

## 最終成果

- [教學型 HTML 簡報](../output/slides/index.html)：13 頁「從餐廳訂位看懂 RAG」，含離線論文引用、案例資料與鍵盤／按鈕翻頁。

