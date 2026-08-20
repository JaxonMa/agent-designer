# Agent Designer — AI 智能体设计指南

[English](README.md)

Agent Designer 是一个面向 AI 智能体的风格指南仓库。智能体在开始设计之前阅读这些指南，每份指南描述一种风格统一的视觉样式，并附带精确的描述和 CSS token，使智能体可以在任何项目中实现美观的外观。

## 使用方法

Agent Designer 供 AI 智能体（例如 opencode）在你的项目中开始设计 UI 之前阅读。常见的使用方式有两种：

### 单次使用某种风格

在智能体会话中，把指南的位置告诉智能体并指定风格，例如：

> "使用 agent-designer 中的 Graphite 风格（styles/graphite.md）来设计我的仪表盘。"

随后智能体会：

1. 提供可用的风格选项（参见可用风格）。
2. 询问详细需求，以达到预期的效果。
3. 遵循所选指南中的 token 和规则，并结合你项目的约束条件。
4. 在交付前，依据指南末尾的一致性检查清单（conformance checklist）验证结果。

### 让某项目默认应用某种风格

如果希望在项目的每次 UI 任务中都应用某种风格：

1. 使用你的智能体生成项目的规则文件——在 opencode 中运行 `/init` 即可创建 `AGENTS.md`。
2. 添加一行指向指南，例如：

   `Before building any UI, read <path-to-agent-designer>/styles/graphite.md and apply its tokens and rules.`

3. 之后智能体会在每次 UI 任务中默认应用该风格，并自动进行一致性检查。

## 工作流程

- 当用户希望智能体选择一种风格时，智能体提供多个风格指南选项，让用户自行选择。
- 选定风格后，智能体询问详细需求，以达到预期的效果。
- 智能体遵循所选风格指南中的限制和要求，并结合当前项目，决定使用何种风格和组件。

## 可用风格

| 风格 | 文件 | 描述 |
| --- | --- | --- |
| Graphite | `styles/graphite.md` | 一款通用单色设计系统：灰度色板、锐利边角、1px 细线边框、反转悬停状态、大写微标签、配套的浅色/深色主题。 |
