---
description: "已新想法展開 multi-agent 開發工作流"
allowed-tools: ["Task", "Read", "Write", "Edit", "MultiEdit", "Grep", "Glob", "TodoWrite"]
---

# 開發工作流程定義
使用結構化的、智慧化的 sub agents 開展完整的開發工作流

## 使用方式
```
/agent-go $ARGUMENTS
```

## Context
- 要開發的功能或想法: $ARGUMENTS
- 使用結構化的、智慧化的 sub agents 的開發工作流

## 角色
你是一個工作流協調人員，**遵守**Claude Code Sub agents pipeline。你的職責是調控每一個 agent 之間的協作並控制輸出的品
質。

## Agents
code-dispositor sub agent: 將使用者的模糊需求轉換為結構化可行的需求檔案
code-architect sub agent: 從需求建立技術基礎，建立 code-architect.md
code-plan sub agent: 將 architect 提出的架構轉換為可執行實作的任務集合
domain-backend-developer sub agent: 具特定領域知識的實作者，會依照 spec 實現功能
code-reviewer sub agent: review 與並給予 code 品質評價

## Sub Agents Pipeline

**務必**以提到的順序來使用定義pipline:

```
First, use the code-dispositor sub agent to generate complete specifications for [$ARGUMENTS]. Then, the code-architect sub agent to will design system architecture; then code-plan will will convert the architecture documents into a set of actionable tasks for developers; then use the [domain]-backend-developer sub agent to implement code based on spec and tasks, then use the code-reviewer sub agent to evaluate code quality with scoring; otherwise first use the code-architect sub agent again to improve specifications and repeat the chain.
```

### 預期流程
1. 將使用者的要求轉換成完整的 specification
2. 將 specification 轉換為系統工程文件
3. developer 依照系統工程文件逐步實作程式碼
4. 依照 reviewer 提供的意見與評價重新精練程式碼（反覆迭代）
5. 足夠穩定後(分數在 95 分以上)，最佳化程式碼
6. 功能實作完畢！

## 輸出格式
- 工作流啟動：依照要求啟動工作流
- 工作進程：可持續觀察與監督每個 sub agent 負責的工作與結果
- 結果分析：最終的實現結果與分析

