---
name: plan-commits
description: |-
  Propose cohesive commit boundaries and dependency order from actual changes, including companion tests and verifiable intermediate states.
  Use when:
  - A user asks to split a working diff, group changes into commits, reorganize existing commits, or plan their sequence.
  - An authorized commit task contains mixed purposes, partial staging, or migration dependencies that need boundary analysis.
  - Follow-up fixes or incomplete companion changes make it unclear which changes belong together for review and rollback.
  Not for:
  - Writing a message for an already coherent change, decomposing future work into issues, or routine coding without a commit-related request.
---

# 设计 commit 边界

根据实际变更及其目的, 设计可以独立理解, 审查和合理回滚的提交单元与顺序. 本阶段只交付边界方案, 不 stage, 创建提交, 改写历史或撰写最终 commit message.

阶段产出作为当前任务的依据. 原请求仅限本阶段时交付结果; 原请求还包含实施时, 完成本阶段后按已有授权继续, 不把阶段结束当作整个任务完成, 不为切换阶段新增确认.

## 检查实际变化

- 检查 `git status --short`, staged 与 unstaged diff, 新增文件及相关需求. 不把当前暂存区当作既定边界; 区分当前任务与用户已有的无关工作.
- 整理已有提交时, 从用户指定的范围和可用历史确定比较基线. 无法判断且不同基线会实质改变方案时再澄清, 不默认改写所有历史.
- 从变更目的与理由识别独立决策, 核对实现, 测试, 配置和迁移之间的依赖. 不按文件数量, 目录或 diff 大小机械拆分; 同一文件内的变化也可能属于不同提交.

## 按语义划分

- 一个 commit 应表达一个完整且连贯的变化, 有一个主要目的和一套主要理由. 两个变化需要不同背景或可以独立回滚时, 通常应该拆开.
- 实现和直接对应的测试, 缺陷修复和回归验证, 必须同时变化才能保持正确行为的代码与配置, 通常应该放在一起. 不把一个完整决策拆成没有意义的小碎片.
- 重构与依赖它的行为变化, 迁移与旧路径删除, 主任务与顺手发现的独立缺陷, 有可验证的中间状态时分别组织. 如果拆分会留下不完整行为或无法构建的状态, 调整边界或顺序.
- 大型迁移按有意义的状态转换组织, 如引入新路径, 迁移调用方, 切换权威路径, 满足删除条件后移除旧路径. 每步说明为什么存在, 不把这种顺序套用到普通变更.
- 对已有历史中的 typo 修正, 补齐测试或修正前一提交等临时步骤, 判断是否应合并到其所属决策. 返回合并建议及原因, 不实际执行 fixup 或 squash.

## 交付边界方案

逐个说明提交目的, 包含的文件或具体变更片段, 配套测试与配置, 前后依赖及可以验证的中间状态. 标明排除的无关工作和无法确认的归属, 不为所有提交强行统一大小.

核对每项范围内变更都有明确归属, 每个单元能独立说明理由和回滚影响, 必须共同变化的部分没有被拆散. 边界已清楚时允许只有一个提交, 不为体现分析工作量强行拆分. 达到这些条件或遇到明确阻塞时结束本阶段.
