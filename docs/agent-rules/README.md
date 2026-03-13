# agent-rules README

## 1. 目标

本目录用于承载项目中 Agent 的详细规则说明。  
项目根级 `AGENTS.md` 只保留最小必要规则与读取路由；更具体的说明拆分到本目录中，按需读取。

本目录遵循渐进式披露原则：

1. 根级 `AGENTS.md` 只放始终需要知道的最小规则
2. 详细规范放在本目录中
3. 局部业务经验放在更接近实际生效位置的局部 `AGENTS.md`
4. 不要把所有细节重新堆回项目根级文件

---

## 2. 使用原则

1. 遇到任务时，不要默认把本目录所有文件一次性读完。
2. 应根据任务类型选择性读取相关文件。
3. 若当前目录已有更局部的 `AGENTS.md`，应优先读取更局部的经验文件。
4. 本目录中的文档负责解释“通用规则”；某个具体页面、组件、链路的经验不应写在这里。

---

## 3. 文件索引

### 3.1 通用编码风格

适用场景：
- 不确定该跟随什么编码风格
- 不确定是否该引入 i18n
- 不确定该复用已有实现还是自己写

读取：
- `coding-style.md`

### 3.2 文件拆分与目录组织

适用场景：
- 不确定常量、类型、hooks、utils、services 是否该拆文件
- 不确定该如何组织当前目录代码结构
- 准备新增或调整某个模块文件结构

读取：
- `code-organization.md`

### 3.3 路径与导入

适用场景：
- 不确定该使用 alias 还是相对路径
- 不确定导入顺序或分组风格
- 准备调整导入路径

读取：
- `imports-and-paths.md`

### 3.4 组件设计与逻辑组织

适用场景：
- 组件过大
- 不确定是否要拆 hooks / utils / services
- 不确定状态该放哪一层
- 准备做页面结构重构

读取：
- `component-design.md`

### 3.5 Code Review

适用场景：
- 需要给 review 意见
- 不确定如何表达问题和替代方案
- 需要评估封装合理性、复杂度和维护成本

读取：
- `code-review.md`

### 3.6 经验沉淀总规则

适用场景：
- 准备沉淀经验
- 需要判断当前任务是否值得记忆
- 需要主动查找历史经验

读取：
- `memory-system.md`

### 3.7 经验作用域与写入位置

适用场景：
- 不确定经验该写到哪里
- 不确定是局部经验、模块经验还是项目经验
- 想避免把局部经验错误写到根级 `AGENTS.md`

读取：
- `memory-scoping.md`

### 3.8 经验过期、更新、删除、下沉

适用场景：
- 发现经验与代码不一致
- 准备改写或删除旧经验
- 准备把高层级经验下沉到局部目录

读取：
- `memory-update-and-pruning.md`

### 3.9 subagent 使用策略

适用场景：
- 任务可拆分
- 任务需要并行处理
- 需要主代理做规划和验收

读取：
- `subagent-strategy.md`

### 3.10 局部 AGENTS 模板

适用场景：
- 准备在某个模块目录创建局部 `AGENTS.md`
- 需要一份尽量短、具体、可维护的局部经验模板

读取：
- `local-agents-template.md`

---

## 4. 推荐读取顺序

### 4.1 普通新增或修改代码

优先读取：
1. `coding-style.md`
2. `code-organization.md`
3. `imports-and-paths.md`

### 4.2 组件封装、页面重构、状态管理问题

优先读取：
1. `component-design.md`
2. `code-organization.md`

### 4.3 做 code review

优先读取：
1. `code-review.md`
2. `component-design.md`
3. `coding-style.md`

### 4.4 沉淀新经验

优先读取：
1. `memory-system.md`
2. `memory-scoping.md`

### 4.5 更新、删除或下沉旧经验

优先读取：
1. `memory-update-and-pruning.md`
2. `memory-scoping.md`

### 4.6 准备使用 subagent

优先读取：
1. `subagent-strategy.md`

### 4.7 准备创建局部 AGENTS

优先读取：
1. `local-agents-template.md`
2. `memory-scoping.md`

---

## 5. 维护原则

1. 本目录中的文件应保持主题单一，避免互相重复。
2. 某条规则如果已经足够局部，应写入对应目录下的局部 `AGENTS.md`，而不是回写到本目录。
3. 如果某份文档开始频繁出现具体页面名、组件名、路由名、链路名，通常说明内容已经过于局部，应考虑下沉。
4. 若不同文档之间出现内容冲突，应优先：
   - 保持根级 `AGENTS.md` 为最小规则入口
   - 把主题解释集中到最匹配的单一文档中
   - 删除其他文件中的重复或冲突表述