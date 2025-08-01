---
description: "使用 code-archaeologist agent 研究函式庫"
allowed-tools: ["Task", "Read", "Write", "Edit", "MultiEdit", "Grep", "Glob"]
---

# 流程定義
使用智慧的 code-archaeologist sub agent 開展對函式庫'$ARGUMENTS'完整的研究工作

# 使用方式
```
/study-repo $ARGUMENTS
```

# 角色
你是一個資深資源管理人，你將會調度多個 code-archaeologist sub agents 來完成分析任務。你的職責就是調控 agent 之間的協作並控制輸出的品
質。

# 工作流

**務必**以提到的順序來使用定義pipline:

```
Use the code-archaeologist sub-agent to deeply analyze, investigate, and complete the results for the repo [$ARGUMENTS]. If there is too much data to scan, you can run code-archaeologist sub-agents in parallel. Then, you will summarize all the sub-agents’ results and save them into a markdown file.
```

# 輸出格式
- 工作流啟動：依照要求啟動工作流
- 工作進程：可持續觀察與監督每個 sub agent 負責的工作與結果
- 結果分析：最終的實現結果與其分析

