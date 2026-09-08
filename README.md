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
│   └── concept-relationship.html
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

## 人工核查与修改说明

以下内容是在 AI 生成结果的基础上**人工阅读、核查并修改**过的：

1. **参考来源逐条核对**：三个概念页的参考来源均为真实可查的资料（Anthropic 官方工程博客/文档、arXiv 论文编号、Lilian Weng 博客、WorkBuddy 官方文档）；AI 初稿中无法确认 URL 的条目已改为"来源名称 + 搜索关键词"的形式，未保留任何可疑链接。
2. **结构补齐**：AI 初稿缺少作业要求的"学习目标、核心问题、使用边界、自测问题、参考来源"，已按 SKILL.md 的自检清单逐页补充。
3. **概念表述修正**：核对参考来源后，将"上下文窗口不是无限数据库""技能不是执行保证"等边界表述明确化，避免夸大 Agent/Skill 的能力。
4. **新增关系文档**：`concept-relationship.md` 为人工撰写框架后由 AI 协助绘图的版本，Mermaid 图中的流向经过人工确认（Skill → 上下文 → Agent → 产出 → 回流 Skill）。

## 建议阅读顺序

agent.html → llm-context.html → skill.html → concept-relationship.md / .html
（先懂个体，再看关系）
