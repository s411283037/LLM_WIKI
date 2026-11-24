# RAG 入門總覽

> 狀態：已匯入 5／5 篇主要論文；已涵蓋檢索、生成、長上下文限制、評估與自我反思。

## 讀完這頁能理解什麼

- RAG 想解決的問題。
- RAG 的基本流程。
- RAG 與一般聊天機器人回答方式的差別。
- 餐廳訂位案例中的資料、檢索與回答如何對應。

## 必要先備知識

- AI 回答問題前，需要取得能支持答案的資料。
- 「找到資料」與「根據資料形成答案」是兩個不同問題，應分開理解與評估。[[../papers/Dense Passage Retrieval for Open-Domain Question Answering#開放領域問答的兩階段流程]]

## 一句話理解 RAG

Retrieval-Augmented Generation, RAG（檢索增強生成）是先從外部資料找出相關文字，再讓生成模型同時參考問題與找到的內容產生答案。[[../papers/Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks#RAG 的基本架構]]

## 整體流程

1. 使用者提出問題。
2. 檢索系統從大量資料中找出少量可能相關的段落。[[../papers/Dense Passage Retrieval for Open-Domain Question Answering#DPR 如何表示與搜尋問題及段落]]
3. 生成模型把原問題與檢索到的文件一起作為上下文，產生答案。[[../papers/Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks#RAG 的基本架構]]
4. 分別評估是否找到可用資料，以及回答是否忠於證據、是否解決問題。第一篇論文能支持檢索與最終正確性需要分開；第二篇則顯示生成器可能使用檢索文件以外的參數知識。[[../papers/Dense Passage Retrieval for Open-Domain Question Answering#檢索表現與最終問答結果]] [[../papers/Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks#RAG 不只是複製檢索文字]]
5. 即使正確資料已放進輸入，也要檢查模型是否能在不同長度與位置下穩定使用。[[../papers/Lost in the Middle - How Language Models Use Long Contexts#評估長上下文時應測試不同資訊位置]]
6. 將「資料是否相關」、「回答是否受資料支持」與「回答是否回應問題」分開評估。[[../papers/Ragas - Automated Evaluation of Retrieval Augmented Generation#Ragas 將 RAG 評估拆成三個面向]]
7. 進階系統可以學習何時檢索並批判候選回答，但這需要專門訓練，且自我判斷仍可能出錯。[[../papers/SELF-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection#SELF-RAG 的三階段流程]]

相關頁面：[[餐廳訂位流程]]、[[檢索]]、[[生成]]、[[評估]]。

## 證據與來源

- [[../papers/Dense Passage Retrieval for Open-Domain Question Answering]]：提供檢索、兩階段問答流程與檢索評估的證據；不作為生成式回答機制的直接證據。
- [[../papers/Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks]]：提供檢索器與生成器結合、外部記憶更新及生成效果與限制的證據。
- [[../papers/Lost in the Middle - How Language Models Use Long Contexts]]：提供資訊位置、上下文長度及檢索文件數量如何影響回答模型的證據。
- [[../papers/Ragas - Automated Evaluation of Retrieval Augmented Generation]]：提供忠實度、回答相關性與上下文相關性的 reference-free 評估方法及限制。
- [[../papers/SELF-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection]]：提供按需檢索、反思標記、批判引導生成及其取捨的證據。

## 目前必須保留的界線

- 有檢索不等於回答完全由檢索內容支持；生成器可能使用參數知識。[[../papers/Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks#RAG 不只是複製檢索文字]]
- 外部資料可替換，不代表系統會自行判斷資料是否最新或正確。[[../papers/Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks#替換外部索引可更新可取得的知識]]
- 論文中的 RAG 架構是一種具體實作，不代表所有現代 RAG 系統的唯一形式。
- 模型能接收長輸入，不代表能穩定使用長輸入中的每個位置；影響程度依模型與任務而變。[[../papers/Lost in the Middle - How Language Models Use Long Contexts#長上下文容量不等於能有效使用長上下文]]
- 自動評估與模型自我反思都是品質檢查代理，不能取代原始來源核對與人工抽查。[[../papers/Ragas - Automated Evaluation of Retrieval Augmented Generation#限制與適用範圍]] [[../papers/SELF-RAG - Learning to Retrieve, Generate, and Critique through Self-Reflection#自我反思仍可能判斷錯誤]]

