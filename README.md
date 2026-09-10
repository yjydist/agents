# 通用 Agent 工程模板, 技能与专用角色

本仓库以敏捷开发为主线, 通过小步交付, 验证与真实反馈逼近需求, 在持续重构中保持低成本变更能力. [工程原则模板](template/agent.md), [技能](skills) 与 [专用 subagent 提示词](agents) 均服务于这条主线, 可按需独立复制使用.

- 模板提供常驻的核心工程判断与委派原则.
- 技能提供按任务加载的具体方法, 主 agent 和 subagent 均可使用.
- 专用角色定义适用任务, 工作边界, 必要方法和返回结果, 供主 agent 委派独立子问题.

模板存放在 `template/agent.md`, 避免被当作本仓库的 Agent 指令加载. 根目录的 [AGENTS.md](AGENTS.md) 为维护本仓库的 agent 提供约定.

## 使用

- 工程原则: 将 `template/agent.md` 的内容复制到目标仓库的 `AGENTS.md`, 可独立使用, 不要求安装技能或专用角色. 目标文件已有指令时合并适用内容, 不覆盖项目约束.
- 技能: 按需将 `skills/` 下的单个技能目录复制到目标工具支持的技能位置, 保留目录名和 `SKILL.md`. 每个技能可独立使用, 不要求同时复制工程原则模板, 其他技能或专用角色.
- 专用角色: 按需复制 `agents/` 下的单个 Markdown 文件, 将正文作为目标工具的 subagent 提示词. 每个文件包含独立工作所需的最小方法, 不要求配套技能或模板. 按任务选用技能时仍遵守角色的工作边界, 不因技能包含实施步骤而扩大委派权限.

`agents/*.md` 是提示词来源, 不是各工具通用的原生配置. 实际注册, 发现, 工具权限和上下文传递方式由目标工具负责, 不能假定仅复制目录就会自动启用 subagent. 文中的工作边界是提示词约束, 实际权限需由目标环境控制.

通用是指正文无需按仓库改写即可使用. 内容不绑定语言, 框架, 目录模板或开发工具; 实际命令与约束由 Agent 从目标仓库中发现. 使用者仍可按自身需要定制.

仓库只负责创建, 修改和存放这些文件, 不提供通过 Agent 插件或 npx skills 等工具下载, 安装或同步内容的机制. 复制后的内容由使用者自行维护.

补充项目说明是可选项. 优先从代码, 测试和配置中获取事实, 只在需要时补充无法可靠推断的约束或决策原因, 不重复维护项目已有信息.

原则提供判断依据. 能可靠自动验证的约束, 按需落实到项目现有的类型, 测试和检查工具中. 代码量等指标用于发现问题, 具体门槛由项目决定.

## skills

- [refactor-analysis](skills/refactor-analysis/SKILL.md): 调查具体维护困难, 比较职责边界, 交付重构依据, 目标结构与首个可验证范围, 不修改代码.
- [refactor](skills/refactor/SKILL.md): 根据具体结构问题或目标实施重构, 保持行为与契约, 小步优化代码和文件组织, 收敛状态与配置.
- [test-maintenance](skills/test-maintenance/SKILL.md): 根据契约变化或测试脆弱, 重复, 膨胀等问题维护测试, 判断新增, 改写, 合并, 迁移和删除, 保留仍有效的验证.
- [debug](skills/debug/SKILL.md): 对原因尚未确定的缺陷, 错误或失败检查建立复现, 区分候选原因, 交付根因证据与未确认事项.
- [fix-bug](skills/fix-bug/SKILL.md): 根据已确认的原因和预期行为实施缺陷修复, 验证原触发场景及受影响的行为.
- [review](skills/review/SKILL.md): 审查代码变更或指定范围, 报告有触发条件, 实际影响和证据的正确性, 兼容性及验证问题.
- [git-history-as-adr](skills/git-history-as-adr/SKILL.md): 优先从 Git 提交说明与差异还原设计原因, 方案取舍和后续演进, 核对历史约束是否仍适用, 区分事实与推断.
- [plan-commits](skills/plan-commits/SKILL.md): 从实际变更设计提交边界, 配套内容和依赖顺序, 只交付方案, 不操作暂存区或历史.
- [decision-rich-commits](skills/decision-rich-commits/SKILL.md): 为边界已明确的变更编写兼容 Conventional Commits 的 message, 保留背景, 决策和理由, 重要决策模板按需加载.

技能的 `description` 使用英文描述能力与适用场景, 正文保留中文工作方法. 具体发现与加载方式由目标工具决定, 不要求每次读取全部技能. 按需加载可以减少无关上下文, 但不保证技能被选中或指令被完全遵守; 实际效果通过任务反馈判断.

诊断, 重构分析和提交边界设计各自以证据或方案作为阶段产出, 对应的实施技能只核对当前需要的依据. 例如, 原因未知时先诊断; 用户已提供充分的故障原因和修复要求时, 可以直接修复. 已明确的局部重构和单一目的提交也不必先运行分析技能. 各技能可独立复制, 不建立固定调用链, 不要求额外的交接文档.

