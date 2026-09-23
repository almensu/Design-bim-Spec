# Recursive Self-Improvement Protocol

这份协议定义 Design-bim-Spec 在什么证据下可以说“自己变好了”。

“自己”指：
- `SKILL.md` 路由；
- `references/` 规则；
- DRS schema；
- review checklist；
- validator / fixtures；
- 维护这些对象的改进机制。

它不代表基础模型权重发生变化。

## 1. 声明级别

| 级别 | 实际变化 | 最低证据 |
|---|---|---|
| L0 当前任务纠错 | 当前 DRS / reference / schema 被修正 | 原失败 + 修复 + 真实读回/验收 |
| L1 可复用改进 | 新规则/guard 被后续任务实际采用并产生收益 | revision + 后续真实任务 + 与基线的可比结果/成本 |
| L2 有界递归改进 | “产生/筛选/验证改进的方法”本身改变，并参与下一轮改进 | 机制版本谱系 + 至少两个相连周期 + 稳定外部验收条件 |

以下都 **不能单独** 证明 L1/L2：
- 新增了 reference；
- 新增了 Gotcha；
- JSON Schema 通过；
- 模型自评“更准确”；
- 同一个调试样本修好了；
- changelog 写了“improved”。

## 2. 三层循环

```text
真实设计失败
→ L0 修当前问题
→ 提取可复用候选
→ 固定 baseline / candidate / evaluator
→ 后续真实任务采用
→ 有收益：L1
→ 检查“我们如何选择/验证改进”
→ 修改该机制
→ 新机制参与下一轮候选产生/筛选
→ 外部条件比较
→ 证据足够才可能 L2
```

## 3. 实验前固定契约

一次实验只验证一个主要假设。

至少固定：

### 目标
例如：
“增加 provenance reconciliation gate 能减少 Human/Machine 对 observed/inferred 的冲突。”

### Baseline
- repository commit/revision；
- DRS spec version；
- 使用的 reference 集；
- 输入设计任务；
- 模型/工具条件（能记录时记录）。

### Candidate
- 改哪些文件；
- 不允许改哪些文件；
- 预期改变哪一个行为。

### Evaluation
- 主指标；
- 正常 positive cases；
- 已知 negative cases；
- 不允许退化的行为；
- 成本/上下文增长上限；
- evaluator/rubric 版本。

### Budget
- 允许多少候选；
- 允许多少轮；
- 何时停止。

### Rollback
- 已知稳定 revision；
- 如何恢复；
- 不能抹掉哪些失败证据。

## 4. 三类样本必须分开

### Discovery sample
暴露原问题，可用于设计 candidate。

### Regression sample
证明已知失败被拦截，并确认合法输入仍通过。

### Held-out / later real task
没有参与 candidate 调整，用来检查迁移。

一旦 held-out task 被拿来调规则，它就不再是 held-out。

## 5. 设计类任务如何比较

设计判断难以完全自动评分，因此应预先固定 rubric。

建议至少比较：

- Material classification accuracy
- Semantic object completeness
- Cross-view consistency
- Provenance correctness
- Constraint completeness
- Attention evidence quality
- Style token executability
- Hallucinated exactness count
- Semantic-reference integrity
- Downstream reconstruction usability
- Context/token cost

不要只比较“看起来更像”。

## 6. 候选生成与验收分离

提出改动的模型可以参与自评，但自评不能成为唯一验收。

优先证据：
- 用户纠正；
- downstream renderer/consumer 反馈；
- deterministic validator；
- frozen rubric；
- later-task result；
- 人类可复核对比。

如果 evaluator 本身也修改：
1. 保留旧 evaluator；
2. 固定样本；
3. 新旧 evaluator 并行；
4. 单独记录 calibration；
5. 不允许用新 evaluator 的高分回填旧结论。

## 7. 晋升 / 停止 / 回滚

### 晋升
只有达到预定收益、成本不过线、不变量通过，才将 candidate 晋升为默认规则。

### 证据不足
保留为 experiment/candidate，不写成 canonical rule。

### 无收益或回归
拒绝或回滚 candidate，保留失败记录。

### 越界
如果为了证明改进而：
- 修改成功标准；
- 删除失败 fixture；
- 降低 validator；
- 改权限；
- 忽略成本；

立即停止本轮。

## 8. L2 递归验收

声明 L2 前必须回答：

1. 哪个 improvement mechanism 被修改？
2. old revision → new revision 是什么？
3. 新机制是否真的参与了下一轮候选产生/筛选/验证？
4. 下一轮候选是否在未参与调优的任务上被验证？
5. 同预算下，新机制是否产生更多有效改进、降低成本、减少漏检或错误晋升？
6. 哪些结果反对假设？
7. 什么条件下退役该机制？

任一关键证据缺失时，只能写：

> recursive-improvement candidate; not yet validated.

## 9. 默认停止条件

没有另行约定时：
- 一次机制实验最多比较两个候选；
- 连续两个候选无收益则停止；
- 不允许无限 self-loop；
- 不允许后台持续自改写；
- 不允许未经维护者授权自动写仓库。

## 10. 与其他 reference 的关系

- `evolution-loop.md`：决定经验落在哪里。
- `Gotchas.md`：重复失败记忆。
- `review-checklists/drs-output-review.md`：人类/模型验收门。
- `improvement-record-template.md`：记录对比证据。
- `changelog.md`：记录真正落地的变化，不负责证明收益。

## 一句话原则

> 让改进后的机制真正参与下一次改进，再用稳定的外部条件判断它是否确实做得更好。
