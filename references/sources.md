# 来源与适配边界

整理日期：2026-11-02。

本 Skill 面向从需求到交付与迭代的全流程应用开发，范围依据作者的实际使用需求明确。下述项目实践提供协作基础，文章主要为其中的审核环节提供收敛方法。

## 原有项目实践

本 Skill 从作者已有的软件项目协作方式抽取通用规则：职责分离、当前 Agent 登记、结构化交接、快速变更与正式版本分流、有效测试证据复用、先交付首要结果。

原始项目材料未随本仓库发布，也不是运行依赖。公开版本不包含本地绝对路径、项目聊天 ID、供应商限制或内部发布配置；没有把必须五个 Agent 等项目专属约定推广为通用要求。应用到已有项目时仍需读取该项目当前约定。

## 需求与方案增强分支

`codex/discovery-planning` 的三份方法参考采用独立编写的中文说明，把下列项目中适用的设计思路转成当前协作流程的决策规则。链接固定到调研时核实的版本；没有捆绑上游实现、复制完整 Skill 或要求安装其运行环境。

| 来源与核实版本 | 参考的方法 | 本分支的适配 |
| --- | --- | --- |
| [phuryn / interview-script](https://github.com/phuryn/pm-skills/blob/2a12295a7717569baa7be181b4cfebe3ca38a6bb/pm-product-discovery/skills/interview-script/SKILL.md)、[identify-assumptions-new](https://github.com/phuryn/pm-skills/blob/2a12295a7717569baa7be181b4cfebe3ca38a6bb/pm-product-discovery/skills/identify-assumptions-new/SKILL.md)、[prioritize-assumptions](https://github.com/phuryn/pm-skills/blob/2a12295a7717569baa7be181b4cfebe3ca38a6bb/pm-product-discovery/skills/prioritize-assumptions/SKILL.md) | 从真实行为了解问题，识别假设，优先处理影响大的未知 | 只对影响当前决定的缺口提问；访谈计划和模拟结果不算已验证的需求 |
| [phuryn / create-prd](https://github.com/phuryn/pm-skills/blob/2a12295a7717569baa7be181b4cfebe3ca38a6bb/pm-execution/skills/create-prd/SKILL.md) | 默认简短的产品需求文档、明确非目标和未知 | 沿用项目已有文档，聚焦流程、范围和可观察验收，不要求填满固定模板 |
| [obra / brainstorming](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/brainstorming/SKILL.md)、[writing-plans](https://github.com/obra/superpowers/blob/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/writing-plans/SKILL.md) | 先读上下文再问、区分用户决定与提案、明确实现接口和验证 | 按需澄清与交接，不增加独立的设计和计划批准流程 |
| [alirezarezvani / senior-architect](https://github.com/alirezarezvani/claude-skills/blob/e4a1dc3695908dd5a6c811cc76ab7aa4cf95f2f0/engineering-team/skills/senior-architect/SKILL.md) | 围绕约束比较技术选项，记录取舍，覆盖数据与接口 | 使用实际项目证据，不移植以人数或数据量直接决定选型的经验阈值，也不运行其分析脚本 |
| [BMAD / bmad-architecture](https://github.com/bmad-code-org/BMAD-METHOD/blob/bd70c643a7ec85d1ec2e88076b3fbdd8e4517f41/skills/bmad-architecture/SKILL.md) | 预先固定会影响独立实现一致性的共同约定 | 聚焦模块边界、状态修改、共享数据和接口；不引入 `_bmad` 运行环境及审核编排。所读版本属于 v7 预览分支 |
| [garrytan / office-hours](https://github.com/garrytan/gstack/blob/f865cd9fc7c89f6ac64e6dcbe219a07a0ba026ad/office-hours/SKILL.md) | 质询问题前提、检查现有替代办法、比较较小的可行方案 | 仅在方向存在实质未知时采用，不默认叠加专项质询、遥测或额外审核 |

这些来源在本次核实时的仓库根许可证为 MIT。其工具命令、外部服务行为和完整流程并非本 Skill 的依赖；这里的链接用于方法溯源，不代表已安装、执行或获得任何项目的背书。其他调研候选未纳入本分支。

本分支的结构检查不证明需求发现质量或交付提速，仍需真实任务检验。

## 文章

[How the Claude Code team does code review](https://claude.dev/blog/solving-code-review-at-anthropic/)，Addy Osmani、Morgan Westlee Lunt、Qing Wang，2026-10-15 发布；2026-11-02 核对。

采用其中的收敛方向：限制审核轮次、后续缩小复审范围、集中处理同类缺陷、避免重复发现，并让审核投入随风险变化。原文描述的是团队流程，不是一个可直接安装的 Codex Skill。

本 Skill 的适配选择：

- 将“前几轮后缩小范围”具体化为首轮完整审核，之后默认按修复增量和影响面复核；需要扩大时写明理由。
- 用一个共享问题状态和工作项计数支持跨 Agent 交接；没有提供运行时自动拦截器。
- 保留用户项目的小改动单 Agent 路径，不复制大型团队的全部审核层或人工审批人数。

这些是流程设计，尚不构成耗时节省或缺陷率改善的实测结论。需要在真实任务中比较审核轮数、等待时间和遗漏缺陷。
