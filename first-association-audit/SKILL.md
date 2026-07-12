---
name: first-association-audit
description: |
  第一联想体检。使用开放式、无提示的调查问题，测量特定人群在一个明确场景下首先提到哪个账号、品牌、产品或办法。用于设计无提示首答调查、检查现有问卷是否含提示、编码原始回答、计算第一提及结果、比较两轮测量，以及判断搜索排名、点赞或提示性投票为什么不能替代无提示回答。用户提出“大家遇到这个问题会先想到谁”“我的账号是否被首先提到”“帮我测第一联想”“复核这份品牌回忆调查”等请求时使用。不生成账号定位、内容计划或传播话术。
---

# 第一联想体检

## 任务定义

本 Skill 测量一个观察结果：

> 面对同一个中性场景问题，受访者在没有看到候选名称、选项或图片时，最先提交的回答是什么；“不知道”、空白和拒答也作为结果保留。

它只测量已经收集到的回答，不推荐某个目标答案，也不根据主页、搜索结果或传播数字猜测答案。

## 公开方法依据

执行前读取：

- [public-foundations.md](references/public-foundations.md)：公开来源与本 Skill 采用的原则。
- [survey-protocol.md](references/survey-protocol.md)：问题设计、招募、数据记录和有效性检查。
- [analysis-rules.md](references/analysis-rules.md)：回答编码、统计、两轮比较和解释边界。
- [unaided-first-mention-report.md](assets/unaided-first-mention-report.md)：固定报告模板。

## 三种工作模式

| mode | 用户已有材料 | 交付 |
|---|---|---|
| `design` | 只有研究目标，尚未收集回答 | 可直接执行的调查方案 |
| `analyze` | 有逐条原始回答和调查记录 | 编码表与描述性结果 |
| `compare` | 有两轮原始回答和两轮调查记录 | 可比性检查与差异报告 |

先判断 mode，再补充该模式缺少的信息。不要为了显得完整而虚构参与者、回答、日期或结果。

## 最小研究合同

实际执行需要明确：

- `subject`：希望在回答中识别的账号、品牌、产品或办法及其常见别名。
- `population`：希望描述的具体人群。
- `scenario`：受访者面对的单一任务或选择场景。
- `sampling_frame`：受访者从哪里来，谁有机会被邀请。
- `recruitment`：如何邀请，是否为自愿报名或现有粉丝。
- `collection_mode`：在线表单、访谈、电话或其他收集方式。
- `prompt_wording`：受访者实际看到的完整问题。
- `field_dates`：开始和结束日期。
- `stopping_rule`：预先规定的结束日期、目标记录数或其他停止条件。
- `actual_stop`：实际停止时间、当时记录数和停止原因；在 `design` 模式保持未填写。
- `stopping_compliance`：实际停止是否遵守预设规则，使用 `compliant / deviated / unknown`。
- `raw_responses`：逐条、去标识化的原始首答。

只询问当前模式真正缺少的字段，不限制固定问数。缺少原始回答时只能进入 `design`，不能输出“大家会先想到谁”的结论。

## Step 1：写研究问题

研究问题使用以下结构：

> 在 `{population}` 中，当 `{scenario}` 时，受访者无提示写下的第一个答案分别是什么？其中 `{subject}` 被首先提到多少次？

`scenario` 必须只包含一个任务。把“想成长、想变好、需要帮助”等宽泛愿望改写成受访者能够判断是否发生过的具体情境。

## Step 2：设计无提示问题

默认问题：

> 当你需要 `{scenario 中的任务}` 时，你首先会想到哪个账号、品牌、产品或办法？请只写第一个想到的答案；没有答案可以写“不知道”。

根据对象类型调整“账号、品牌、产品或办法”，不要一次列出所有类别。问题必须：

- 开放式作答，不提供候选列表。
- 不出现 `subject`、别名、头像、截图、首字母或其他暗示。
- 邀请文案、发件身份、链接预览、表单标题和引导语在首答前都不暴露 `subject` 或别名。
- 一次只问一个概念。
- 使用目标人群能理解的普通词。
- 在任何提示性或评价性问题之前出现。

如果现有问题包含“是不是想到我”“你听过哪些以下品牌”或候选选项，只能描述为提示后识别或认同，不能当作无提示首答。

## Step 3：记录调查实施

建立以下记录，并在收集、停止和清理数据时持续更新：

```text
study_id
population
sampling_frame
recruitment
collection_mode
field_dates
stopping_rule
actual_stop_at
actual_stop_n_collected
actual_stop_n_eligible
actual_stop_reason
stopping_compliance
prompt_wording
eligibility_rule
exclusion_rule
response_id
population_eligible
reached_prompt
duplicate_status
prompt_exposure
raw_answer_status
response_outcome
raw_first_answer
analysis_status
primary_exclusion_reason
exclusion_timing
coding_spec_version
mapping_snapshot_id
```

公开报告不得包含姓名、手机号、参与者账号 ID、聊天记录或其他可识别个人的信息。参与者应知道回答将如何使用；涉及公开发布时，按适用的隐私规则处理。

## Step 4：检查数据是否可分析

具备以下信息才进入 `analyze`：

- 能逐条判断参与者是否符合 `population`、是否到达问题、是否重复以及是否受到目标提示。
- 对 `answered` 记录保留未改写的原始首答，对 `unknown`、`blank`、`refusal` 和 `not_reached` 分别保留结果状态，而不是只提供汇总数字。
- 能把提示暴露或其他不合法记录单独排除；进入 `n_eligible` 的记录在招募邀请、发件身份、表单首页和问题本身中均未提前看到 `subject` 或候选列表。
- 招募来源、收集方式和日期可说明。
- 排除规则在查看结果前已经确定；事后发现的数据质量问题必须逐条说明，且不能根据答案是否有利决定排除。
- 记录流转能够从 `n_collected` 对账到各类排除和 `n_eligible`。
- 计划停止规则、实际停止时间与数量、停止原因和 `stopping_compliance` 均有记录；缺失时标为 `unknown`，不能假定遵守。

