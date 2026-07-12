# 无提示首答调查协议

## 1. 建立研究记录

在发出第一份问卷前固定：

```text
study_id:
subject:
subject_aliases:
population:
scenario:
sampling_frame:
recruitment:
collection_mode:
prompt_wording:
field_start:
field_end:
stopping_rule:
eligibility_rule:
exclusion_rule:
planned_comparison:
```

`subject_aliases` 只用于事后编码，不能显示给参与者。

停止收集后追加：

```text
actual_stop_at:
actual_stop_n_collected:
actual_stop_n_eligible:
actual_stop_reason:
stopping_compliance: compliant / deviated / unknown
```

`stopping_compliance` 根据预设规则与实际停止记录判断。材料不足时写 `unknown`，不能默认写 `compliant`。

## 2. 问题检查清单

- 是否只描述一个任务或场景？
- 是否没有出现目标对象及别名？
- 是否没有列出回答选项？
- 是否没有使用“是不是、应该、最好、专业”等推动性措辞？
- 是否允许“不知道”？
- 是否在任何品牌、账号或评价提示之前出现？
- 邀请文案、发件身份、链接预览、表单标题和引导语是否都没有暴露目标对象？
- 目标人群是否能不看说明就理解问题？

任一项不满足，先修改问题再收集数据。

## 3. 招募记录

明确参与者从哪里来：

- 现有粉丝或客户。
- 平台公开招募的自愿参与者。
- 第三方样本服务。
- 组织内部名单。
- 其他可说明的抽样框。

不要把便利样本写成随机样本。现有粉丝和客户通常比陌生人更熟悉研究对象，结果只能描述该样本。

从现有粉丝或客户中抽样不等于可以由目标账号直接发出邀请。若发件身份、邀请文案或表单首页在首答前显示了目标对象，该记录属于 `prompt_exposure`，不能作为无提示首答。

收集前写明 `stopping_rule`，例如固定结束日期或固定目标记录数；使用记录数时同时写明按 `n_collected` 还是 `n_eligible` 计数。停止时记录实际时间、数量和原因。不能因为当前结果有利或不利而提前停止、继续加样本或更换计数口径。

## 4. 原始回答格式

```csv
response_id,population_eligible,reached_prompt,duplicate_status,prompt_exposure,raw_answer_status,collection_mode,submitted_at,response_outcome,raw_first_answer,analysis_status,primary_exclusion_reason,exclusion_timing
R001,true,true,unique,unexposed,verbatim,online,2026-07-11T09:00:00+08:00,answered,原样回答,eligible,,
```

`response_outcome` 使用 `answered`、`unknown`、`blank`、`refusal` 或 `not_reached`。`not_reached` 仅用于 `reached_prompt=false`；其余四种状态仅用于已经到达问题的记录。拒答保留为合法调查结果，不编造成空白、不知道或未到达。

`analysis_status` 使用 `eligible` 或 `excluded`。`exclusion_timing` 仅在排除时填写：排除规则在查看回答前已经存在写 `predefined`，查看回答后才增加写 `posthoc`。`ambiguous` 是对 `answered` 首答的事后编码，不是 `response_outcome`。

不收集分析不需要的姓名、电话或参与者账号 ID。必须收集联系方式时，将身份表与回答表分开保存，公开输出只使用不可识别的 `response_id`。

## 5. 数据有效性

以下记录不进入无提示首答计算：

- 参与者不符合预先定义的人群。
- 参与者没有到达无提示问题；看到问题后明确拒答的记录属于 `refusal`，仍进入主分母。
- 邀请、发件身份、链接预览、表单首页或问题页在首答前展示了目标名称或候选列表。
- 同一参与者的重复提交无法可靠区分。
- 回答不是首答，而是研究者修改后的总结。

为每轮保存可核对的记录流转：

```text
n_collected:
n_not_reached:
n_excluded_population:
n_excluded_duplicate:
n_excluded_prompt_exposure:
n_excluded_not_raw_first_answer:
n_excluded_other:
n_eligible:
```

`n_eligible` 只包含符合人群定义、到达该题、满足唯一性、未受候选提示污染且保留未改写首答的记录。存在多个问题时，每条不合法记录按 `exclusion_rule` 中预先固定的优先顺序只分配一个 `primary_exclusion_reason`；其他问题放在说明中，不能重复计数。`n_excluded_other` 只接收有记录的技术或数据完整性问题，不能用来排除不利答案。所有排除都保留原记录、原因以及 `predefined` 或 `posthoc` 标记，并满足：

```text
n_collected = n_not_reached
            + n_excluded_population
            + n_excluded_duplicate
            + n_excluded_prompt_exposure
            + n_excluded_not_raw_first_answer
            + n_excluded_other
            + n_eligible
```

不要因为答案不利而删除。

## 6. 两轮测量

若计划前后比较，在第一轮开始前保存问卷截图或导出文件。第二轮复制同一问题原文、顺序、招募路径、收集方式、停止规则的计数口径与目标数量或预设时长，以及有效规则，并分别保存两轮实际停止记录与遵守状态。两轮日历日期不必相同；按固定时长收集时，实际记录数也不要求相同。

发生任何变化时记录：

```text
changed_field:
wave_1_value:
wave_2_value:
reason:
expected_effect:
```

变化不代表数据无用，但会限制两轮差异的解释。
