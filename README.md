# hippo-repo · 个人概念学习资料仓库 🦛

**作业 1：用 AI 构建个人概念学习资料生成 Skill**

本仓库包含两部分：

1. **`.workbuddy/skills/concept-learning-materials/`** —— 一个"概念学习资料生成" Skill。
   它定义了一套工作流程：当需要学习某个概念时，自动生成 4 个互相链接的 HTML 学习页面
   （概念详解、上下文、应用、概念关系图），统一格式、自包含、可离线阅读。

2. **`learning-materials/`** —— 由该 Skill 生成的第一批学习资料，主题为本次作业涉及的
   三个核心概念及其关系：
   - [agent.html](learning-materials/agent.html) —— Agent（智能体）：大脑 + 工具 + 记忆 + 规划
   - [llm-context.html](learning-materials/llm-context.html) —— LLM 上下文：模型的"工作桌面"
   - [skill.html](learning-materials/skill.html) —— Skill：写给 AI 的 SOP 手册
   - [concept-relationship.html](learning-materials/concept-relationship.html) —— 三者的关系图

## 目录结构

```
hippo-repo/
├── .workbuddy/
│   └── skills/
│       └── concept-learning-materials/
│           └── SKILL.md          # Skill 定义（触发条件/流程/输出规范）
├── learning-materials/           # Skill 生成的学习资料
│   ├── agent.html
│   ├── llm-context.html
│   ├── skill.html
│   ├── concept-relationship.html
│   └── concept-relationship.md
├── README.md
└── .gitignore
```

## 使用方法（在 WorkBuddy 中调用）

1. 本仓库的 `.workbuddy/skills/` 目录就是 WorkBuddy 的**项目级技能目录**：在 WorkBuddy 中打开本仓库作为工作区，技能即被识别。
2. 对 AI 助手说：**"帮我搞懂 <概念名>"**（如"帮我搞懂注意力机制"）。
3. 助手匹配到 `concept-learning-materials` 技能后，会按 SKILL.md 定义的流程，在 `learning-materials/` 下生成该概念的 4 页学习资料（概念详解、上下文、应用、关系图），并附学习目标、核心问题、自测问题与参考来源。
4. 所有页面为自包含 HTML，双击即可离线打开。

## 已生成的学习资料

| 文件 | 主题 |
|---|---|
| `learning-materials/agent.html` | Agent（智能体） |
| `learning-materials/llm-context.html` | 大模型的上下文 |
| `learning-materials/skill.html` | Skill |
| `learning-materials/concept-relationship.html` | 三者关系（图形版） |
| `learning-materials/concept-relationship.md` | 三者关系（Mermaid 文字版） |

## 人工核查与 AI 使用说明

**AI 参与的部分**：Skill 框架设计、学习资料初稿、Mermaid 图绘制、Git 命令辅助诊断。
**人工完成的部分**：全部内容的阅读理解、参考来源逐条核查、结构与表述修改、最终提交判断。

以下是在 AI 生成结果的基础上**人工阅读、核查并修改**过的内容：

1. **参考来源逐条核对**：三个概念页的参考来源均为真实可查的资料（Anthropic 官方工程博客/文档、arXiv 论文编号、Lilian Weng 博客、WorkBuddy 官方文档）；AI 初稿中无法确认 URL 的条目已改为"来源名称 + 搜索关键词"的形式，未保留任何可疑链接。
2. **结构补齐**：AI 初稿缺少作业要求的"学习目标、核心问题、使用边界、自测问题、参考来源"，已按 SKILL.md 的自检清单逐页补充。
3. **概念表述修正**：核对参考来源后，将"上下文窗口不是无限数据库""技能不是执行保证"等边界表述明确化，避免夸大 Agent/Skill 的能力。
4. **新增关系文档**：`concept-relationship.md` 为人工撰写框架后由 AI 协助绘图的版本，Mermaid 图中的流向经过人工确认（Skill → 上下文 → Agent → 产出 → 回流 Skill）。
5. **参考来源链接逐一实测**（2025-10）：用 HTTP 状态码与网页抓取实际访问了全部来源——Anthropic 工程博客两篇、WorkBuddy 文档均返回 200；两篇 arXiv 论文核对到准确标题/作者/日期（ReAct: 2210.03629；Lost in the Middle: 2307.03172）。发现 `docs.claude.com` 文档域名迁移且存在地区访问限制，已将其替换为 Anthropic 开源技能仓库（github.com/anthropics/skills）等可核查来源，并在页面中注明替换原因。
6. **个人理解部分为本人观点**：`concept-relationship.md` 中"我的个人理解与判断"一节，基于本次作业的亲身经历（来源核查、技能编写）总结而成，非 AI 生成后照搬。

## 敏感信息处理

- 创建仓库时使用的 GitHub Token 只保存在本地 Git 配置中（`.git/config`，该目录不会被提交推送）；仓库全部文件中不包含任何 API Key、密码或个人隐私信息。
- `.gitignore` 中已添加密钥/证书/凭据类文件（`*.key`、`*.pem`、`.env*`、`*token*` 等）的排除规则，防止后续误提交。

## 遇到的问题与解决记录

完成过程中遇到的主要报错，以及最终的解决方式：

| # | 问题 | 诊断与解决 |
|---|---|---|
| 1 | 创建仓库时填写中文名「河马的小仓库」，GitHub 自动将其转换为 `-`，仓库名失效 | 查阅 GitHub 文档确认仓库名仅支持字母/数字/连字符，通过 GitHub API（PATCH /repos）重命名为 `hippo-repo` |
| 2 | `git push` 报 `CONNECT tunnel failed, response 502` / `SSL handshake failed` | 用 `curl` 分别测试 `github.com` 与 `api.github.com`，定位到本地代理仅放行 API 域名；改用 GitHub Contents API 逐个上传文件作为备用通道，之后网络恢复再改回正常 git 工作流 |
| 3 | 恢复后执行 `git pull --rebase` 中断，`.git` 目录意外丢失（工作区文件完好） | 工作区文件未受损；重新 `git init` → `git fetch` → `git reset FETCH_HEAD`（混合重置，保留工作区）→ 重新提交，历史与远程重新对齐，最终推送成功（`1c01f50`） |
| 4 | 远程仓库根目录出现网页端误建的空文件 `Skill` | 确认其为空文件后在下一次提交中删除，保持目录结构清晰 |

## 后续计划

本仓库是后续课程项目的长期载体，将在现有基础上继续扩展：

- 学习新概念时，通过 Skill 生成新的学习资料追加到 `learning-materials/`；
- 沉淀新的个人 Skill 到 `.workbuddy/skills/`（如课程笔记、代码复盘等）；
- 每次新增内容保持"生成 → 人工核查 → 提交"的流程，仓库历史即学习轨迹。

## 建议阅读顺序

agent.html → llm-context.html → skill.html → concept-relationship.md / .html
（先懂个体，再看关系）
