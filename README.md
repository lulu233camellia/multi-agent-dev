# Multi-Agent Dev · 多 Agent 协作开发

让规划、开发和独立验收各负其责，同时减少没有新证据的重复审核。

这是一个以中文编写的 Agent Skill，适用于软件开发协作。它提供风险分流、任务交接和审核停止条件；普通小改动可以由一个 Agent 完成。

## 解决什么问题

- 每个小修改都经过规划、开发、验收多次传递。
- 修复一个问题后，重新审核整个仓库，又发现一批无关改进。
- 已解决的问题换个说法被再次提出。
- 不同 Agent 重复运行输入未变、已经通过的同一组测试。
- 切换代理或恢复聊天后丢失审核记录，循环从头开始。

## 工作方式

| 场景 | 执行方式 |
| --- | --- |
| 小范围文案、样式和普通缺陷 | 单 Agent 最小修改与相关检查 |
| 跨模块功能或需要独立验收的任务 | 协调者锁定范围，开发者实现，独立验收者检查 |
| 有具体重大风险的变更 | 增加必要专项检查，并保留项目要求的人工门槛 |

角色按任务需要启用，不要求每次建立固定人数的团队。

### 审核如何结束

首轮查看本次完整变更。修复后的复核默认围绕未解决问题、修复差异与受影响行为；扩大范围需要具体理由。有效测试证据可以复用，项目必需的独立检查与 CI 仍须完成。

问题使用稳定 ID 跟踪。已有结论需要新证据才重新打开，范围外建议不会自动变成本轮任务。默认审核上限为三轮，满足条件可提前结束；到限仍有阻断问题时，报告当前状态和下一步。用户明确要求额外复核，可以追加对应预算，历史轮数继续累计。

这些规则受当前用户指令和项目约定约束。Skill 是行为指导，不是能在运行时强制拦截调用的限流器。

## 安装

使用 Skills CLI：

```bash
npx skills add lulu233camellia/multi-agent-dev --skill multi-agent-dev -g -a codex
```

也可以将完整仓库克隆到自己的 Skill 目录。以下示例仅适用于目标目录尚不存在时：

```bash
git clone https://github.com/lulu233camellia/multi-agent-dev.git ~/.codex/skills/multi-agent-dev
```

其他 Agent Skills 兼容工具可以使用其自己的 Skill 目录。实际代理分工能力取决于宿主提供的工具；没有独立代理能力时，不能声称已完成独立验收。安装后若未被发现，重新打开会话或重载宿主。

## 使用示例

```text
使用 $multi-agent-dev 完成这个跨模块功能，先锁定验收条件，再安排开发和独立验收。
```

```text
使用 $multi-agent-dev 检查现有开发协作流程，减少没有新证据的复审。
```

```text
按 $multi-agent-dev 处理这个小范围 UI 修改，采用适合它的最小流程。
```

已有长期团队时复用当前登记和任务文件。创建新的长期聊天须由用户明确要求；单次任务分工使用宿主可用的子代理能力。普通问答、寻找 Skill 和内容创作团队不属于本 Skill 的范围。

## 文件

```text
multi-agent-dev/
├── SKILL.md                       # 入口、职责与审核规则
├── agents/openai.yaml             # Codex 界面元数据
├── references/collaboration.md    # 团队与任务交接
├── references/review-state.md     # 问题及证据状态模板
├── references/sources.md          # 设计来源与适配边界
├── README.md
└── LICENSE
```

## 验证与限制

当前版本通过了 Skill 结构、相对引用和元数据检查，并完成六个合成流程场景的一轮独立推演，覆盖小改动、重复问题、预算追加、过期证据、重叠写入和真实验收缺口。推演发现的一处预算授权歧义已修正。

这些是结构与流程验证，不是实际项目的速度或缺陷率基准。仓库不声称已经证明节省时间；应结合真实任务的审核轮数、等待时间和遗漏缺陷评估效果。

## 来源

基于作者的项目协作实践，并参考 [How the Claude Code team does code review](https://claude.dev/blog/solving-code-review-at-anthropic/) 的审核收敛思路。具体适配见 [sources.md](references/sources.md)。这是独立社区项目，与 Anthropic、OpenAI 没有官方关联。

## License

[MIT](LICENSE)
