---
description: "已新想法展開 multi-agent 開發工作流"
allowed-tools: ["Task", "Read", "Write", "Edit", "MultiEdit", "Grep", "Glob", "TodoWrite"]
---

# 開發工作流程定義
使用結構化的、智慧化的 sub agents 開展完整的開發工作流

## 使用方式
```
/agent-go <FEATURE_DESCRIPTION>
```

## Context
- 要開發的功能或想法: $ARGUMENTS
- 使用結構化的、智慧化的 sub agents 的開發工作流

## 角色
你是一個工作流協調人員，**遵守**Claude Code Sub agents pipeline。你的職責就是調控每一個 agent 之間的協作並控制輸出的品
質。

## Agents
code-architect sub agent: 建立基礎，建立 code-architect.md
backend-developer sub agent: 依照 spec 進行實作
code-reviewer sub agent: review與給 code 的品質評價

## Sub Agents Pipeline

**務必**以提到的順序來使用定義pipline:

```
First, use the code-architect sub agent to generate complete specifications for [$ARGUMENTS] and design system architecture, then use the backend-developer sub agent to implement code based on specifications, then use the code-reviewer sub agent to evaluate code quality with scoring; otherwise first use the code-architect sub agent again to improve specifications and repeat the chain.
```

### 預期流程
1. 初步實作功能
2. 依照 reviewer 提供的意見重新精練程式碼（反覆迭代）
3. 穩定後最佳化程式碼

## 輸出格式
- 工作流啟動：依照要求啟動工作流
- 工作進程：可持續觀察與監督每個 sub agent 負責的工作與結果
- 結果分析：最終的實現結果與其情報分析

