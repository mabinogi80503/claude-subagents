---
description: "以新想法啟動 multi-agent 開發工作流"
allowed-tools: ["Task", "Read", "Write", "Edit", "MultiEdit", "Grep", "Glob", "TodoWrite"]
---

# Multi-Agent 開發工作流

智慧化協調多個專業 Sub-Agent，將創意想法轉化為完整可執行的軟體解決方案。

## 指令用法
```bash
/agent-go [功能描述或開發需求]
```

## 工作流定位

### 輸入參數
- **$ARGUMENTS**: 待開發的功能需求或創意想法
- **工作模式**: 結構化、智慧化的 Sub-Agent 協作流程

### 協調者角色
Multi-Agent 工作流協調者，嚴格遵循 Claude Code Sub-Agent Pipeline 標準。負責：
- 統籌各 Agent 間的協作流程
- 監控每階段的輸出品質
- 確保最終交付成果符合需求

## Agent 團隊組成

| Agent 角色 | 職責範圍 |
|-----------|----------|
| **code-dispositor** | 需求分析師 - 將模糊需求轉化為結構化規格文件 |
| **code-architect** | 系統架構師 - 建立技術架構與系統設計文件 |
| **code-plan** | 專案經理 - 將架構轉換為可執行的任務分解 |
| **domain-backend-developer** | 領域專家 - 依據規格實現特定領域功能 |
| **code-reviewer** | 品質檢核師 - 程式碼審查與品質評分 |

## 標準執行流程

### Pipeline 執行序列
**嚴格按照以下順序執行 Sub-Agent 鏈：**

```
code-dispositor → code-architect → code-plan → domain-backend-developer → code-reviewer
```

**流程說明**：
1. **需求分析**: `code-dispositor` 生成完整需求規格
2. **架構設計**: `code-architect` 建立系統架構文件
3. **任務規劃**: `code-plan` 拆解為可執行任務集合
4. **功能實作**: `[domain]-backend-developer` 依規格開發
5. **品質審查**: `code-reviewer` 評估程式碼品質與評分

### 品質迭代機制
- **評分標準**: 95 分以上視為穩定可接受
- **迭代條件**: 未達標準時重新優化架構設計
- **最終最佳化**: 達標後進行效能與程式碼品質最佳化

## 執行階段輸出

### 1. 工作流啟動
- 接收需求參數並驗證
- 初始化 Agent 協作環境
- 啟動 Pipeline 執行序列

### 2. 階段性監控
- 即時追蹤各 Agent 執行狀態
- 監控階段性交付物品質
- 提供進度回饋與異常處理

### 3. 成果交付
- 完整功能實作結果
- 品質評估報告與建議
- 專案交付文件與維護指南

---
**工作流理念**: 專業分工、品質導向、迭代優化、協作高效

