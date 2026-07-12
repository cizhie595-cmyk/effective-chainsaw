# 回答编码与分析规则

## 编码顺序

1. 锁定原始回答文件并保留副本。
2. 汇总所有不同原始答案，并保留它们与原记录的对应关系。
3. 建立 `raw_answer -> canonical_answer` 字典。
4. 对合法记录标记 `include`、`ambiguous`、`unknown`、`blank` 或 `refusal`。
5. 记录 `coding_spec_version`，为冻结的实际映射表生成 `mapping_snapshot_id` 后计算结果。
6. 修改任何映射时生成新快照并重算，不覆盖旧结果；修改合并、别名或模糊回答规则时同时升级规范版本。

## 合并规则

可以合并：

- 大小写、全半角和明显拼写差异。
- 可公开核验的官方简称。
- 研究开始前已经登记的别名。

不得合并：

- 只属于同一类别但不是同一对象的答案。
- 研究者认为“意思差不多”的模糊描述。
- 同时提到多个对象且无法确定第一项的回答。

## 基本统计

设：

- `n_collected`：研究数据中收到的全部记录数量。
- `n_eligible`：符合人群定义、到达该题、满足唯一性、未提前看到目标或候选提示，并保留未改写首答的记录数量。目标答案、其他答案、`unknown`、空白、拒答和 `ambiguous` 都计入。
- `n_substantive`：可选的次级分母，只包含能够编码到具体对象的实质答案；必须与主分母分开报告。
- `x`：目标对象被首先提及的数量。
- `p = x / n_eligible`：仅在 `n_eligible > 0` 时定义的样本内主第一提及比例。

先按原因报告未到达与排除记录，并标记规则是 `predefined` 还是 `posthoc`。每条不合法记录只计入一个主排除原因，所有类别之和必须与 `n_collected` 和 `n_eligible` 对账。事后发现的数据问题只有在破坏人群资格、唯一性、无提示条件或原始首答完整性时才能排除，不能按答案方向筛选。

当 `n_eligible > 0` 时，必须同时报告 `x/n_eligible` 和百分比。样本很小时，以人数和原始分布为主，不单独展示百分比制造精确感。如果报告 `x/n_substantive`，必须明确它排除了哪些回答，且不能用它替换主比例；`n_substantive = 0` 时不计算该次级比例。

当 `n_eligible = 0` 时，将估计状态标为 `not_estimable`，不计算 `p`、百分比或区间；只报告记录流转和无法估计的原因。

只有 `n_eligible > 0`、抽样与观测条件支持独立二项模型且 `stopping_compliance = compliant` 时，才可选报告 95% Wilson 区间：

```text
center = (p + z^2 / (2n_eligible)) / (1 + z^2 / n_eligible)
margin = z * sqrt(p(1-p)/n_eligible + z^2/(4n_eligible^2)) / (1 + z^2/n_eligible)
z = 1.96
interval = center +/- margin
```

`stopping_compliance` 为 `deviated / unknown` 时绝不使用上面的简单 Wilson 公式；需要序贯或其他停止调整时，属于本 Skill 之外的另行分析。停止合规但样本为便利、自愿报名或其他非概率样本时默认不报告该区间；若另有明确的独立二项模型依据，只能把区间标为模型条件下的描述，并说明它不能修复样本选择偏差或总体外推问题。

存在权重、分层、整群、配对或重复观测时，不使用上面的简单 Wilson 公式替代与设计相符的分析；仍可单独报告未加权人数和原始分布。

## 必报分布

- 目标对象第一提及。
- 其他每个主要答案。
- `unknown`。
- `blank`。
- `refusal`。
- `ambiguous`。
- 未到达与被排除记录的数量、原因及 `predefined / posthoc` 标记。
- 预设停止规则、实际停止时间与数量、停止原因和 `stopping_compliance`。

只报告目标对象比例会隐藏竞争答案和数据质量。

## 两轮比较

先制作可比性表：

| 项目 | Wave 1 | Wave 2 | 一致？ |
|---|---|---|---|
| population | | | |
| sampling_frame | | | |
| recruitment | | | |
| collection_mode | | | |
| prompt_wording | | | |
| eligibility_rule | | | |
| exclusion_rule | | | |
| stopping_rule design | | | 比较计数口径、目标数量或预设时长，不比较日历日期 |
| actual_stop | | | 各自是否符合预设规则 |
| stopping_compliance | | | 两轮都必须为 `compliant` |
| coding_spec_version | | | 必须相同 |
| mapping_snapshot_id | | | 可以不同，分别保存实际映射 |
| overlapping raw-answer mappings | | | 同一原始答案在两轮的映射必须一致 |

只在一轮出现的新原始答案不构成编码方法变化。按以下顺序确定状态：任一轮 `n_eligible = 0` 时标记 `not_estimable`；否则，关键项存在变化、任一轮 `stopping_compliance` 不是 `compliant`、`coding_spec_version` 不同，或两轮重叠原始答案映射不一致时标记 `comparison_limited`；否则标记 `comparable`。只有 `comparable` 才计算样本内比例差值；前两种状态只并列报告各轮可用结果，差值写为 `not_calculated`。

除非研究设计包含适当对照、随机化或其他因果识别方法，不把两轮差异归因于某次内容、活动或账号动作。

## 解释用语

推荐：

- “在本次样本的 `n_eligible` 条合法记录中，`x` 条首先提到目标对象；主比例包含不知道、空白、拒答和模糊回答。”
- “这批参与者来自现有粉丝招募，结果不代表全部目标人群。”
- “两轮问题措辞不同，因此只能并列描述。”

避免：

- “所有用户都会首先想到……”
- “已经证明全市场……”
- “搜索第一，所以用户第一反应也是……”
- “比例上升完全由某次传播动作造成。”