阶段完成是当前任务内部的里程碑. 用户已要求实施时, 继续完成授权范围内的修改与验证, 不为切换技能反复请求确认; 用户只要求诊断, 分析或方案时, 交付该阶段结果. 拆分技能能减少加载的后续流程, 但不会自动清除模型已读过的上下文, 不能仅凭文件拆分保证阶段隔离或工作投入.

## agents

| 角色 | 适用任务 | 返回结果 |
| --- | --- | --- |
| [code-explorer](agents/code-explorer.md) | 查明入口, 调用链, 数据流及修改影响边界 | 关键路径与符号, 实现关系, 约束和未查明事项 |
| [debugger](agents/debugger.md) | 复现故障, 检查候选原因并定位根因 | 复现条件, 原因与证据, 未排除假设, 修复及验证建议 |
| [reviewer](agents/reviewer.md) | 独立审查指定差异或代码范围 | 有触发条件, 影响和位置的发现, 实际审查范围与限制 |
| [history-researcher](agents/history-researcher.md) | 追溯设计或兼容逻辑的原因与演进 | 历史证据, 当前仍有效的约束, 事实与推断的区分 |

这些角色只调查并返回结果, 不修改项目文件或外部状态, 不继续委派. 需要修改才能验证时返回实验建议, 由主 agent 统一修复, 整合与最终验收. `debug` 技能专注根因诊断, 可在任务权限内进行临时实验; `debugger` 角色保持只读调查边界, `fix-bug` 技能承担已知原因的修复与回归验证. 技能与角色不要求一一对应.

上下文隔离依靠实际委派: 主 agent 传递目标, 范围, 必要背景, 约束与预期产出, subagent 自行读取相关材料并返回结论与证据索引. 不默认传递完整对话或回传大段日志. 上下文隔离不代表工作区隔离, 只读调查中的检查也应避免干扰其他工作.

例如, 重构一个跨模块流程时, 主 agent 可使用 `refactor` 技能, 先选取一段可独立验证的完整行为, 将影响本步修改的调用关系交给 `code-explorer` 调查, 将已定位的兼容分支交给 `history-researcher` 查证. 两个问题已有独立入口时可并行; 如果历史问题依赖探索结果, 则收到结果后再委派. 当前行为的契约与修改边界已有充分依据时, 主 agent 即可实施本步修改并验证, 仅等待会影响当前决定的调查结果, 同时避免修改干扰仍在进行的调查. 需要独立审查时将本步差异交给 `reviewer`, 根据验证, 审查与用户反馈修正实现和下一步范围, 持续小步交付.

小改动直接完成即可. 使用 subagent 应围绕明确问题, 帮助更快获得有效反馈, 消除当前阻塞或完成本轮交付, 并计入协调成本. 不要求每次加载全部角色或执行固定流程. 文件本身不保证效果或并行效率, 需通过实际任务反馈判断.

## 维护

修改本仓库时遵循 [AGENTS.md](AGENTS.md), 其中包含内容组织, skill 触发描述与验证约定. 供其他项目复制的工程原则仍使用 [template/agent.md](template/agent.md).

## 参考资料

以下资料支持不同方面的设计判断, 不作为必须整套采用的规则.

- [敏捷宣言](https://agilemanifesto.org/iso/zhchs/manifesto.html) 与 [十二条原则](https://agilemanifesto.org/iso/zhchs/principles.html): 尽早交付价值, 保持用户协作, 响应变化, 持续改善设计和工作方式.
- Parnas 的 [模块划分论文](https://www.cs.lafayette.edu/~gexia/cs301/resources/parnas.html): 围绕设计决策划分边界, 用信息隐藏减少变更传播.
- Ousterhout 的 [模块抽象讲义](https://web.stanford.edu/~ouster/CS349W/lectures/abstraction.html) 和 [复杂度讲义](https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=complexity): 用简单接口隐藏复杂实现, 关注理解负担和修改影响.
- Matt Pocock 的 [improve-codebase-architecture](https://github.com/mattpocock/skills/tree/main/skills/engineering/improve-codebase-architecture) 与 [codebase-design](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design): 从维护困难选择重构区域, 计入调用者必须掌握的全部知识, 推演删除抽象后的复杂度去向, 验证组合行为.
- Fowler 对 [简单设计](https://martinfowler.com/bliki/BeckDesignRules.html) 和 [YAGNI](https://martinfowler.com/bliki/Yagni.html) 的阐释: 保证行为与表达清晰, 减少多余元素, 推迟未被需要的能力.
- Liskov 与 Wing 的 [行为子类型论文](https://www.cs.cmu.edu/~wing/publications/LiskovWing94.pdf): 替换实现时保持调用者依赖的行为契约.
- Martin 的 [开闭原则论文](https://www.cs.utexas.edu/~downing/papers/OCP-1996.pdf): 有选择地隔离变化, 无法对所有变化预先封闭.
- [Software Engineering at Google 的工程权衡](https://abseil.io/resources/swe-book/html/ch01.html) 与 [单元测试](https://abseil.io/resources/swe-book/html/ch12.html): 考虑软件寿命与总体成本, 用行为测试支持持续修改.
- Microsoft Research 的 [软件度量研究](https://www.microsoft.com/en-us/research/publication/mining-metrics-to-predict-component-failures/): 复杂度指标可辅助识别风险, 该研究在五个系统中未发现通用的最佳缺陷预测指标组合.
