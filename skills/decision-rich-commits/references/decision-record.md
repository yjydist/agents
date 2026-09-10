# 重要决策的提交说明

用于架构, API, 数据模型, 持久化, 安全, 性能, 并发, 兼容性, 部署或重要运维行为.

推荐结构:

```text
<type>(<scope>): <description>

背景:
<问题和约束>

决策:
<选择的方案>

理由:
<为什么这个方案更适合当前约束>

备选方案:
- <真实考虑过的方案>: <没有选择的原因>

影响:
- <重要权衡, 新不变量, 迁移要求或后续义务>

Decision-Relates-To: <sha>
Decision-Supersedes: <sha>
Decision-Follows-Up: <sha>
Refs: <issue-or-ticket>
```

只保留有长期价值的部分. 没有真实信息就不要写对应 section.

## 决策关系 trailer

当 commit 和历史决策有明确关系时, 可以使用 Git trailer:

```text
Decision-Relates-To: <sha>
Decision-Supersedes: <sha>
Decision-Follows-Up: <sha>
Refs: <issue-or-ticket>
```

使用规则:

- `Decision-Relates-To`: 与另一个决策相关, 但不是替代关系.
- `Decision-Supersedes`: 当前决策明确替代旧决策.
- `Decision-Follows-Up`: 当前 commit 是前一个决策的计划内后续步骤.
- `Refs`: 关联 issue, ticket 或其他稳定引用.

不要为了建立关系图而滥用 trailer.

