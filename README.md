# 通用 Agent 工程模板与技能

本仓库提供可直接复制的 [工程原则模板](template/agent.md) 与 [技能](skills). 模板提供常驻的核心工程判断, 技能提供按任务使用的具体方法, 帮助 Agent 通过交付, 验证和反馈满足真实需求, 降低理解与修改成本. 模板存放在 `template/agent.md`, 避免被当作本仓库的 Agent 指令加载.

## 使用

- 工程原则: 将 `template/agent.md` 的内容复制到目标仓库的 `AGENTS.md`, 可独立使用, 不要求安装技能. 目标文件已有指令时合并适用内容, 不覆盖项目约束.
- 技能: 按需将 `skills/` 下的单个技能目录复制到目标工具支持的技能位置, 保留目录名和 `SKILL.md`. 每个技能可独立使用, 不要求同时复制工程原则模板或其他技能.

通用是指正文无需按仓库改写即可使用. 内容不绑定语言, 框架, 目录模板或开发工具; 实际命令与约束由 Agent 从目标仓库中发现. 使用者仍可按自身需要定制.

仓库只负责创建, 修改和存放这些文件, 不提供通过 Agent 插件或 npx skills 等工具下载, 安装或同步内容的机制. 复制后的内容由使用者自行维护.

补充项目说明是可选项. 优先从代码, 测试和配置中获取事实, 只在需要时补充无法可靠推断的约束或决策原因, 不重复维护项目已有信息.

原则提供判断依据. 能可靠自动验证的约束, 按需落实到项目现有的类型, 测试和检查工具中. 代码量等指标用于发现问题, 具体门槛由项目决定.

## skills

- [refactor](skills/refactor/SKILL.md): 通用重构技能, 在保持行为与契约的前提下优化代码结构, 文件组织与目录结构, 收敛状态和配置, 降低理解与修改成本.
- [test-maintenance](skills/test-maintenance/SKILL.md): 根据契约变化或测试脆弱, 重复, 膨胀等问题维护测试, 判断新增, 改写, 合并, 迁移和删除, 保留仍有效的验证.
- [debug](skills/debug/SKILL.md): 对原因尚未确定的缺陷, 错误或失败检查建立复现, 用证据定位根因, 完成修复与回归验证.
- [review](skills/review/SKILL.md): 审查代码变更或指定范围, 报告有触发条件, 实际影响和证据的正确性, 兼容性及验证问题.
- [decision-history](skills/decision-history/SKILL.md): 追溯设计与兼容逻辑的历史原因, 核对约束是否仍适用, 区分已知依据与未解决的问题.

技能的 `description` 用于描述能力与适用场景, 正文提供工作方法. 具体发现与加载方式由目标工具决定, 不要求每次读取全部技能. 按需加载可以减少无关上下文, 但不保证技能被选中或指令被完全遵守; 实际效果通过任务反馈判断.

## 维护

- 根据真实任务中的失败, 验证结果和维护成本改进原则与技能. 新增内容前, 先确认它解决什么问题, 何时适用, 是否与已有内容重复或冲突.
- 模板只保留值得跨任务提醒的核心判断, 具体方法归入对应技能. 已有覆盖不重复搬运, 模型通常已具备的一般知识可直接删去, 不要求每条旧规则另找存放位置.
- 阅读并提炼参考材料, 将适用的判断方法直接写入正文. 优先合并, 改写和删除, 不堆叠原则名称或特定项目流程; 使用技能不以阅读原资料为前提.
- 每个技能存放在 `skills/<技能名>/SKILL.md`, 在本文件的 skills 章节维护链接与简短介绍. 文档使用简体中文和 ASCII 标点, 技术名称与链接保留原文.

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
