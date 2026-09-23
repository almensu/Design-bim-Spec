# 更新日志

本文档记录 Design-bim-Spec 的重要变更。

英文版 `CHANGELOG.md` 是事实来源；本文件是简体中文镜像。

仓库发布版本与 DRS 的 `spec_version` 是两条独立版本轴。Schema 使用 `0.1.0`，不代表仓库已经发布 `v0.1.0`。

## [未发布]

### 新增
- 建立“薄 `SKILL.md`、厚 `references/`”的多模态设计复刻规范架构。
- 新增 DRS JSON Schema、设计物料 taxonomy、视觉分析协议、布局约束、视觉注意力模型、Style Tokens、输出契约，以及 Human/Machine 示例。
- 参考 `yanghoo-reference` 新增仓库学习基础设施：Gotchas 踩坑记忆、Evolution Loop、有限递归自我改进协议、改进记录模板、DRS 输出审查清单和首轮递归改进基线记录。
- 新增双语 changelog 维护规则，要求重要变更来源于真实证据，而不是愿望式记录。

### 调整
- 正常 DRS 运行在验收前会读取相关 Gotcha，并执行 DRS 输出审查。
- 将“正常生成规范”和“维护 Skill 自身”严格分开：普通运行仍然在 Human View + Machine View 后 STOP；只有显式维护任务才允许修改仓库。
- 加入生命周期与证据要求，避免把“改了文档”直接等同于“已经证明变好了”。

### 修复
- 将详细规则从 `SKILL.md` 下沉到专门 reference，避免主 Skill 再次膨胀成说明书。
