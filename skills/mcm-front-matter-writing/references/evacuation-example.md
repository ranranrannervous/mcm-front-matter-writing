# 疏散论文的写法对照

以下片段来自本次以 2025 HiMCM A、Team 16390 论文为依据的改写。用于说明语言密度和章节分工，不是原论文逐字摘录，也不代表这些假设、符号或场景适用于其他题目。用户最后确认的规范优先于先导课中的早期示例，例如假设最多四条、理由另起一行、Our Work 只留空图、符号表后无说明。

## 单段问题背景

During a fire or toxic gas leak, emergency responders must inspect rooms to confirm whether occupants have evacuated and assist those who remain inside. Differences in floor configurations, corridor layouts, and occupant distributions, together with smoke spread and communication limitations, complicate route planning and responder coordination. Poorly coordinated sweeps may leave rooms unchecked, duplicate inspections, or delay checks of high-risk areas and prolong the exposure of occupants and responders to hazardous conditions. A mathematical model is therefore needed to account for building geometry, changing hazards, and responder coordination. The model should evaluate inspection sequences, staffing levels, and completion times under full coverage and verification requirements to support sweep planning for different building types.

此段依次交代研究对象、实际困难、后果和建模目的，没有列算法或报告模拟结果。它的句数和词数不构成固定要求。

## 任务重述片段

**Task 2:** Develop a sweep model for two firefighters in a single-story office with six rooms and two exits at opposite ends. Incorporate the floor plan, movement rules, clearance verification, and smoke conditions to determine the sweep sequence and completion time.

任务保留了对象、必须考虑的条件与交付结果，没有提前写最短路算法、贪心调度或求得的完成时间。

## 四条假设的内容与格式

**Assumption 1: The floor plan is known, and routes remain accessible.**  
**Justification:** Floor plans supply routing inputs, and fixed connectivity permits schedule comparisons within an intact building.

**Assumption 2: Responders share the same baseline capabilities.**  
**Justification:** A common movement and inspection profile isolates the effects of task allocation and local hazards.

**Assumption 3: Each room inspection proceeds without interruption.**  
**Justification:** Complete inspections give each task a defined duration and an unambiguous clearance status.

**Assumption 4: Occupants do not delay responders in the baseline model.**  
**Justification:** This defines a low-congestion reference. The extended model accounts for occupant interference.

这些是论文模型的简化条件，不是应急行动规则或经过独立验证的安全建议。第四条明确限定基础模型，避免与后续考虑拥堵的扩展模型冲突。Markdown 显示行数不用于验证三行要求，最终以目标 LaTeX 版式为准。

## 符号选择

该示例保留了 $G(t)$、$V_R$、$N$、$d(e)$、$R_0(r)$、$S(p,t)$、$v_{\mathrm{eff}}(e,t)$、$W(e,t)$、$T_{\mathrm{sweep}}(r,t)$、$T_{\mathrm{total}}(j)$、$T_{\mathrm{makespan}}$ 和 $\mathrm{CV}$。

烟气浓度采用 $\mathrm{kg\,m^{-3}}$，速度采用 $\mathrm{m\,s^{-1}}$，时间及具有时间量纲的风险调整路径代价采用 $\mathrm{s}$。$\mathrm{CV}$ 为无量纲量，不能在未说明转换时把小数值当作百分数。不要把这十二个符号复制到使用其他模型的论文中。正文交付的表格后不附本参考中的解释。

## 两行以内的模型优缺点

以下六点是用户确认的压缩版；在本次目标 LaTeX 版式中已用段落行数检查确认每点含加粗标题不超过两行。更换模板仍须重新核查。

### Strengths

1. **Hazard-dependent routing.** Smoke and fatigue modify travel costs, linking route selection to changing local conditions.
2. **Explicit verification.** Separate clearance states and checks by a second responder make high-risk verification traceable.
3. **Multiple building layouts.** A common framework handles stair travel and room risks in the tested one-, three-, and five-floor buildings.

### Weaknesses

1. **Simplified behavior.** Omitted hesitation and route choice can bias congestion estimates; calibrated agent-based simulations could address this.
2. **Fixed connectivity.** Route closures can invalidate schedules; updating the graph and recalculating assignments would address this limitation.
3. **Workload imbalance.** The three-floor CV is 24.5%, above the 15% target; assignment rules need to enforce the balance constraint.

条目保留具体机制或证据，不重复整段建模过程。缺点中的改进是建议，不代表已实现；三层情景的 24.5% 与 15% 只属于该论文，不能迁移为其他论文的结果。
