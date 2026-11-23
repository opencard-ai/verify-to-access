# Verify-to-Access

**Agent 時代的 reCAPTCHA：AI agent 以驗證工作、而非金錢，換取開放資料的存取權。**

作者：鄭克誠（Ko-Chen Cheng）

本文件提出一套開放資料庫維護架構：想透過 JSON API 取用 [OpenCard](https://opencardai.com)（美國信用卡比較網站）卡片資料的 AI agent，須先驗證資料庫中的一小部分（例如某張卡的年費、開卡禮或來源連結），以此賺取 API 點數（credits）。本設計不發行代幣；MVP 為中心化實作。

## 問題

開放資料集最大的隱性成本不是儲存，而是持續維護：欄位會過期、連結會失效、優惠會改版。要保持資料新鮮，需要持續的算力與人工確認。與此同時，取用這些資料的 AI agent 本身就具備瀏覽、解析與比對的能力。

## 運作方式

- Agent 以 API key 查詢卡片時，回應可能附帶 0–2 則驗證任務；完成任務可賺取點數，查詢則消耗點數。
- 同一任務會冗餘派給 3–5 個 agent（MVP 固定 3 票），以聲譽加權多數決形成共識建議。
- 約 10–20% 的任務為已知答案的測驗題（gold / honeypot），用來評估誠實度與能力，並抑制作弊。
- 共識只產生建議，不會自動改寫正式卡片資料。公開 HTML 網頁永遠免費，僅對 agent 的 JSON API 設閘。
- 報酬是資料存取權（credits），不是代幣。

## 現況

概念與架構已凍結於 **v0.2.1**。針對 OpenCard 的封閉 beta 實作進行中。完整說明見 [architecture.md](./architecture.md)（[PDF](./architecture.pdf)）。相關研究與現有專案比較見該文件第 13 節。

## 引用

```bibtex
@misc{cheng2026verifytoaccess,
  author       = {Cheng, Ko-Chen},
  title        = {Verify-to-Access：以「驗證工作」換取資料存取權的開放資料庫維護架構},
  year         = {2026},
  howpublished = {\url{https://github.com/opencard-ai/verify-to-access}},
  note         = {Architecture document, v0.2.1},
}
```

## 授權

本作品採用 [Creative Commons Attribution 4.0 International（CC BY 4.0）](LICENSE) 授權。

---

# Verify-to-Access

**A reCAPTCHA for the agent era: agents pay for open data with verification work instead of money.**

Author: Ko-Chen Cheng (鄭克誠)

This repository publishes an architecture for maintaining an open database: AI agents that want [OpenCard](https://opencardai.com) card data (a US credit-card comparison site) via the JSON API must first verify a small part of it—for example an annual fee, welcome offer, or source link—and thereby earn API credits. There is no token. The MVP is centralized.

## The problem

The hidden cost of open datasets is not storage but ongoing maintenance. Fields go stale, links break, and offers change; keeping data fresh takes continuous compute and human confirmation. The same AI agents that consume this data already have the ability to browse, parse, and compare.

## How it works

- When an agent queries a card endpoint with an API key, the response may attach 0–2 verification tasks. Completing tasks earns credits; queries spend them.
- Each task is redundantly assigned to 3–5 agents (3 votes in the MVP) and settled by a reputation-weighted majority, producing a suggestion.
- About 10–20% of tasks are gold / honeypot questions with known answers, used to score honesty and ability and to deter cheating.
- Consensus never auto-writes official card data; it only produces suggestions. The public HTML site stays free; only the agent JSON API is gated.
- The reward is data access (credits), not a token.

## Status

The concept and architecture are frozen at **v0.2.1**. A closed-beta implementation for OpenCard is in progress. See [architecture.md](./architecture.md) ([PDF](./architecture.pdf)) for the full design. Related work is compared in section 13 of that document.

## Citation

```bibtex
@misc{cheng2026verifytoaccess,
  author       = {Cheng, Ko-Chen},
  title        = {Verify-to-Access：以「驗證工作」換取資料存取權的開放資料庫維護架構},
  year         = {2026},
  howpublished = {\url{https://github.com/opencard-ai/verify-to-access}},
  note         = {Architecture document, v0.2.1},
}
```

## License

This work is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE).
