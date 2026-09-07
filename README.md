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

## 使用方法

将 Skill 安装到 WorkBuddy 后（放入 `.workbuddy/skills/` 即可），对 AI 助手说：

> "帮我搞懂 <概念名>"

助手会按 SKILL.md 中定义的流程，在 `learning-materials/` 下生成该概念的 4 页学习资料。
页面均为自包含 HTML，双击即可离线打开。

## 建议阅读顺序

agent.html → llm-context.html → skill.html → concept-relationship.html
（先懂个体，再看关系）
