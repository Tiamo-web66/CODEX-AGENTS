# CODEX-AGENTS

用于维护 Codex/Agent 相关的工作约定、提示词、技能说明、插件配置和项目协作资料。

## 仓库用途

- 记录通用 Agent 工作流和工程规范。
- 存放可复用的提示词、技能说明、配置片段和脚本。
- 管理项目初始化模板、代码审查清单和常用排障文档。

## 推荐结构

```text
.
├── AGENTS.md          # Codex 在本仓库工作时优先读取的协作规则
├── README.md          # 仓库说明
├── docs/              # 设计、流程、规范、排障文档
├── prompts/           # 可复用提示词
├── rules/             # 可合并到 AGENTS.md 的规则集
├── scripts/           # 辅助脚本
└── templates/         # 项目或文档模板
```

后续按真实内容逐步创建目录，避免空目录和无用模板膨胀。

## 使用建议

1. 将稳定规则写入 `AGENTS.md`。
2. 将一次性讨论或较长说明放入 `docs/`。
3. 将可复制复用的提示词放入 `prompts/`。
4. 将可组合的 Codex 规则放入 `rules/`。
5. 将可执行自动化逻辑放入 `scripts/`，并在脚本头部写明用途和运行方式。

## 已收录规则

- `rules/karpathy-codex.zh.md`：Karpathy 风格 Codex 规则中文版本。
- `rules/karpathy-codex.en.md`：Karpathy-style Codex rules in English.

## 初始化状态

当前仓库已完成基础初始化：

- Git 远端：`git@github.com:Tiamo-web66/CODEX-AGENTS.git`
- 默认分支：`main`
- 基础文件：`README.md`、`AGENTS.md`、`.gitignore`、`.editorconfig`
