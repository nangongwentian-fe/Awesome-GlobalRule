# Awesome Global Rule

一套面向 Coding Agent 的全局规则模板与经验系统骨架，目标不是塞更多“提示词”，而是让 Agent 在真实项目里更像一个长期维护者：

- 先看已有实现，再改代码
- 按作用域读取规则，而不是一次性加载全部文档
- 主动复用历史经验，也主动修订和清理过期经验
- 在 code review、方案判断、目录组织、局部沉淀上保持稳定输出

当前仓库同时兼容两类常见命名：

- `AGENTS.md`：适用于 Codex 等工具
- `CLAUDE.md`：适用于 Claude Code 等工具

两者职责等价，核心思想一致。

## 这个仓库解决什么问题

很多 Agent 规则仓库最后都会失控：

- 根文件越写越长，什么都往里塞
- 局部经验没有作用域，页面级细节被写进全局规则
- 旧经验只增不减，最终和真实代码脱节
- Agent 只会背规则，不会先对齐现有实现

这个仓库的设计目标是反过来处理这些问题：

1. 根级文件只保留长期稳定的最小必要规则。
2. 细节规则拆到 `docs/agent-rules/`，按任务类型选择性读取。
3. 更具体的经验优先写入更近目录下的局部 `AGENTS.md`。
4. 经验系统允许新增、合并、修订、删除和下沉，而不是只追加。

## 核心能力

### 1. 渐进式披露

根级 `AGENTS.md` 只负责：

- 仓库级约束
- 规则路由
- 经验沉淀机制
- 详细文档索引

详细规则按需读取，不要求 Agent 每次任务都把所有文档一次性读完。

### 2. 作用域优先的经验系统

经验写入前先判断作用域：

- 局部
- 模块
- 项目
- 全局

默认遵循“写低不写高”，避免把只对单个页面或目录生效的经验错误提升到根级规则。

### 3. 现有实现优先

这套规则不鼓励 Agent 凭空发明“最佳实践”，而是要求：

- 先读现有代码、配置、测试和文档
- 优先模仿当前目录内已经验证过的模式
- 默认做最小且正确的改动

### 4. 可落地的 Review 标准

除了语法和格式，本仓库会把 review 的关注点放在：

- 逻辑设计
- 组件封装
- 状态层级
- 代码组织
- 可维护性与后续演进成本

### 5. 可维护的经验生命周期

经验不是历史垃圾堆。仓库明确要求在以下场景修订旧经验：

- 当前代码与旧经验冲突
- 目录结构、接口、配置或实现已变化
- 原本的高层级经验现在只在局部仍成立

## 仓库结构

```text
.
├── AGENTS.md
├── README.md
├── docs/
│   └── agent-rules/
│       ├── README.md
│       ├── coding-style.md
│       ├── code-organization.md
│       ├── imports-and-paths.md
│       ├── component-design.md
│       ├── code-review.md
│       ├── memory-system.md
│       ├── memory-scoping.md
│       ├── memory-update-and-pruning.md
│       ├── subagent-strategy.md
│       └── local-agents-template.md
└── log/
```

## 文档索引

| 文件 | 作用 |
| --- | --- |
| `AGENTS.md` | 项目根级规则入口，定义总体原则、优先级、经验沉淀机制和详细文档索引 |
| `docs/agent-rules/README.md` | 详细规则目录说明，告诉 Agent 该在什么任务下读取哪些文档 |
| `docs/agent-rules/coding-style.md` | 通用编码偏好、改动边界、复用与命名原则 |
| `docs/agent-rules/code-organization.md` | 文件拆分、常量/类型放置、hooks/utils/services 组织方式 |
| `docs/agent-rules/imports-and-paths.md` | alias 与相对路径选择、导入分组与路径改动边界 |
| `docs/agent-rules/component-design.md` | 组件职责划分、状态管理、抽 hook / utils / services 的边界 |
| `docs/agent-rules/code-review.md` | review 关注点、问题表达方式和建议输出结构 |
| `docs/agent-rules/memory-system.md` | 什么值得沉淀为经验、何时主动复用和新增经验 |
| `docs/agent-rules/memory-scoping.md` | 经验按局部/模块/项目/全局进行路由的规则 |
| `docs/agent-rules/memory-update-and-pruning.md` | 旧经验的修订、删除、重写和下沉策略 |
| `docs/agent-rules/subagent-strategy.md` | subagent 的拆分边界、适用场景和主代理职责 |
| `docs/agent-rules/local-agents-template.md` | 在业务目录下创建局部 `AGENTS.md` 的推荐模板 |

