---
name: debug
description: |-
  Diagnose failures and return root-cause evidence, remaining uncertainty, and regression scenarios for a correction.
  Use when:
  - A user reports a bug or requests diagnosis or a repair whose cause is still unknown.
  - An unexplained error, failed check, regression, or intermittent failure blocks the current task.
  - A failure could come from product behavior, test expectations, configuration, or the environment, and the cause must be distinguished before changing it.
  Not for:
  - Implementing an established correction, maintaining tests with understood problems, or reviewing a diff without a reported failure.
---

# 根因诊断

围绕报告的问题建立证据, 定位能解释现象的原因. 本阶段交付诊断结论, 不实施产品修复, 不以找到一处可疑代码作为结束条件. 从仓库配置和已有工具发现运行与检查方式, 不假定语言, 框架或部署环境.

阶段产出作为当前任务的依据. 原请求仅限本阶段时交付结果; 原请求还包含实施时, 完成本阶段后按已有授权继续, 不把阶段结束当作整个任务完成, 不为切换阶段新增确认.

## 确定问题与复现

- 区分已观察的事实, 预期行为与待验证假设. 从需求, 调用方或外部契约核对预期; 报错文字和已有测试预期也可能需要查证.
- 阅读相关入口, 实现, 配置和失败输出, 检查当前工作区修改. 只收集能影响本次判断的输入, 状态和环境差异, 不输出凭据或无关敏感数据.
- 优先复用失败检查或用户给出的步骤建立最小复现, 保留触发问题所需的条件. 不稳定故障记录出现和未出现时的差异, 不把偶然成功当作问题消失.
- 无法复现时利用可用日志, 静态路径和相关历史缩小范围, 明确哪些结论尚未证实. 仅在缺失信息阻止关键判断时向用户询问具体输入或条件.

## 用检查区分原因

- 环境支持委派且候选原因可独立调查时, 可将具体假设与已知证据交给 subagent, 明确只调查并返回检查结果与未确认部分. 汇总并核对证据后更新根因判断, 不并行试改同一故障路径或运行会相互干扰的检查. 无委派能力时直接完成, 不要求特定角色文件.
- 从异常结果沿实际数据流, 状态变化和副作用追踪, 找到最早偏离预期的位置. 检查可能跨越的调用边界, 不把最后抛错的位置直接当成根因.
- 针对当前证据提出有限候选原因, 选择结果能区分这些原因的最小检查. 检查前明确不同结果各说明什么, 得到结果后更新判断, 避免无依据地反复试改.
- 区分产品缺陷, 测试预期错误, 环境或配置问题及已有失败. 历史变更可以提供线索, 但时间相邻或代码可疑不等于因果关系.
- 临时日志或实验只用于回答具体问题, 控制影响范围并清理本轮临时改动. 无新证据时更换调查方向或说明阻塞, 不重复相同失败操作.

## 交付诊断依据

说明复现条件, 预期与实际行为, 原因及可定位证据, 实际检查与结果, 尚未排除的假设. 指出需要恢复的规则或契约, 以及能暴露该问题的回归场景, 不写完整实施流程.

结论须能解释从触发条件到错误结果的因果链, 并有区分候选原因的检查或可追踪的静态证据. 无法复现或验证时降低结论强度, 说明缺失证据及下一项有区分力的检查, 不伪装成根因已确认. 清理本轮临时诊断改动, 保留用户已有工作; 证据足以支持判断或遇到明确阻塞时结束本阶段.
