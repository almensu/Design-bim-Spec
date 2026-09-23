# Gotchas

## 1. 目的

这份文件记录 Design-bim-Spec 中 **高复发、高代价、低显眼度** 的失败模式。

它不是：
- changelog；
- 情绪记录；
- 普通任务流水账；
- 所有错误的垃圾桶。

它是：
- 多模态设计复刻最容易重复踩的坑；
- Human View / Machine View 漂移的失败记忆；
- 后续 checklist、schema、validator、fixture 的来源。

一句话：

> Gotchas 不是记录“某次做错了什么”，而是记录“这个系统最容易以什么方式再次做错”。

## 2. 快速路由

| 当前任务 | 优先阅读 |
|---|---|
| 修改 Skill / reference 架构 | G-001、G-007、G-009 |
| 分析布局、bbox、父子关系 | G-002 |
| 处理观察与推断 | G-003、G-006 |
| 建立视觉动线 | G-004 |
| 提取风格 | G-005、G-006 |
| 输出 Human + Machine Spec | G-003、G-008、G-009 |
| 从失败中改进 Skill | G-010 |

不需要每次通读整份文件；按任务读取相关条目。

## 3. 什么问题值得进入 Gotchas

满足任一条件即可考虑：
- 已经重复；
- 第一次出现但代价高；
- AI 明显容易自然重犯；
- 很难从表面发现；
- 能进一步固化成 checklist / schema / validator / regression fixture。

一条高价值 Gotcha 必须回答：

```text
失败长什么样？
→ 为什么模型自然会这么做？
→ 哪一层本应拦住？
→ 如何让下一次更难再次发生？
```

高代价失败应尽量先保留：
- 原始输入；
- 错误 Human View；
- 错误 Machine View；
- 当时使用的 Skill/reference revision；
- 用户纠正；
- 可复现的最小 negative fixture。

不要先覆盖唯一失败证据，再宣称“已经修好”。

## 4. 生命周期

- `active`：已识别，仍主要依赖规则/审查。
- `guarded`：已有稳定 validator、schema gate 或强制 review，但保留条目解释机制。
- `retired`：架构与后续真实任务证据表明该失败在预期路径中已不可达。

加了 checklist 并不等于可以立刻 retired。

---

## G-001 把 SKILL.md 写成完整说明书

### 现象
所有 taxonomy、bbox、anchor、attention、style、schema 细则不断塞回 `SKILL.md`，主入口越来越长。

### 为什么容易踩
模型倾向把“重要规则”全部放在入口，短期看起来完整，长期却导致上下文膨胀、重复定义和 reference 失去意义。

### 错误信号
- `SKILL.md` 开始重复 reference 的字段定义；
- 修改一条规则要同时改多个地方；
- 主 Skill 比任一 reference 都长；
- 用户再次要求“细则下沉”。

### 错误写法
```text
SKILL.md
  taxonomy
  bbox schema
  constraints vocabulary
  attention theory
  typography tokens
  examples
  ...
```

### 正确做法
```text
SKILL.md = router + sequence + boundary
references/* = domain details
```

### 防复发挂载点
- 类型：architecture rule / review
- 落点：`AGENTS.md`, `references/reference-index.md`
- 动作：只有 orchestration 行为变化才修改主 Skill；字段细则默认进入 focused reference。

### 责任层
repository architecture / routing

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

---

## G-002 只记录 bbox，把“为什么在那里”丢掉

### 现象
Machine View 给每个元素精确坐标，却没有 parent、anchor、constraint；换比例后设计立即散架。

### 为什么容易踩
视觉模型天然擅长检测“在哪里”，容易把设计复刻误解成 object detection。

### 错误信号
- 大量 bbox，没有 anchors；
- promo badge 与 product 没有依赖；
- CTA 只有绝对坐标；
- 1:1 改 9:16 后只能整体缩放。

### 错误写法
```json
{"id":"conversion.badge","bbox":{"x":0.72,"y":0.18,"w":0.16,"h":0.08}}
```

### 正确做法
bbox + semantic parent + anchor + constraint：

```text
conversion.badge.center
→ product.main.top_right
offset = normalized vector
```

### 防复发挂载点
- 类型：reference / checklist
- 落点：`layout-constraints.md`, `review-checklists/drs-output-review.md`
- 动作：对关键依赖元素检查“位置 + 原因”是否同时存在。

### 责任层
geometry / topology

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

---

## G-003 observed / inferred / proposed 被混成一种真相

### 现象
参考图里看不清的内容、模型猜测、规划建议都以确定事实写进 DRS。

### 为什么容易踩
结构化 JSON 看起来天然“确定”，模型容易把合理推断写成 observed。

### 错误信号
- design_planning 中大量 `source: observed`；
- 看不清的字号/颜色/文本却 confidence 很高；
- Human View 说“推测”，Machine View 却写成已观察事实。

### 错误写法
```json
{"text":"限时立减300元","source":"observed","confidence":0.99}
```
但原图小字根本不可读。

### 正确做法
严格区分：
- `observed`
- `inferred`
- `proposed`

并降低 confidence、进入 `needs_review`。

### 防复发挂载点
- 类型：schema semantics / checklist
- 落点：`canonical-schema.md`, `visual-analysis-protocol.md`, `review-checklists/drs-output-review.md`

### 责任层
provenance / epistemic state

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

---

## G-004 把眼动路径硬编码成“产品 → 标题 → CTA”

### 现象
无论输入是什么海报/DM/电商图，attention graph 都套同一条模板。

### 为什么容易踩
这是常见营销设计范式，模型容易把经验当成视觉证据。

