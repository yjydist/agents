# 面向 Agent 的软件工程原则

本仓库维护可跨项目复制的 [AGENTS.md](AGENTS.md), 以敏捷开发和持续设计为主线, 帮助 Agent 在交付, 验证和反馈中满足真实需求, 持续降低软件的理解与修改成本.

## 使用

将 AGENTS.md 的内容复制或合并到项目中, 按当前任务与项目约束微调. 文档不依赖特定语言, 框架或开发工具, 可以独立使用.

补充项目说明是可选项. 优先从代码, 测试和配置中获取事实, 只在需要时补充无法可靠推断的约束或决策原因, 不重复维护项目已有信息.

原则提供判断依据. 能可靠自动验证的约束, 按需落实到项目现有的类型, 测试和检查工具中. 代码量等指标用于发现问题, 具体门槛由项目决定.

## 维护

- 根据真实任务中的失败, 验证结果和维护成本改进原则. 新增条目前, 先确认它解决什么问题, 何时适用, 是否与已有条目重复或冲突.
- 吸收书籍和研究中可迁移的判断方法, 结合适用条件取舍. 优先合并, 改写和删除, 保持文档简洁, 不堆叠原则名称或特定项目流程.
- 本仓库只维护模板及其说明. 文档使用简体中文和 ASCII 标点, 技术名称与链接保留原文.

## 参考资料

以下资料支持不同方面的设计判断, 不作为必须整套采用的规则.

- [敏捷宣言](https://agilemanifesto.org/iso/zhchs/manifesto.html) 与 [十二条原则](https://agilemanifesto.org/iso/zhchs/principles.html): 尽早交付价值, 保持用户协作, 响应变化, 持续改善设计和工作方式.
- Parnas 的 [模块划分论文](https://www.cs.lafayette.edu/~gexia/cs301/resources/parnas.html): 围绕设计决策划分边界, 用信息隐藏减少变更传播.
- Ousterhout 的 [模块抽象讲义](https://web.stanford.edu/~ouster/CS349W/lectures/abstraction.html) 和 [复杂度讲义](https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=complexity): 用简单接口隐藏复杂实现, 关注理解负担和修改影响.
- Fowler 对 [简单设计](https://martinfowler.com/bliki/BeckDesignRules.html) 和 [YAGNI](https://martinfowler.com/bliki/Yagni.html) 的阐释: 保证行为与表达清晰, 减少多余元素, 推迟未被需要的能力.
- Liskov 与 Wing 的 [行为子类型论文](https://www.cs.cmu.edu/~wing/publications/LiskovWing94.pdf): 替换实现时保持调用者依赖的行为契约.
- Martin 的 [开闭原则论文](https://www.cs.utexas.edu/~downing/papers/OCP-1996.pdf): 有选择地隔离变化, 无法对所有变化预先封闭.
- [Software Engineering at Google 的工程权衡](https://abseil.io/resources/swe-book/html/ch01.html) 与 [单元测试](https://abseil.io/resources/swe-book/html/ch12.html): 考虑软件寿命与总体成本, 用行为测试支持持续修改.
- Microsoft Research 的 [软件度量研究](https://www.microsoft.com/en-us/research/publication/mining-metrics-to-predict-component-failures/): 复杂度指标可辅助识别风险, 该研究在五个系统中未发现通用的最佳缺陷预测指标组合.
