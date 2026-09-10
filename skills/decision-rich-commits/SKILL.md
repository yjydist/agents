---
name: decision-rich-commits
description: |-
  Write Conventional Commit messages for coherent changes, preserving evidenced context, decisions, tradeoffs, and consequences at an appropriate level of detail.
  Use when:
  - A user asks to write or improve commit messages for defined changes.
  - An authorized commit task has understood change boundaries and needs decision-rich messages.
  - A commit message needs to explain architectural, API, compatibility, or migration decisions whose reasons and relationship to earlier decisions are absent from the diff.
  Not for:
  - Resolving mixed commit boundaries, investigating unknown historical rationale, standalone ADR authoring, or routine coding without a commit-message need.
metadata:
  short-description: 为完整变更编写保留决策理由的 commit message
---

# 写出保留决策理由的 commit message

让未来的人或 agent 从每个 commit 理解改了什么, 为什么要改, 为什么选择这个方案, 以及它与前后决策的关系. 按当前请求和已有授权执行; 仅请求 message 时交付文本, 不因加载本技能而 stage, 创建提交或改写历史.

## 核对说明对象

- 检查工作区状态, 相关 staged 与 unstaged diff, 新增文件及用户指定范围, 确认说明对应哪一个完整变化. 不把当前暂存区自动当成合理边界, 不遗漏未暂存但属于同一行为的测试或配置.
- 边界已有依据时直接核对, 不重新规划全部提交. 若发现多个无关目的, 缺失的配套变更或未解决的迁移依赖, 先解决具体边界问题, 不用一篇长 message 掩盖它.
- 从需求, 当前讨论和实际差异提取背景与理由. 不编造备选方案, benchmark, incident 或 requirement; 不确定的动机保留为未知.
- message 只描述对应 commit 实际包含的变化, 不把整个任务, PR 或未来目标写成该 commit 已完成的结果. 执行已授权的提交操作时, 精确 stage 对应内容并核对最终 diff, 内容变化后同步调整 message.

## Commit message 基本结构

保持 Conventional Commits 兼容:

```text
<type>[optional scope][!]: <description>
```

例如:

```text
feat(auth): support overlapping signing keys during rotation
```

优先遵守仓库已有的 type 和 scope 约定. header 描述结果, 不写模糊的操作过程.

## 根据决策密度决定 message 长度

不是每个 commit 都需要完整 ADR.

### Level 0: 简单或机械变化

例如 typo, format, generated file refresh.

通常只需要 header:

```text
docs(readme): fix installation command typo
```

### Level 1: 普通行为变化

当理由不能从 diff 直接看出时, 增加简短 body:

```text
<type>(<scope>): <description>

背景:
<为什么需要这个变化>

决策:
<选择了什么, 以及最关键的原因>
```

### Level 2: 重要决策

涉及架构, API, 数据模型, 兼容性, 性能等重要取舍, 或需要表达与已有决策的关系时, 读取 [重要决策模板与 trailer](references/decision-record.md). 仅保留有实际依据和长期价值的部分, 普通提交不加载该参考.

## Body 应该记录什么

### 背景

说明为什么必须做这个变化.

优先记录:

- 原方案哪里不够
- 必须保持什么不变量
- 有什么兼容要求
- 有什么性能, 安全或运维约束
- 为什么现在需要改变

不要把 diff 过程重新描述一遍.

### 决策

说明这个 commit 建立了什么行为, 规则, 架构或实现策略.

### 理由

说明为什么选择这个方案.

重点写代码本身无法可靠表达的信息.

### 备选方案

只写真实考虑过的方案.

不要为了让 message 看起来完整而编造备选方案.

### 影响

记录这个决策带来的长期结果, 例如:

- 新的不变量
- 兼容窗口
- 暂时保留的 legacy path
- migration 要求
- 性能或存储成本
- 运维责任
- 未来删除条件

## 最终检查

核对 header 是否准确描述结果, body 是否补充 diff 无法可靠表达的 why, 理由是否有实际依据. 如果未来的人或 agent 只找到这个 commit, 应能说明改了什么, 为什么这样改, 以及 revert 会撤销什么. 简单变化无需为填满格式增加段落.