以下材料不能替代原始回答：搜索排名、推荐流、粉丝数、点赞、播放、收藏、评论投票、主页介绍和作者自述。

不满足时，输出“当前数据不能回答研究问题”，并明确哪些数据仍可描述。例如，提示性投票可以报告认同率，但不能改名为无提示首答率。

## Step 5：编码原始回答

先完成记录资格判断，只对进入 `n_eligible` 的记录建立编码字典：

| scope | mapping_snapshot_id | raw_answer | canonical_answer | rule | decision |
|---|---|---|---|---|---|
| single / both / Wave 1 only / Wave 2 only | 快照编号 | 原样回答 | 统一名称 | 精确名称、公开简称或已声明别名 | include / ambiguous / unknown / blank / refusal |

规则：

- 只合并可证明指向同一对象的拼写、简称和别名。
- 模糊回答保留为 `ambiguous`，不强行分给目标对象。
- “不知道”、空白和拒答分别记录。
- `coding_spec_version` 标识合并、别名和模糊回答的统一规则；`mapping_snapshot_id` 标识一次冻结的实际映射表。修改映射后生成新快照并重算，修改统一规则时同时升级规范版本。
- 编码字典必须与结果一起保存。`compare` 模式中，两轮都出现且映射相同的原始答案标为 `both`，只在一轮出现的答案标为 `Wave 1 only` 或 `Wave 2 only`；同一原始答案在两轮映射不同时分别保存两行。
- 公开或高风险研究优先由第二名编码者独立复核分歧。
- 记录排除只在数据有效性阶段完成，不能根据首答内容在编码阶段排除。

## Step 6：计算结果

按 [analysis-rules.md](references/analysis-rules.md) 计算并报告：

- 记录流转：收集记录总数、未到达该题的记录、各类排除数量与原因，以及排除规则是预先规定还是事后发现。
- 合法记录总数 `n_eligible`：符合人群定义、到达该题、能够区分重复提交、未提前看到目标或候选提示，并保留了未改写首答的记录。目标答案、其他答案、`unknown`、空白、拒答和 `ambiguous` 都进入这个主分母。
- 每个统一答案的第一提及次数。
- `subject` 的第一提及次数 `x` 与主比例 `x / n_eligible`。
- “不知道”、空白、拒答和模糊回答的数量。
- 可选报告只含可编码实质答案的次级分母 `n_substantive`，但必须单独命名，不能替代主分母。
- 招募来源、收集方式和调查日期。

事后发现但确实破坏人群资格、唯一性、无提示条件或原始首答完整性的记录不进入 `n_eligible`；必须单列数量、原因和发现时间。不得因答案没有提到 `subject` 而排除记录。

如果 `n_eligible = 0`，结果状态写为 `not_estimable`，只报告记录流转与无法估计的原因，不计算比例或 Wilson 区间。

只有抽样与观测条件支持独立二项模型且 `stopping_compliance = compliant` 时才可选报告 Wilson 区间；便利、自愿报名、其他非概率样本或停止状态未知/偏离时默认不报告该区间。

先报告人数，再报告比例。便利样本、粉丝样本或自愿报名样本只能描述这批参与者，不能外推为所有目标用户。

本 Skill 不提供通用“通过线”。用户必须根据研究用途、样本设计和基线预先写明决策规则；没有预设规则时只报告结果，不宣布成功或失败。

## Step 7：比较两轮测量

进入 `compare` 前逐项核对：

- `population` 是否相同。
- `sampling_frame` 与 `recruitment` 是否相同。
- 收集方式是否相同。
- 问题原文和出现顺序是否相同。
- 有效与排除规则是否相同。
- `coding_spec_version` 是否相同，且两轮都出现的原始答案是否映射一致；只在一轮出现的新答案不构成编码方法变化。
- `stopping_rule` 的计数口径、目标记录数或预设收集时长是否相同；两轮日历日期不必相同。
- 两轮实际停止是否各自遵守预设规则；不要求固定日期规则下的实际记录数相同。

任何关键项变化时，只能做并列描述并标记 `comparison_limited`。不能把差异全部解释为账号、传播或时间导致，也不能用前后变化自动宣称因果。

只有所有关键项可比且两轮都可估计时才计算比例差值；`comparison_limited` 或 `not_estimable` 时差值写为 `not_calculated`。

## Step 8：输出

使用 [unaided-first-mention-report.md](assets/unaided-first-mention-report.md)。根据 mode 填写：

- `design`：研究合同、问题原文、招募与记录方案，不填写结果。
- `analyze`：数据质量、编码字典、人数与比例、解释限制。
- `compare`：两轮可比性表、两轮实际编码映射及其规范版本与快照编号、两轮分别的记录流转与答案分布、各轮 `x/n_eligible`、样本内差值及限制。

报告中的每个结论都必须能回到问题原文、样本说明和原始回答。未知项保持未知。

## 不做的事

- 不生成用户应该采用的身份、定位、口号或栏目。
- 不判断产品、价格、商业模式或内容质量。
- 不把平台搜索结果改写成受访者回答。
- 不把提示后认同、识别或选择改写成无提示首答。
- 不从非概率样本推断总体市场份额。
- 不在缺少对照或稳定测量条件时作因果结论。
- 不公开可识别个人的原始回答。
