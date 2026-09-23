# Evolution Loop

这份文档定义 Design-bim-Spec 如何从真实设计任务中学习，同时避免两个极端：

- 规则永远不变，反复踩同一个坑；
- 每次用户纠正都立刻加一条永久总规则，导致 reference 无限膨胀。

## 核心循环

```text
真实 DRS 任务证据
→ local note / improvement record
→ Gotcha
→ review checklist
→ schema / validator / regression fixture
→ SKILL / README routing（必要时）
→ 后续真实任务采用并与基线比较
→ guarded / retired / split
```

不是每条反馈都必须走完整链路。

## 正常运行与维护运行必须分开

### 正常 DRS 运行
目标：
```text
reference/brief → Human View + Machine View → STOP
```

普通运行不得因为“发现了一个可以优化 Skill 的点”就自动修改仓库。

### Skill 维护运行
只有用户/维护者明确要求改进 Design-bim-Spec 时，才允许：
- 修改 references；
- 修改 schema；
- 修改 examples；
- 更新 Gotchas；
- 更新 changelog；
- 创建 validator / regression fixture。

## Stage 1 — Task Evidence

可用证据包括：
- 用户明确指出复刻错误；
- Human/Machine 不一致；
- Machine View 无法被下游稳定消费；
- schema/validator failure；
- 某一失败在多个设计物料中重复；
- 某个成功结构在不同任务中稳定复用。

证据要具体，不把“感觉一般”直接升级成规则。

高代价或语义细微的失败，修复前优先保存：
- 输入图/brief 的稳定引用或摘要；
- baseline Skill/reference revision；
- 原 Human View；
- 原 Machine View；
- 用户纠正；
- 最小可复现 negative fixture。

## Stage 2 — Local Improvement Record

一次性但有价值的反馈先进入 improvement record。

回答：
- 发生了什么？
- 在什么条件下发生？
- 预期是什么？
- 实际是什么？
- 哪个 revision 产生？
- 下一次什么现象说明它又出现了？

模板：
`improvement-record-template.md`

## Stage 3 — Gotcha

以下情况进入 `Gotchas.md`：
- 第二次出现；
- 第一次但代价高；
- AI 极易自然重犯；
- 不容易从表面识别。

Gotcha 必须给出“防复发挂载点”，不能只写“以后注意”。

## Stage 4 — Review Checklist

当问题需要视觉/语义判断、难以完全机械化时，进入：

`review-checklists/drs-output-review.md`

典型：
- attention path 是否真正来自视觉证据；
- style 是否参数化充分；
- Human/Machine 是否一致；
- inference 是否过度。

## Stage 5 — Schema / Validator / Regression Fixture

当信号足够确定时，优先机械化。

适合 schema：
- 类型；
- enum；
- 必填结构；
- numeric range。

适合 semantic validator：
- ID 引用完整性；
- scene graph 无悬空节点；
- constraint subjects 存在；
- terminal action 存在；
- anchor endpoint 存在。

适合 regression fixture：
- 一个真实失败 Machine View；
- 一个合法 positive control。

验证器把合法输入全部拒绝，不算 hardening 成功。

## Stage 6 — Entrypoint Routing

只有当规则改变“模型开始任务时必须知道什么”，才更新：
- `SKILL.md`
- `AGENTS.md`
- `README.md`
- `reference-index.md`

入口只负责路由，不重新复制规则正文。

## Stage 7 — Later-task Verification

持久化 ≠ 已证明有效。

一次规则/检查器修改只有进入后续真实任务并改善结果，才能声明可复用收益。

至少记录：
- baseline revision；
- candidate revision；
- 未参与调参的后续任务；
- 相同或可比输入条件；
- 成功/失败；
- 成本；
- 是否出现新回归。

失败和 inconclusive 结果同样要保留。

## Stage 8 — Lifecycle

- `active`：仍靠规则/人工判断。
- `guarded`：有稳定 gate/validator，但仍保留解释与回归上下文。
- `retired`：架构 + 后续任务证据表明预期流程已无法再触发。

## Promotion Matrix

| 信号 | 首次落点 | 升级条件 |
|---|---|---|
| 一次性观察 | improvement record | 重复或高代价 |
| 隐蔽重复失败 | Gotcha | 需要审查/自动化 |
| 依赖设计判断 | checklist | 信号变得可机械判断 |
| 确定性错误 | schema / validator | 应阻断验收 |
| 启动行为变化 | entrypoint routing | 每个运行都必须知道 |
| 成熟通用原则 | focused reference | 后续任务证明确有迁移价值 |

## 每次维护任务结束后的 12 个问题

1. 这次是否有用户可见失败？
2. 是否已经有 Gotcha，却仍没提前拦住？
3. 失败属于 geometry、topology、provenance、attention、style、serialization 还是 routing？
4. 是一次性问题，还是高复发模式？
5. 能否保留一个 negative fixture？
6. 需要 Gotcha、checklist、schema 还是 validator？
7. 是否真的需要修改 `SKILL.md`，还是应该继续下沉？
8. Human/Machine 是否产生新的不一致风险？
9. 是否让 renderer 特性污染了 canonical DRS？
10. 是否把 candidate/inference 错当成 canonical truth？
11. CHANGELOG 是否需要记录实际已落地变化？
12. 这次只能声明 L0，还是已有后续证据支持 L1/L2？

## 验收规则

完成一次“学习复盘”只意味着找到了合理落点。

它不自动证明系统变好。

要声明收益，进入：
`recursive-self-improvement-protocol.md`

## Review the loop itself

如果反复出现：
- Gotcha 写了却没人读；
- checklist 很长却没有拦截价值；
- validator 误报太多；
- 每次都新增规则；
- 复盘成本大于收益；

说明需要改进的对象已经不是某一条设计规则，而是 **evolution loop 本身**。

这时使用 bounded recursive self-improvement protocol，不允许靠“再写一篇流程文档”自证成功。

## 一句话原则

> 从每次有价值的扰动中学习，但只把值得约束下一次任务的经验硬化下来。