### 错误信号
- 明明价格最大，仍把产品排第一；
- 没有 CTA 的设计被强行制造 CTA；
- fixation 顺序与尺寸、对比、位置完全不符。

### 正确做法
attention graph 必须从 scale、contrast、isolation、centrality、type scale、directional cue 等证据推导。

### 防复发挂载点
- 类型：reference / review
- 落点：`attention-model.md`, `review-checklists/drs-output-review.md`

### 责任层
attention inference

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

---

## G-005 用“高级、现代、科技感”代替 Style Tokens

### 现象
风格分析充满形容词，却没有可执行的色彩、字号比例、间距、阴影、圆角、光照参数。

### 为什么容易踩
语言模型很容易生成审美描述，但下游 renderer 无法稳定复现抽象形容词。

### 错误信号
- style_tokens 只有 mood；
- headline 没有 relative size/weight；
- “科技蓝”没有可验证 palette；
- 阴影只写 “soft shadow”。

### 正确做法
形容词只能做 summary；核心必须尽量参数化。

### 防复发挂载点
- 类型：reference / checklist
- 落点：`style-tokens.md`, `review-checklists/drs-output-review.md`

### 责任层
style representation

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

---

## G-006 看不清的文字、字体和颜色被“补全”

### 现象
低分辨率参考图中不可读的文案、未知字体或微妙颜色被模型自信填成具体值。

### 为什么容易踩
生成模型倾向输出完整答案，而不是保留空缺。

### 错误信号
- OCR 证据不足却给出完整促销句；
- 未知字体直接指定品牌字体；
- 色偏/压缩严重却给出高精度 HEX。

### 正确做法
使用 semantic placeholder、估计值、confidence 与 `needs_review`；不要伪造精确性。

### 防复发挂载点
- 类型：visual protocol / checklist
- 落点：`visual-analysis-protocol.md`, `style-tokens.md`

### 责任层
evidence handling

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

---

## G-007 Renderer 细节反向污染 canonical DRS

### 现象
为了方便某一个 ComfyUI、Figma、HTML 或图片模型，把 renderer-specific 字段写成 DRS 必填核心。

### 为什么容易踩
“马上能执行”会诱导规范围绕第一个 renderer 设计，最终失去通用中间表示能力。

### 错误信号
- canonical schema 出现某模型专属 sampler/node；
- Figma node ID 成为语义身份；
- CSS class 被当作核心 layout relation；
- 换 renderer 就必须改 DRS。

### 正确做法
DRS 只表达设计语义；renderer adapter 负责翻译。

### 防复发挂载点
- 类型：architecture invariant
- 落点：`AGENTS.md`, `canonical-schema.md`

### 责任层
canonical IR / downstream adapter boundary

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

---

## G-008 Human View 与 Machine View 各说各话

### 现象
人类说明写“标题第一视点”，JSON attention graph 却写 product rank=1；或 prose 说元素右上依附，Machine View 没有对应 anchor。

### 为什么容易踩
两个输出常被模型分别生成，后生成的一份会发生语义漂移。

### 错误信号
- fixation rank 不一致；
- layer stack 与 layer_depth 不一致；
- Human View 提到的 group 在 JSON 中不存在；
- JSON 标记 `needs_review`，人类说明却声称确定。

### 正确做法
把 Human/Machine 当作同一内部模型的两个 view，最后做 cross-view reconciliation。

### 防复发挂载点
- 类型：output contract / checklist
- 落点：`output-contract.md`, `review-checklists/drs-output-review.md`

### 责任层
serialization / presentation

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

---

## G-009 JSON Schema 通过，被误当成“设计语义有效”

### 现象
Machine View 能通过 JSON Schema，但 scene graph、anchor、constraint、attention target 引用了不存在的 element/group，或逻辑互相冲突。

### 为什么容易踩
JSON Schema 很擅长结构和类型，但跨节点引用完整性通常需要额外语义验证。

### 错误信号
- `from.element` 不存在；
- scene graph child 没有对应 node/element；
- constraint subjects 不存在；
- layer_depth 与 occlusion 相反；
- terminal_action 指向未知 ID。

### 正确做法
区分：
```text
schema validity != semantic integrity
```

当前至少通过 review checklist 检查；重复出现后应升级成专门 validator + negative fixtures。

### 防复发挂载点
- 类型：checklist → future validator
- 落点：`review-checklists/drs-output-review.md`
- 后续候选：`scripts/validate-drs-references.py`

### 责任层
semantic validation

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

---

## G-010 修复前覆盖掉唯一失败样本

### 现象
用户指出 DRS 复刻失败后，直接改 prompt/reference 和输出，把原失败结果删除，后面只能凭记忆说“已经改进”。

### 为什么容易踩
清理错误产物很自然，但递归改进需要可比较的 baseline 和 negative evidence。

### 错误信号
- 只有修复后的样例；
- 找不到旧 Skill revision；
- 不能重放原始输入；
- “效果更好”只有主观回忆。

### 正确做法
高代价失败先保存最小证据，再修：
```text
input + baseline revision + bad output + user correction
→ candidate change
→ comparable rerun
```

### 防复发挂载点
- 类型：evolution protocol
- 落点：`evolution-loop.md`, `recursive-self-improvement-protocol.md`, `improvement-record-template.md`

### 责任层
evaluation / learning memory

### 状态
- 状态：active
- 首次记录：2026-09-23
- 最近确认：2026-09-23

## 一句话总纲

> 好的 Gotcha 不是让模型“以后小心”，而是逐步把失败下沉成下一次必经的约束、审查或验证。
