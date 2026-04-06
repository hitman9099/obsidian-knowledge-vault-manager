# Obsidian Knowledge Vault Manager

一个面向 Codex 的 skill，用于按固定中文规则维护可追溯、按文件夹分类的 Obsidian 知识库。

这个 skill 适合以下场景：

- 在新电脑上恢复既有 Obsidian 知识库规则
- 接收文字、URL、截图、图片、PDF 或其他文件并先写入 `00_Inbox`
- 把内容沉淀到 `10_Knowledge`、`20_Projects` 或 `05_网页资料`
- 更新索引与别名映射
- 回答知识库检索问题并返回具体笔记路径

## 核心特点

- 全程中文优先
- 先收件留痕，再沉淀知识
- 知识层必须按文件夹分类，不允许长期平铺
- 支持链接、截图、PDF 和其他文件入库
- 自带恢复规则、分类规则和验证流程

## 目录结构

```text
obsidian-knowledge-vault-manager/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    ├── vault-rules.md
    ├── current-taxonomy.md
    ├── validation-scenarios.md
    └── last-validation-report.md
```

## 安装方式

把整个目录复制到：

```text
$CODEX_HOME/skills/obsidian-knowledge-vault-manager
```

如果没有设置 `CODEX_HOME`，通常放到：

```text
~/.codex/skills/obsidian-knowledge-vault-manager
```

## 使用方式

当任务涉及以下内容时，使用这个 skill：

- 恢复一套已有的 Obsidian 知识库规则
- 维护按中文规则组织的知识库
- 处理知识收件、沉淀、索引和检索

推荐先读取：

1. `AGENTS.md`
2. `30_Indexes/知识库规则总览.md`
3. `README.md`
4. `30_Indexes/总导航.md`
5. `30_Indexes/高频主题索引.md`
6. `30_Indexes/别名与关键词映射.md`

如果只允许读取两份文件，最少读取前两份。

## 参考文件

- `references/vault-rules.md`
  记录知识库固定规则
- `references/current-taxonomy.md`
  记录当前分类体系与命名规则
- `references/validation-scenarios.md`
  记录 skill 的验证场景
- `references/last-validation-report.md`
  记录最近一次验证结果

## 验证

这个 skill 内置了验证流程，包含：

- 结构校验
- 恢复场景验证
- 链接收件验证
- 文件收件验证

最近一次验证结果见：

- `references/last-validation-report.md`

如需手动校验结构，可运行：

```bash
python /path/to/quick_validate.py /path/to/obsidian-knowledge-vault-manager
```

## 适用的知识库约束

- 所有输出默认使用中文
- 新内容先写 `00_Inbox`
- 再沉淀到 `10_Knowledge`、`20_Projects` 或网页资料目录
- 新增重要知识时更新：
  - `30_Indexes/高频主题索引.md`
  - `30_Indexes/别名与关键词映射.md`

## License

MIT
