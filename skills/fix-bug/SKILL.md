---
name: fix-bug
description: |-
  Correct an established defect and verify the original trigger, affected behavior, and regression protection.
  Use when:
  - A user requests a fix and the cause and expected behavior are established.
  - Diagnosis or an evidenced review finding within an authorized repair task has identified the faulty rule, state transition, or configuration.
  - A known correction needs to be completed and checked against the original failure and affected callers.
  Not for:
  - Failures whose cause or expected behavior still needs investigation, diagnosis-only requests, or new feature requirements.
---

# 缺陷修复与回归验证

根据已建立的原因和预期行为, 在授权范围内完成修复与验证. 依据可以来自当前任务, 用户提供的复现或已有诊断, 不要求先运行其他技能. 仅请求诊断时不实施修复.

## 核对修复依据

- 阅读相关实现, 调用方, 配置与测试, 检查工作区已有修改, 确认诊断针对当前状态. 原因至少应有从触发条件到错误结果的证据, 不能只依赖先前的完成声明.
- 明确需要恢复的行为, 兼容要求, 失败语义和必要副作用. 预期来自需求或契约, 不能从拟采用的修复反推.
- 原因仍有关键歧义或新证据推翻诊断时, 回到该问题的调查, 不继续试改. 从项目发现适用的运行与检查方式, 不要求固定工具或独立诊断文档.

## 修复与验证

- 修复造成偏差的规则, 状态管理或边界处理, 必要时做相关结构调整. 不用吞错, 无依据的默认值, 无界重试或跳过检查掩盖问题.
- 建立与风险相称的回归验证, 其预期来自需求或契约, 不复制修复实现. 对关键修复, 确认检查能因目标缺陷失败, 再确认修复后通过; 无法验证修复前状态时说明限制.
- 验证原触发场景及受影响的边界, 失败状态和调用方行为, 完成相关项目检查. 修复环境或配置问题时验证实际故障链路, 不只检查文件格式.
- 审阅实际差异, 保留用户已有工作, 移除临时诊断内容. 证据不支持的试改不应混入最终修复.

交付时说明原因及其证据, 修复后的行为, 实际验证和未确认部分. 部分缓解须如实说明, 不将其表述为根因已修复.
