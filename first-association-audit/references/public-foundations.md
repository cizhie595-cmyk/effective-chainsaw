# 公开方法依据

本文件只记录公开来源和本 Skill 从中采用的调查原则，不复制外部文章正文。

## SurveyMonkey：Aided vs. Unaided Brand Awareness

- 页面：<https://www.surveymonkey.com/learn/market-research/unaided-vs-aided-brand-awareness-survey-questions/>
- 页面标题：Aided vs. Unaided Brand Awareness: A Complete Guide
- 核对日期：2026-07-11

采用的原则：

- 无提示测量使用开放式问题，不向参与者展示候选名称。
- 提供候选名称的题目测量的是提示后识别，而不是无提示回忆。
- 回答中是否自然出现目标名称，是无提示测量的观察对象。

## AAPOR：Best Practices for Survey Research

- 机构：American Association for Public Opinion Research
- 页面：<https://aapor.org/standards-and-ethics/best-practices/>
- 页面标题：Best Practices for Survey Research
- 核对日期：2026-07-11

采用的原则：

- 问题应具体、一次只问一个概念，并使用目标人群能理解的简短语言。
- 避免会推动参与者作出特定回答的措辞。
- 开放式题允许参与者使用自己的词，但结果需要编码。
- 问题顺序会影响回答；一般问题应先于更具体的问题。
- 比较两个时间点时，应尽量保持问题措辞、收集方式和研究方法一致。
- 非概率样本需要谨慎解释，并透明披露研究方法。
- 公开数据前应处理个人可识别信息和隐私风险。

## 使用边界

上述来源支持的是调查设计与解释原则，不为任何具体样本量、结果阈值、传播策略或商业结论背书。本 Skill 的计算与报告必须完整披露样本来源和限制。

## Brown、Cai 与 DasGupta：二项比例区间

- 论文：Lawrence D. Brown, T. Tony Cai, Anirban DasGupta, “Interval Estimation for a Binomial Proportion”
- 期刊：Statistical Science, 2001, 16(2), 101-133
- DOI：<https://doi.org/10.1214/ss/1009213286>

采用的原则：在独立二项模型成立时，Wilson score interval 可用于表达二项比例的不确定性。本 Skill 只在抽样与观测条件支持该模型时把它作为可选描述，不把区间当作成功门槛，也不声称它能修复非概率样本的选择偏差。

## 本包自行规定的工程约定

以下做法是为了让结果可复查而在本包中定义的操作约定，不归因于上述网页，也不宣称是唯一正确的调查流程：

- 保留未改写的原始回答后再建立编码字典。
- 给编码字典保存版本，修改后重新计算。
- 把查看结果前写下的排除规则与事后排除分开披露。
- 在查看结果前写下停止收集的条件，并披露实际停止与遵守状态，避免按结果方向改变收集时长或记录数。
- 在公开或高风险研究中，可请第二名编码者复核模糊答案。