## 如何使用

### 方式一：作为项目级规则模板

适合你想让某个仓库直接拥有这套规则体系。

1. 把根级 `AGENTS.md` 放到目标仓库根目录。
2. 把 `docs/agent-rules/` 一并拷贝过去。
3. 在具体业务目录出现稳定经验后，再新增更近的局部 `AGENTS.md`。
4. 后续迭代时，优先修改局部经验或详细文档，不要持续膨胀根文件。

### 方式二：作为个人全局规则参考仓库

适合你想把这套方法用于多个项目。

1. 将根级规则合并到你使用的 Agent 工具全局说明中。
2. 保留本仓库作为“详细规则索引库”。
3. 需要时把相关文档或局部模板迁移到具体项目，而不是把所有细节直接塞进全局提示词。

### 方式三：作为现有规则仓库的重构参考

如果你的 `AGENTS.md` / `CLAUDE.md` 已经很长，这个仓库可以作为重构模板：

1. 先把根文件中稳定的仓库级规则保留。
2. 把主题化说明拆到 `docs/agent-rules/`。
3. 把页面级、目录级、链路级经验下沉到局部 `AGENTS.md`。
4. 为经验补上“更新 / 删除 / 下沉”的维护机制。

## 推荐工作流

### 新任务开始时

1. 先查看当前目录及其上层是否已有局部 `AGENTS.md`。
2. 根据任务类型，按需读取 `docs/agent-rules/` 中对应文档。
3. 先对齐现有代码、配置、测试和文档，再决定改法。

### 任务完成后

1. 判断这次结论是否值得沉淀。
2. 若值得沉淀，先判断作用域，再决定写入位置。
3. 如果旧经验已过期，优先修订或删除旧条目，而不是继续叠加。

## 适用对象

这套规则更适合以下场景：

- 你长期使用 Claude Code、Codex、Cursor、Aider 等 Coding Agent
- 你希望 Agent 更像“熟悉项目的同事”，而不是“会背提示词的生成器”
- 你需要稳定的代码评审、经验沉淀和局部规则治理能力
- 你已经感受到根级规则文件持续膨胀带来的维护成本

## 不适合把它当成什么

它不是：

- 一份包治百病的超长万能 Prompt
- 一套要求 Agent 每次都全文背诵的规则大杂烩
- 一份只会新增、不允许修订删除的“历史档案馆”

它更接近一套可维护的规则分层方案。

## 建议的落地原则

1. 先最小接入，不要一开始就为每个目录建局部规则。
2. 先让 Agent 养成“先看现有实现”的习惯，再补更多规范。
3. 经验沉淀要少而准，能复用才值得写。
4. 根级文件保持稳定，局部经验保持贴近真实代码。

## 参考阅读顺序

- 想统一编码习惯：先看 `coding-style.md`
- 想规范文件拆分：看 `code-organization.md`
- 想管控组件边界：看 `component-design.md`
- 想提高 review 质量：看 `code-review.md`
- 想建设经验系统：看 `memory-system.md` 与 `memory-scoping.md`
- 想治理旧规则：看 `memory-update-and-pruning.md`
- 想在局部目录新增规则文件：看 `local-agents-template.md`

## License

当前仓库未声明 License。如需对外分发或商用，建议先补充明确的许可证文件。
