# 自用的 Agent 工程原则与技能

本仓库保存自用的 [AGENTS.md](AGENTS.md) 与 [skills](skills) 文件, 以敏捷开发和持续设计为主线, 帮助 Agent 在交付, 验证和反馈中满足真实需求, 持续降低软件的理解与修改成本.

## 使用

按需选择 AGENTS.md 或技能, 在自己的目标目录创建相应文件, 手工复制粘贴内容, 再根据实际需求决定是否定制或修改. 每个技能可单独复制使用, 不要求同时复制本仓库的 AGENTS.md. 内容不依赖特定语言, 框架或开发工具.

仓库只负责创建, 修改和存放这些文件, 不提供通过 Agent 插件或 npx skills 等工具下载, 安装或同步内容的机制. 复制后的内容由使用者自行维护.

补充项目说明是可选项. 优先从代码, 测试和配置中获取事实, 只在需要时补充无法可靠推断的约束或决策原因, 不重复维护项目已有信息.

原则提供判断依据. 能可靠自动验证的约束, 按需落实到项目现有的类型, 测试和检查工具中. 代码量等指标用于发现问题, 具体门槛由项目决定.

## skills

- [refactor](skills/refactor/SKILL.md): 通用重构技能, 在保持行为与契约的前提下简化结构, 收敛状态和配置, 降低理解与修改成本.

## 维护

- 根据真实任务中的失败, 验证结果和维护成本改进原则与技能. 新增内容前, 先确认它解决什么问题, 何时适用, 是否与已有内容重复或冲突.
- 阅读并提炼参考材料, 将适用的判断方法直接写入正文. 优先合并, 改写和删除, 保持文档简洁, 不堆叠原则名称或特定项目流程; 使用技能不以阅读原资料为前提.
- 每个技能存放在 `skills/<技能名>/SKILL.md`, 在本文件的 skills 章节维护链接与简短介绍. 文档使用简体中文和 ASCII 标点, 技术名称与链接保留原文.

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
