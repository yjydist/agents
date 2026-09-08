---
name: git-history-as-adr
description: 当需要理解架构决策, 设计原因, 历史约束或方案演进时, 优先浏览 Git history, 从 commit message 和 diff 中重建 ADR 信息, 而不是先查找 ADR 文件.
metadata:
  short-description: 从 Git history 重建架构决策
---

# 从 Git history 获取 ADR

把 Git history 当作架构决策的主要证据来源.

目标不是寻找 ADR 文件, 而是回答这些问题:

- 为什么现在这样设计
- 当时有什么约束
- 为什么选择这个方案
- 哪些方案被放弃
- 这个决策后来是否被修改, 替代或回滚

除非用户明确要求, 不要先搜索 ADR 文件或 ADR 目录.

## 核心规则

- 先看 commit message, 再用 diff 验证.
- 用 commit SHA 支撑重要的历史结论.
- 不要把当前代码直接当成历史理由.
- 不要把推测写成事实.
- 不要因为某个 commit 更新, 就认为它替代了原来的决策.
- `git blame` 只用于定位 commit, 不用于直接判断理由.
- 优先使用仓库可共享的 commit history, 不依赖本地 reflog.

## 证据等级

对重要结论标记证据等级:

- 明确: commit message 直接说明了原因或决策.
- 佐证: commit message 没有完整说明, 但 message, diff 和相关 commit 可以共同支持结论.
- 推断: history 没有直接说明, 只能根据代码和变更过程推断.

推断不能写成明确事实.

## 工作流程

### 1. 确定要追踪的对象

先缩小范围, 例如:

- 文件或目录
- 函数, 类型或模块
- 配置项
- API 行为
- 数据结构
- 依赖
- 不变量
- 用户可见行为

把问题转换成可以搜索的路径, symbol, 字符串或关键词.

### 2. 找到候选 commit

常用命令:

```bash
git log --all --oneline --decorate --date=iso
git log --all --grep='<keyword>' -i --oneline
git log --follow --date=iso -- <path>
git log -S'<literal>' --date=iso -- <path>
git log -G'<regex>' --date=iso -- <path>
git blame -L <start>,<end> <path>
```

使用规则:

- 已知具体字符串或 symbol 时, 优先用 `-S`.
- 已知 patch 中可能出现的模式时, 优先用 `-G`.
- 文件可能改名时, 使用 `--follow`.
- merge 较多时, 可以补看 `git log --first-parent --oneline`.

不要把第一个搜索结果直接当成决策 commit.

### 3. 检查 commit message 和 diff

对候选 commit 至少检查:

```bash
git show --format=fuller --stat <sha>
git show --format=fuller --patch <sha> -- <path>
```

重点寻找:

- 问题是什么
- 有什么约束
- 选择了什么方案
- 为什么这样选
- 是否提到备选方案
- 有什么兼容性要求
- 有什么性能, 安全或运维限制
- 是否留下迁移成本或后续工作

### 4. 追踪决策演进

不要只看引入变更的 commit. 继续向后查找:

- revert
- fix
- migration
- deprecation
- replacement
- compatibility change
- cleanup

判断当前状态:

- active: 决策仍然有效.
- superseded: 后续决策已经替代它.
- reverted: 决策被明确回滚.
- partially-superseded: 核心决策仍在, 但部分约束已经改变.
- uncertain: history 不足以确定当前意图.

### 5. 重建决策记录

优先输出简洁结论, 不要直接倾倒 git log.

推荐格式:

```text
决策: <一句话说明当前或历史决策>
状态: <active | superseded | reverted | partially-superseded | uncertain>

背景:
- <问题或约束>

决策内容:
- <选择了什么>

理由:
- <为什么这样选择>

备选方案:
- <只有 history 明确支持时才写>

影响:
- <重要权衡, 兼容要求, 迁移成本或后续义务>

演进:
- <后续如何修改这个决策>

证据:
- <sha> <subject> - <明确 | 佐证 | 推断> - <为什么相关>

置信度: <high | medium | low>
```

没有证据的部分直接省略. 不要为了补齐模板而编造内容.

## 常见情况

### commit message 很弱

如果 message 只有 `fix bug`, `refactor` 这类内容, 只能报告 diff 可以支持的事实. 对理由使用推断等级.

### history 被 squash

如果 feature 被 squash merge, 以 squash commit 作为主要决策边界. 不要假设已经丢失的 branch history 仍然存在.

### commit 混合多个目的

分别判断每一部分变更. 不要用一个理由解释整个 commit.

### 后续 fix 暴露了原始约束

可以把后续 fix 当成重要证据. 如果原始理由没有被直接写明, 仍然标记为佐证或推断.

## 输出要求

- 先给决策结论, 再给证据.
- 只列支撑结论所需的关键 commit.
- 重要历史判断带 SHA.
- 明确区分历史事实和当前工程建议.
- 证据不足时直接说明不确定.