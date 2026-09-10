---
name: refactor-analysis
description: |-
  Assess maintenance problems and recommend a justified refactoring boundary, target structure, and first verifiable scope.
  Use when:
  - A user asks where or whether to refactor, or requests a structural assessment or refactoring plan.
  - Scattered rules, unclear state ownership, or changes that span modules require comparing responsibility boundaries before choosing a change.
  - File organization or an existing abstraction makes related code hard to find or change, and the benefit and compatibility cost of restructuring are unclear.
  Not for:
  - Implementing an already understood refactoring, diagnosing an unexplained failure, or managing a goal and its issue backlog.
---

# 重构分析

围绕指定范围调查实际维护困难, 明确是否值得重构, 哪个边界需要改变及必须保留的行为. 本阶段只交付依据和方案, 不修改实现, 测试或配置, 不把分析变成全库清理任务.

阶段产出作为当前任务的依据. 原请求仅限本阶段时交付结果; 原请求还包含实施时, 完成本阶段后按已有授权继续, 不把阶段结束当作整个任务完成, 不为切换阶段新增确认.

## 建立本轮依据

- 用户指定问题或区域时从该范围调查. 开放式探索时, 可结合可用历史中的近期反复修改, 缺陷修复和跨模块联动选择调查区域. 变更频率只用于确定调查优先级, 是否重构仍以实际维护困难为依据.
- 从待改流程的入口追踪实际调用, 依赖, 数据流和副作用, 阅读相关实现, 配置与测试, 检查相关文件的命名与目录层级. 识别工作区已有修改, 避免覆盖其他工作.
- 特殊设计或兼容逻辑的原因无法从当前实现判断时, 定向查阅可用的版本历史和变更讨论, 核对历史约束是否仍适用. 缺失的原因保持为未知, 不据此认定实现无用.
- 环境支持委派且调查可独立开展时, 可将具体代码关系或历史约束问题交给 subagent, 明确只调查并返回证据与未确认事项. 主 agent 核对结果, 统一分析结论; 不重复进行同一轮探索, 不让调查与正在修改的内容相互干扰. 无委派能力时直接完成, 不要求特定角色文件.
- 优先处理与本轮目标直接相关的维护困难, 找到具体的复杂度来源: 同一规则需要多处修改, 调用方必须了解内部步骤, 多份状态需要同步, 或配置与隐式回退让执行路径难以判断. 文件大小, 目录深度与代码相似度只提供线索, 不构成必须重构的证据.
- 检查职责混放, 相关实现分散, 命名或层级妨碍定位等组织问题, 核对目录表达的边界是否符合实际职责与依赖. 即使逻辑无需修改, 文件组织造成的理解困难也可以独立成为重构依据.
- 明确必须保留的完整流程及其成功与失败行为, 确定调用方依赖的输入, 输出和副作用. 复用现有检查建立验证基线, 记录已有失败或尚未覆盖的关键行为.

## 比较目标边界

- 用具体维护场景比较现状与候选结构: 哪条规则能集中, 哪份状态能明确归属, 调用方可以少知道哪些前提, 或一次相关修改能减少哪些联动. 不为凑方案数列举无关架构.
- 推演拟删除或转移的职责最终由谁承担, 核对完整流程中的输入, 输出, 失败状态与副作用. 将迁移, 验证和兼容成本计入收益, 不把复杂度转移到调用方当作消除复杂度.
- 选择一段可独立验证的完整行为作为首个调整范围, 说明它如何检验目标边界的关键假设. 不按数据库, API, 前端等技术层机械铺开全部工作.

## 交付分析结论

说明问题证据及位置, 推荐边界与取舍, 保留行为, 首个可验证范围, 可用检查及尚未确认的约束. 没有足够收益时可以建议保持现状; 不以代码较长或形式不统一证明必须重构.

依据应足以解释为什么值得改, 为什么选这个边界, 如何发现行为回归. 缺少影响决定的证据时继续定向调查; 只有无法从项目查明且影响关键选择时才澄清. 达到上述条件或遇到明确阻塞时结束本阶段, 不为了多列重构机会扩大范围.
