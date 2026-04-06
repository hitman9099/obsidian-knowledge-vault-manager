---
name: obsidian-knowledge-vault-manager
description: 维护一套中文优先、可追溯、按文件夹分类的 Obsidian 知识库。用于以下场景：在新电脑上恢复这套知识库规则；接收文字、URL、截图、图片、PDF 或其他文件并先写入 `00_Inbox`；把内容沉淀到 `10_Knowledge`、`20_Projects` 或 `05_网页资料`；更新索引与别名映射；回答知识库检索问题并返回具体笔记路径。只要任务涉及按固定中文规则维护 Obsidian 知识库，就应使用此 skill。
---

# Obsidian Knowledge Vault Manager

## 概览

按固定中文规则维护 Obsidian 知识库。先恢复规则，再收件留痕，再沉淀知识，最后保持索引和检索一致。

## 快速入口

如果目标库根目录中存在这些文件，按这个顺序读取：

1. `AGENTS.md`
2. `30_Indexes/知识库规则总览.md`
3. `README.md`
4. `30_Indexes/总导航.md`
5. `30_Indexes/高频主题索引.md`
6. `30_Indexes/别名与关键词映射.md`

如果只允许读取两份文件，最少读取前两份。

固定规则摘要见：
- [vault-rules.md](references/vault-rules.md)
- [current-taxonomy.md](references/current-taxonomy.md)

## 工作流

### 1. 恢复环境

- 先确认根目录是否存在 `00_Inbox`、`10_Knowledge`、`20_Projects`、`30_Indexes`、`90_Attachments`、`99_Templates`。
- 若缺失目录，按 [current-taxonomy.md](references/current-taxonomy.md) 补齐。
- 不改动已有中文分类名，不把知识层改回平铺。

### 2. 接收新内容

- 用户提交的内容可以是文字、URL、图片、截图、PDF、其他文件，或多种内容混合。
- 所有新内容先写入当天的 `00_Inbox/YYYY-MM-DD 收件.md`。
- 若当天收件文件不存在，则先创建。
- 原始记录必须保留，除非用户明确要求删除。

### 3. 判断落点

- 长期可复用知识：写入 `10_Knowledge`
- 项目状态、目标、决策、待办：写入 `20_Projects`
- 网页正文未稳定解析：写入 `10_Knowledge/05_网页资料/01_待补充解析`
- 截图、长图、聊天图片资料：优先写入 `10_Knowledge/05_网页资料/02_截图资料`
- 仅需留痕的内容：保留在 `00_Inbox`

### 4. 维护正式笔记

- 优先更新已有主题笔记，不重复创建近义文件。
- 正式笔记使用 YAML frontmatter，至少包含：
  - `id`
  - `title`
  - `type`
  - `status`
  - `created`
  - `updated`
  - `tags`
  - `aliases`
  - `summary`
- 按需补充：
  - `topic`
  - `project`
  - `people`
  - `source_refs`
  - `related`

### 5. 维护索引

- 新增重要知识后，至少检查：
  - `30_Indexes/高频主题索引.md`
  - `30_Indexes/别名与关键词映射.md`
- 如果新增了新的中文分类目录，同时更新：
  - `AGENTS.md`
  - `30_Indexes/知识库规则总览.md`
  - `README.md`
  - `30_Indexes/总导航.md`

### 6. 回答检索问题

- 默认先直接回答。
- 再给出具体笔记路径。
- 必要时补充原始来源路径。
- 所有回答默认使用中文。

## 分类与命名

- 分类、标题、摘要、索引说明默认使用中文。
- 外部原始标题或术语可保留原文，但整理后的说明必须写中文。
- 收件文件命名：`YYYY-MM-DD 收件.md`
- 知识笔记命名：中文主题名，必要时保留英文专有名词
- 项目笔记命名：中文项目名
- 附件目录：`90_Attachments/年-月/`

当前固定分类见 [current-taxonomy.md](references/current-taxonomy.md)。

## 文件处理

- URL：记录原始 URL、平台、链接说明、提取结果。
- 图片或截图：尽量提取核心内容；有必要时复制到附件目录。
- PDF 或其他文件：保留原文件到附件目录，并提取正文或关键信息后沉淀成知识笔记。
- 无法完整解析的资料不得丢弃，至少保留来源、路径和当前判断。

## 输出约束

- 所有问答都用中文。
- 返回路径时优先给出可定位的具体笔记路径。
- 不擅自引入英文分类体系。
- 不删除旧收件或旧知识，除非用户明确要求。

## 验证流程

每次新建或修改这个 skill 后，都执行一次最小验证。验证顺序如下：

1. 结构校验
   - 运行 `quick_validate.py` 检查 skill 结构是否合法。
2. 恢复场景验证
   - 模拟“换电脑后接管知识库”。
   - 检查是否能从 `AGENTS.md` 和 `30_Indexes/知识库规则总览.md` 恢复目录、分类和默认流程。
3. 链接收件验证
   - 模拟用户只提交 URL。
   - 验证行为应包含：
     - 写入当天 `00_Inbox`
     - 沉淀到正确知识目录
     - 更新 `高频主题索引`
     - 更新 `别名与关键词映射`
4. 文件收件验证
   - 模拟用户提交 PDF、图片或其他本地文件。
   - 验证行为应包含：
     - 写入当天 `00_Inbox`
     - 附件复制到 `90_Attachments/年-月/`
     - 生成或更新正式知识笔记
     - 补充相关索引
5. 记录验证结果
   - 参考 [validation-scenarios.md](references/validation-scenarios.md)。
   - 把最近一次验证结论写入 [last-validation-report.md](references/last-validation-report.md)。

如果任一场景失败，先修 skill，再重新跑完整验证，不跳过失败项。
