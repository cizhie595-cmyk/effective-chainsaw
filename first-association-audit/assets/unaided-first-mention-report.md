# 无提示首答报告

- Study mode：`design / analyze / compare`
- Study ID：
- 报告日期：

## 研究问题

- Subject：
- Population：
- Scenario：
- 研究问题：

## 调查实施

| 项目 | 记录 |
|---|---|
| Sampling frame | |
| Recruitment | |
| Collection mode | |
| Field dates | |
| Planned stopping rule | |
| Actual stop at | |
| Actual stop `n_collected / n_eligible` | |
| Actual stop reason | |
| Stopping compliance `compliant / deviated / unknown` | |
| Exact prompt wording | |
| Eligibility rule | |
| Exclusion rule | |

## 数据有效性

- 是否开放式：
- 是否无候选提示：
- 邀请、发件身份、链接预览和表单首页是否无目标提示：
- 是否保留逐条原始首答：
- 是否说明样本来源：
- 是否存在事后排除：
- 实际停止记录是否完整并遵守预设规则：
- 当前数据能回答什么：
- 当前数据不能回答什么：

### 记录流转

`analyze` 模式填写；每条不合法记录只计入一个主排除原因。`compare` 模式改填下方两轮表。

| 状态或排除原因 | 数量 | `predefined / posthoc` | 说明 |
|---|---:|---|---|
| Collected | | | |
| Did not reach prompt | | | |
| Population ineligible | | | |
| Duplicate | | | |
| Prompt exposure | | | |
| Not raw first answer | | | |
| Other exclusion | | | |
| Eligible `n_eligible` | | | |

## 编码字典

- Coding specification version `coding_spec_version`：
- Mapping snapshot ID `mapping_snapshot_id`：

`analyze` 模式的 Scope 写 `single`。`compare` 模式中，两轮都出现且映射相同写 `both`，只在一轮出现写 `Wave 1 only` 或 `Wave 2 only`；同一原始答案映射不同时分别保存两行。

| Scope | Mapping snapshot ID | Raw answer | Canonical answer | Rule | Decision |
|---|---|---|---|---|---|
| | | | | | |

## 结果

`analyze` 模式填写。`design` 模式不填写结果；`compare` 模式改填下方两轮结果。

| Canonical answer | First mentions | Share of `n_eligible` |
|---|---:|---:|
| | | |

- Estimation status：`estimable / not_estimable`
- Eligible records `n_eligible`：
- Subject first mentions `x/n_eligible`：
- Optional substantive-answer denominator `n_substantive`：
- Optional `x/n_substantive`；分母为 0 时写 `not_estimable`：
- Unknown：
- Blank：
- Refusal：
- Ambiguous：
- Excluded：
- 可选 Wilson 95% 区间：
- Wilson 模型适用依据；不适用则写“不报告”：

## 两轮可比性

仅在 `compare` 模式填写。

| 项目 | Wave 1 | Wave 2 | 一致？ |
|---|---|---|---|
| Population | | | |
| Sampling frame | | | |
| Recruitment | | | |
| Collection mode | | | |
| Prompt wording | | | |
| Eligibility rule | | | |
| Exclusion rule | | | |
| Planned stopping design | | | 比较计数口径、目标数量或预设时长，不比较日历日期 |
| Actual stop at / counts / reason | | | 各自是否符合预设规则 |
| Stopping compliance | | | 两轮都必须为 `compliant` |
| Coding specification version | | | 必须相同 |
| Mapping snapshot ID | | | 可以不同，分别保存实际映射 |
| Overlapping raw-answer mappings | | | 必须一致；单轮新答案不影响可比性 |

### 两轮记录流转

每条不合法记录只计入一个主排除原因；同一原因同时含预设和事后排除时，在说明中分别写明数量。

| 状态或排除原因 | Wave 1 数量 | Wave 1 规则时点与说明 | Wave 2 数量 | Wave 2 规则时点与说明 |
|---|---:|---|---:|---|
| Collected | | | | |
| Did not reach prompt | | | | |
| Population ineligible | | | | |
| Duplicate | | | | |
| Prompt exposure | | | | |
| Not raw first answer | | | | |
| Other exclusion | | | | |
| Eligible `n_eligible` | | | | |

### 两轮结果

两轮分别保留完整答案分布，不用合并后的分母代替。仅当 Comparison status 为 `comparable` 时计算差值；`comparison_limited` 或 `not_estimable` 时，差值列统一写 `not_calculated`。

| Canonical answer | Wave 1 first mentions | Share of Wave 1 `n_eligible` | Wave 2 first mentions | Share of Wave 2 `n_eligible` | Share difference `Wave 2 - Wave 1` |
|---|---:|---:|---:|---:|---:|
| | | | | | |

| 指标 | Wave 1 | Wave 2 |
|---|---:|---:|
| Eligible `n_eligible` | | |
| Subject first mentions `x` | | |
| Subject share `x/n_eligible` | | |
| Unknown | | |
| Blank | | |
| Refusal | | |
| Ambiguous | | |
| Excluded | | |
| Estimation status | | |

- Comparison status：`comparable / comparison_limited / not_estimable`
- Difference calculation：`calculated / not_calculated`
- 样本内比例差值；未计算时写 `not_calculated`：
- 差值解释限制：

## 解释

- 样本内可以说明：
- 不能外推或归因：
- 测量限制：

## 后续测量建议

- 
