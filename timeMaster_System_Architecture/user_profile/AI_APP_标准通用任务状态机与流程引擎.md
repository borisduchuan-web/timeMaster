# AI APP 标准通用任务状态机与流程引擎

版本：v0.1  
日期：2026-05-28  
适用范围：所有任务、订单、子单、AI 接管任务、公益任务、新手任务、技能任务

---

# 一、设计目标

本文件定义平台统一任务流程。

核心目标：

1. 所有任务都走同一套标准流程模板。
2. 简单任务可以把不用的节点标灰，而不是删除流程节点。
3. 复杂任务可以把某个流程节点拆成新的子单。
4. 无人接单、超时、异常时，AI 可以接管流程控制、拆单、沟通、调度或线上可执行部分。
5. 执行过程必须沉淀证据，关键任务要求手机录像，本地 AI 先做检测和评分。
6. 每个流程节点都映射技能树能力值，任务完成后更新熟练度。
7. 个人知识库参与任务准备、任务辅助和成长路径规划。

一句话定义：

任务不是一个订单状态，而是一条可配置、可审计、可拆分、可评分、可成长的标准化履约流程。

---

# 二、核心设计原则

## 1. 流程先于任务

平台不允许只有“标题 + 金额 + 接单按钮”的任务。

每个任务发布前，必须先生成任务流程：

```text
任务需求
→ AI 识别任务类型
→ 选择标准流程模板
→ 生成任务流程节点
→ 设置哪些节点启用、哪些节点标灰
→ 发布任务
```

## 2. 节点不删除，只标灰

为了避免争议，所有任务都展示完整标准流程。

简单任务不用的节点进入：

```text
DISABLED_GREY
```

用户看到的是：

* 当前任务需要执行哪些节点
* 哪些节点本任务不需要
* 为什么不需要
* 是否在接单前已经确定

## 3. 节点可以升级为子单

如果某个节点需要其他人、AI、平台客服或质检员参与，该节点可以生成子单。

例如：

* 上门维修任务中的“配件采购”生成采购子单
* 家政任务中的“垃圾清运”生成清运子单
* 线上资料整理任务中的“AI 初稿生成”生成 AI 子单
* 复杂维修任务中的“二次质检”生成质检子单
* 无人接单时由 AI 接管“任务重拆解与再调度”子单

## 4. AI 接管不是模糊兜底

AI 接管必须定义清楚接管对象。

AI 可以接管：

* 流程控制
* 任务解释
* 沟通摘要
* 任务拆解
* 重新派发
* 线上可自动完成的子任务
* 交付物预审
* 本地检测评分
* 成长建议

AI 不能直接替代现实世界身体劳动。

线下任务无人接单时，AI 的接管方式是：

```text
扩大匹配范围
→ 拆分任务
→ 调整时间
→ 建议调价
→ 通知需求方
→ 转人工运营
→ 生成新的候选子单
```

## 5. 证据链先于争议处理

平台要尽量让争议在发生前被流程消解。

每个关键节点都必须记录：

* 谁操作
* 什么时间操作
* 在哪里操作
* 做了什么
* 上传了什么证据
* AI 检测结果是什么
* 对方是否确认
* 是否超时
* 是否改动过流程

---

# 三、标准通用流程总览

所有任务默认拥有以下标准节点。

| 节点编号 | 节点名称 | 是否默认启用 | 可标灰 | 可转子单 | 说明 |
|---|---|---:|---:|---:|---|
| N00 | 需求录入 | 是 | 否 | 否 | 需求方或平台录入原始需求 |
| N01 | AI 需求理解 | 是 | 否 | 否 | AI 识别任务类型、风险、技能需求 |
| N02 | 合规与风险分级 | 是 | 否 | 是 | 判断是否高风险、是否需人工审核 |
| N03 | 流程模板生成 | 是 | 否 | 否 | 生成完整节点清单 |
| N04 | 报酬与结算规则确认 | 是 | 否 | 是 | 明确用户到账、平台服务费、通道费 |
| N05 | 任务发布 | 是 | 否 | 否 | 发布到任务池或定向派发 |
| N06 | 匹配与候选人推送 | 是 | 否 | 是 | AI/规则匹配候选人 |
| N07 | 接单确认 | 是 | 否 | 否 | 用户确认范围、报酬、流程节点 |
| N08 | 执行前准备 | 是 | 是 | 是 | 工具、路线、材料、知识包 |
| N09 | 到场/上线确认 | 线下启用 | 是 | 否 | 线下到场或线上进入工作区 |
| N10 | 录像/证据采集启动 | 关键任务启用 | 是 | 否 | 手机录像或替代证据开始 |
| N11 | 标准执行节点 | 是 | 否 | 是 | 任务主体执行，可包含多个子步骤 |
| N12 | 中途检查 | 复杂任务启用 | 是 | 是 | 阶段性检查，降低返工 |
| N13 | 交付提交 | 是 | 否 | 否 | 用户提交结果、材料、说明 |
| N14 | 本地 AI 预检评分 | 是 | 是 | 否 | 端侧 AI 对证据和结果初评 |
| N15 | 需求方验收 | 是 | 是 | 否 | 需求方确认或提出返工 |
| N16 | 平台质检/抽检 | 关键任务启用 | 是 | 是 | 平台质检或专家复核 |
| N17 | 返工/补救 | 条件启用 | 是 | 是 | 验收不通过时进入 |
| N18 | 结算 | 是 | 否 | 否 | 账本入账、冻结、提现状态 |
| N19 | 双方评价 | 是 | 是 | 否 | 双方评价、标签化反馈 |
| N20 | 成长结算 | 是 | 否 | 否 | 更新等级、声望、技能熟练度 |
| N21 | 知识库沉淀 | 是 | 是 | 否 | 生成复盘、SOP、作品案例 |
| N22 | 归档 | 是 | 否 | 否 | 任务完成并进入历史档案 |

---

# 四、任务总状态机

任务总状态只描述任务整体生命周期。

节点状态描述具体执行进度。

## 1. 正常主流程

```text
DRAFT
→ AI_ANALYZING
→ FLOW_COMPILED
→ PENDING_REVIEW
→ PUBLISHED
→ MATCHING
→ ACCEPTED
→ PREPARING
→ IN_PROGRESS
→ SUBMITTED
→ AI_PRECHECKING
→ ACCEPTANCE_PENDING
→ QUALITY_CHECKING
→ COMPLETED
→ SETTLEMENT_PENDING
→ SETTLED
→ ARCHIVED
```

## 2. 异常状态

```text
NO_PROVIDER
AI_TAKEOVER
REDISPATCHING
OVERDUE
PAUSED
BLOCKED
REWORK_REQUIRED
DISPUTED
RISK_HOLD
CANCEL_REQUESTED
CANCELLED
REFUNDING
FAILED
```

## 3. 状态说明

| 状态 | 含义 | 可操作角色 |
|---|---|---|
| DRAFT | 需求草稿 | 需求方、平台 |
| AI_ANALYZING | AI 分析需求 | AI |
| FLOW_COMPILED | 已生成流程节点 | AI、平台 |
| PENDING_REVIEW | 待人工审核 | 平台 |
| PUBLISHED | 已发布 | 平台 |
| MATCHING | 匹配候选人 | AI、调度系统 |
| ACCEPTED | 已接单 | 服务者 |
| PREPARING | 执行前准备中 | 服务者、AI |
| IN_PROGRESS | 执行中 | 服务者 |
| SUBMITTED | 已提交交付物 | 服务者 |
| AI_PRECHECKING | AI 初检中 | AI |
| ACCEPTANCE_PENDING | 待需求方验收 | 需求方 |
| QUALITY_CHECKING | 平台质检中 | 平台、质检员 |
| COMPLETED | 已完成 | 系统 |
| SETTLEMENT_PENDING | 待结算 | 系统、财务 |
| SETTLED | 已结算 | 系统 |
| ARCHIVED | 已归档 | 系统 |
| NO_PROVIDER | 无人接单 | AI、平台 |
| AI_TAKEOVER | AI 接管流程 | AI、平台 |
| REDISPATCHING | 重新派发 | AI、平台 |
| OVERDUE | 已超时 | 系统、平台 |
| PAUSED | 暂停 | 平台、双方确认 |
| BLOCKED | 阻塞 | 服务者、AI、平台 |
| REWORK_REQUIRED | 需要返工 | 需求方、平台 |
| DISPUTED | 争议中 | 平台、仲裁 |
| RISK_HOLD | 风控冻结 | 风控系统、平台 |
| CANCEL_REQUESTED | 申请取消 | 需求方、服务者 |
| CANCELLED | 已取消 | 系统、平台 |
| REFUNDING | 退款中 | 财务、平台 |
| FAILED | 任务失败 | 系统、平台 |

---

# 五、节点状态机

每个流程节点都有自己的状态。

## 1. 节点状态

```text
NOT_STARTED
PENDING
ACTIVE
COMPLETED
DISABLED_GREY
SKIPPED_CONFIRMED
BLOCKED
OVERDUE
SUBTASK_CREATED
AI_TAKEOVER
REWORKING
DISPUTED
RISK_HOLD
```

## 2. 节点状态说明

| 节点状态 | 含义 |
|---|---|
| NOT_STARTED | 尚未开始 |
| PENDING | 等待前置节点完成 |
| ACTIVE | 当前正在执行 |
| COMPLETED | 已完成并有证据 |
| DISABLED_GREY | 本任务不启用，前端灰显 |
| SKIPPED_CONFIRMED | 经双方/平台确认跳过 |
| BLOCKED | 当前节点阻塞 |
| OVERDUE | 当前节点超时 |
| SUBTASK_CREATED | 已从节点生成子单 |
| AI_TAKEOVER | 当前节点由 AI 接管 |
| REWORKING | 当前节点返工中 |
| DISPUTED | 当前节点产生争议 |
| RISK_HOLD | 当前节点被风控冻结 |

## 3. 节点数据要求

每个节点至少包含：

```text
node_id
task_id
node_code
node_name
node_status
is_required
is_greyable
grey_reason
can_create_subtask
executor_type
executor_id
start_condition
complete_condition
evidence_required
ai_check_required
human_check_required
deadline
started_at
completed_at
created_subtask_id
```

---

# 六、灰显节点机制

## 1. 为什么要灰显

灰显不是 UI 装饰，而是防争议机制。

例如简单线上资料整理任务，不需要：

* 到场确认
* 线下录像
* 平台质检
* 配件采购

这些节点不应从流程中消失，而应标灰显示：

```text
本任务为线上低风险任务，无需到场确认。
```

## 2. 灰显规则

节点可以灰显的前提：

* 流程模板允许该节点灰显
* AI 给出灰显原因
* 接单前展示给服务者
* 需求方可见
* 接单后不得随意启用或关闭

接单后如果要改变灰显节点，必须走：

```text
变更申请
→ 对方确认
→ 平台/AI 重新评估风险
→ 生成流程变更记录
```

## 3. 灰显节点前端展示

前端状态建议：

* 已完成：绿色
* 当前执行：蓝色
* 待执行：正常灰黑
* 本任务不需要：浅灰
* 阻塞/争议：红色
* AI 接管：紫色或独立标识
* 已生成子单：链路标识

---

# 七、子单机制

## 1. 子单定义

子单是从主任务某个节点拆出来的独立履约单元。

子单必须继承主任务上下文：

```text
parent_task_id
parent_node_id
subtask_type
required_skill
reward_rule
deadline
acceptance_standard
evidence_requirement
```

## 2. 子单类型

| 子单类型 | 说明 | 执行者 |
|---|---|---|
| HUMAN_SUBTASK | 需要其他人完成 | 服务者 |
| AI_SUBTASK | 线上可由 AI 完成 | AI |
| PLATFORM_SUBTASK | 平台运营处理 | 平台 |
| QUALITY_SUBTASK | 质检/复核 | 质检员 |
| PROCUREMENT_SUBTASK | 采购/材料 | 服务者、第三方 |
| REWORK_SUBTASK | 返工补救 | 原服务者或新服务者 |
| ESCALATION_SUBTASK | 升级处理 | 平台、专家 |

## 3. 子单生成场景

可生成子单的场景：

* 主服务者不具备某个子技能
* 任务拆解后可并行执行
* 当前节点无人接单
* 当前节点超时
* AI 判断需要质检
* 需求方追加需求
* 线下任务需要材料采购
* 复杂任务需要专家确认

## 4. 子单与主任务关系

子单完成后，必须回写主任务节点。

```text
子单完成
→ 子单证据包归档
→ 主任务节点状态更新
→ 主任务继续流转
```

如果子单失败：

```text
子单失败
→ 主任务节点 BLOCKED
→ AI 生成处理建议
→ 重新派发/取消/转人工
```

---

# 八、无人接单与 AI 接管流程

## 1. 无人接单触发条件

任务进入 `MATCHING` 后，满足任一条件进入 `NO_PROVIDER`：

* 超过最晚接单时间
* 推送人数达到上限仍无人接单
* 候选人全部拒绝
* 接单后又取消且无人补位
* 风控导致候选人全部不可用

## 2. AI 接管步骤

```text
NO_PROVIDER
→ AI_TAKEOVER
→ 分析无人接单原因
→ 生成接管策略
→ 执行接管策略
→ REDISPATCHING 或 AI_SUBTASK 或 PLATFORM_SUBTASK
```

## 3. AI 接管策略

| 原因 | AI 策略 |
|---|---|
| 报酬过低 | 建议需求方调价或平台项目补贴 |
| 时间过紧 | 建议调整时间窗口 |
| 地点偏远 | 扩大范围、拆分交通节点 |
| 技能要求过高 | 拆成多个低门槛子单 |
| 风险过高 | 转人工审核或提高准入门槛 |
| 描述不清 | AI 追问需求方，重新生成任务 |
| 线上可完成 | 生成 AI 子单或 AI 辅助完成 |

## 4. AI 子单适用范围

AI 可直接执行的子单：

* 文案初稿
* 资料整理
* 表格清洗
* 图片初筛
* 任务说明重写
* 沟通摘要
* 质检初审
* SOP 生成
* 风险提示

AI 不可直接执行的子单：

* 上门维修
* 搬运
* 家政清洁
* 老人儿童陪护
* 需要真实专业资质签字的事项
* 任何现实世界身体操作

---

# 九、手机录像与证据链机制

## 1. 录像触发规则

以下任务建议强制开启手机录像或关键节点录像：

* 入户服务
* 维修安装
* 搬运交付
* 贵重物品相关
* 高金额任务
* 老人儿童相关服务
* 夜间任务
* 争议高发任务
* 技能验证任务

低风险线上任务可不录全程，但必须有交付物证据。

## 2. 录像方式

建议采用：

* 本地录制
* 本地 AI 检测
* 关键帧上传
* 证据摘要上传
* 原始视频加密保存
* 争议时按授权上传完整视频

这样既能保留证据，又能降低隐私和存储成本。

## 3. 视频证据包

每个录像节点生成 `EvidenceBundle`：

```text
evidence_bundle_id
task_id
node_id
video_session_id
local_ai_score
key_frames
audio_risk_flags
location_stamp
time_stamp
device_id
hash
upload_status
privacy_level
```

## 4. 本地 AI 检测项

本地 AI 可以检测：

* 是否到达指定地点
* 是否开启录像
* 画面是否连续
* 是否拍到关键对象
* 是否完成规定步骤
* 是否存在明显危险行为
* 是否存在辱骂、威胁、压价等沟通风险
* 交付物是否清晰
* 是否疑似伪造或重复视频
* 是否满足任务 SOP

## 5. 本地 AI 评分

建议评分结构：

```text
local_ai_score =
process_completeness * 0.30
+ evidence_quality * 0.20
+ safety_compliance * 0.20
+ location_time_match * 0.15
+ delivery_match * 0.15
```

评分只用于辅助验收和成长计算，不直接作为最终处罚依据。

## 6. 隐私规则

录像必须满足：

* 接单前明确告知
* 需求方和服务者知道哪些节点需要录像
* 涉及家庭隐私时支持局部遮挡、关键物证拍摄、语音转写脱敏
* 原始视频默认不公开给需求方
* 争议时按权限调用
* 高隐私场景允许使用替代证据方案

---

# 十、标准节点证据要求

| 节点 | 证据要求 |
|---|---|
| 接单确认 | 用户确认任务范围、报酬、流程节点 |
| 执行前准备 | 工具清单、路线、材料、AI 知识包阅读记录 |
| 到场/上线确认 | GPS、时间、水印照片或线上工作区记录 |
| 录像启动 | video_session_id、本地 AI 检测结果 |
| 标准执行 | 视频片段、照片、操作日志、阶段说明 |
| 中途检查 | 阶段性交付物、AI 检测摘要 |
| 交付提交 | 最终交付物、完成说明、问题记录 |
| AI 预检 | AI 评分、风险标记、缺失项 |
| 需求方验收 | 确认、返工意见或超时自动规则 |
| 平台质检 | 质检结论、抽检证据 |
| 结算 | 账本流水 |
| 成长结算 | 等级、声望、技能变化记录 |
| 知识库沉淀 | 复盘、SOP、作品、经验标签 |

---

# 十一、技能树与熟练度能力值

## 1. 技能树结构

技能树不是静态标签，而是任务节点能力图。

每个技能包含：

```text
skill_id
skill_name
skill_category
parent_skill_id
ability_score
proficiency_level
verified_status
evidence_count
last_used_at
decay_status
```

## 2. 熟练度等级

| 熟练度 | 能力值区间 | 含义 |
|---|---:|---|
| S0 未验证 | 0-19 | 只有自述，没有任务证据 |
| S1 入门 | 20-39 | 可做低风险辅助任务 |
| S2 基础 | 40-59 | 可独立做标准任务 |
| S3 熟练 | 60-74 | 可处理常见异常 |
| S4 专业 | 75-89 | 可做高价值任务和复杂任务 |
| S5 专家 | 90-100 | 可质检、带教、制定 SOP |

## 3. 节点映射技能

每个任务节点都必须配置技能映射。

示例：家电维修任务

| 节点 | 映射技能 | 权重 |
|---|---|---:|
| 执行前准备 | 工具准备、故障判断 | 10% |
| 到场确认 | 服务规范、沟通能力 | 5% |
| 标准执行 | 电器维修、安全操作 | 55% |
| 中途检查 | 故障复核、问题解释 | 10% |
| 交付提交 | 结果说明、清洁收尾 | 10% |
| 需求方验收 | 服务质量、沟通满意度 | 10% |

## 4. 能力值更新公式

建议：

```text
skill_delta =
task_difficulty
* node_weight
* quality_factor
* ai_score_factor
* acceptance_factor
* anti_fraud_factor
```

说明：

* task_difficulty：任务难度
* node_weight：节点对该技能的贡献
* quality_factor：交付质量
* ai_score_factor：本地 AI 检测评分
* acceptance_factor：需求方/质检验收
* anti_fraud_factor：反作弊权重

## 5. 防刷规则

必须限制低价值任务刷熟练度。

规则：

* 同类型低难度任务每日成长有上限
* 同一需求方重复评价权重递减
* 公益任务声望有上限
* 没有视频或有效证据的任务成长权重降低
* 被投诉或争议中的任务暂缓成长结算
* 高等级技能必须通过高难度任务或质检任务验证

---

# 十二、个人知识库参与任务执行

## 1. 知识库作用

个人知识库不是资料夹，而是用户执行任务的 AI 能力底座。

它帮助用户：

* 判断自己能接什么任务
* 提前准备工具和材料
* 生成任务执行 SOP
* 识别自己技能缺口
* 复盘失败任务
* 规划下一阶段成长路径

## 2. 接单前辅助

用户查看任务时，AI 读取个人知识库并生成：

```text
适配度说明
所需技能对比
风险提醒
工具准备清单
预计完成难度
是否建议接单
如果不建议，推荐先做哪些训练任务
```

## 3. 执行中辅助

任务执行时，AI 生成个人化任务包：

```text
当前任务 SOP
用户曾做过的类似任务
常见错误提醒
关键检查点
拍摄证据提醒
交付模板
沟通建议
```

## 4. 完成后沉淀

任务完成后，系统自动生成：

* 本次任务复盘
* 新增技能证据
* 可展示作品
* 常见问题
* 用户个人 SOP
* 下一步成长建议

## 5. 成长路径生成

AI 根据技能树和任务记录生成路径：

```text
当前能力
→ 可接任务
→ 缺口能力
→ 推荐新手/训练/公益任务
→ 推荐正式任务
→ 目标等级
→ 可解锁高价值任务
```

示例：

```text
家具安装 S1
→ 完成 3 个低风险安装辅助任务
→ 学会工具准备和尺寸确认
→ 接 2 个标准安装任务
→ 达到 S2
→ 解锁独立家具安装任务
```

---

# 十三、争议预防机制

## 1. 接单前锁定

接单前必须锁定：

* 任务范围
* 报酬
* 流程节点
* 灰显节点
* 证据要求
* 交付标准
* 超时规则
* 返工规则

## 2. 执行中变更

任何变更都必须生成变更记录。

```text
变更申请
→ AI 解释影响
→ 对方确认
→ 平台风控判断
→ 更新流程节点
→ 生成事件记录
```

## 3. 验收规则

建议验收分三层：

1. AI 预检：检查证据是否完整
2. 需求方验收：确认结果是否满意
3. 平台抽检：处理高风险、高金额、争议任务

## 4. 自动验收

低风险任务可设置自动验收：

```text
提交后 N 小时内需求方未反馈
AND AI 预检通过
AND 无风控标记
→ 自动验收通过
```

## 5. 争议处理依据优先级

建议：

```text
流程节点记录
> 视频/证据包
> 变更记录
> AI 检测摘要
> 双方聊天记录
> 双方口头描述
```

---

# 十四、研发落地数据表

## 1. TaskFlowTemplate

```text
template_id
template_name
task_category
risk_level
version
status
```

## 2. TaskNodeTemplate

```text
node_template_id
template_id
node_code
node_name
sort_order
default_required
greyable
can_create_subtask
evidence_required
ai_check_required
human_check_required
skill_mapping_config
```

## 3. TaskFlowInstance

```text
flow_instance_id
task_id
template_id
template_version
compiled_by
compiled_at
locked_at
change_count
```

## 4. TaskNodeInstance

```text
node_instance_id
flow_instance_id
task_id
node_code
node_name
node_status
is_required
grey_reason
executor_type
executor_id
deadline
started_at
completed_at
subtask_id
evidence_bundle_id
ai_score_id
```

## 5. SubTask

```text
subtask_id
parent_task_id
parent_node_id
subtask_type
title
required_skill
reward
executor_type
executor_id
status
deadline
result
```

## 6. EvidenceBundle

```text
evidence_bundle_id
task_id
node_id
evidence_type
storage_mode
video_session_id
key_frame_urls
hash
privacy_level
created_at
```

## 7. LocalAIScore

```text
ai_score_id
task_id
node_id
model_version
process_score
evidence_score
safety_score
location_time_score
delivery_score
risk_flags
summary
created_at
```

## 8. SkillGrowthLedger

```text
ledger_id
user_id
task_id
node_id
skill_id
before_score
delta_score
after_score
growth_reason
evidence_bundle_id
created_at
```

## 9. KnowledgeUpdateLog

```text
update_id
user_id
task_id
source_node_id
knowledge_type
title
summary
visibility
created_at
```

---

# 十五、关键事件

系统建议采用事件驱动。

```text
TASK_CREATED
TASK_AI_ANALYZED
TASK_FLOW_COMPILED
TASK_FLOW_LOCKED
TASK_PUBLISHED
TASK_MATCHING_STARTED
TASK_NO_PROVIDER
TASK_AI_TAKEOVER_STARTED
TASK_ACCEPTED
NODE_ACTIVATED
NODE_COMPLETED
NODE_DISABLED_GREY
NODE_SUBTASK_CREATED
VIDEO_SESSION_STARTED
LOCAL_AI_SCORE_CREATED
TASK_SUBMITTED
TASK_AI_PRECHECK_PASSED
TASK_ACCEPTED_BY_DEMANDER
TASK_REWORK_REQUIRED
TASK_DISPUTED
TASK_COMPLETED
SETTLEMENT_CREATED
SKILL_GROWTH_SETTLED
KNOWLEDGE_UPDATED
TASK_ARCHIVED
```

---

# 十六、MVP 落地建议

第一版不要一次做完所有复杂能力。

建议先实现：

1. 固定 1-2 个任务流程模板。
2. 每个任务生成节点实例。
3. 前端展示完整流程，支持灰显节点。
4. 支持接单前锁定流程。
5. 支持关键节点上传图片/视频。
6. 支持简单本地 AI 检测结果字段，初期可人工录入或模拟模型结果。
7. 支持节点转子单，但第一版只开放平台人工子单和质检子单。
8. 支持任务完成后写入技能成长账本。
9. 支持知识库自动生成任务复盘。

第二版再实现：

* AI 自动拆单
* 无人接单 AI 接管
* 本地端侧模型真实评分
* 高级视频证据管理
* 复杂技能树能力值计算
* 个性化成长路径推荐

---

# 十七、产品壁垒总结

这套流程的壁垒不在于“能不能接单”，而在于：

1. 每个任务都有标准流程，不再依赖口头约定。
2. 简单任务灰显无关节点，复杂任务拆子单，流程既统一又灵活。
3. 无人接单时 AI 接管调度和拆解，减少任务死单。
4. 手机录像和本地 AI 评分形成低成本证据链。
5. 每个节点都能反向更新技能树，使任务履约变成能力成长。
6. 个人知识库让用户越做越会做，平台越用越懂用户。
7. 等级、声望、熟练度来自真实流程证据，不靠充值和刷资料。

这就是区别于传统接单平台的核心套路：

传统平台记录订单结果，本平台记录人的能力生成过程。

---

# 十八、标准状态迁移表

状态迁移表是研发实现任务状态机的核心依据。

任何状态变更都必须通过状态机服务执行，不允许业务代码直接修改 `task_status`。

## 1. 主任务状态迁移

| 当前状态 | 触发事件 | 下一个状态 | 触发角色 | 必要校验 |
|---|---|---|---|---|
| DRAFT | TASK_SUBMIT_FOR_AI | AI_ANALYZING | 需求方/平台 | 需求描述不为空 |
| AI_ANALYZING | TASK_AI_ANALYZED | FLOW_COMPILED | AI | 已生成任务类型、风险、技能要求 |
| FLOW_COMPILED | TASK_SUBMIT_REVIEW | PENDING_REVIEW | AI/平台 | 流程节点已生成 |
| PENDING_REVIEW | TASK_REVIEW_PASS | PUBLISHED | 平台 | 报酬、流程、风险、证据规则完整 |
| PENDING_REVIEW | TASK_REVIEW_REJECT | DRAFT | 平台 | 写入驳回原因 |
| PUBLISHED | TASK_MATCHING_STARTED | MATCHING | 调度系统 | 任务可见、未过期 |
| MATCHING | TASK_ACCEPTED | ACCEPTED | 服务者 | 准入条件通过 |
| MATCHING | TASK_NO_PROVIDER | NO_PROVIDER | 调度系统 | 超时或候选耗尽 |
| NO_PROVIDER | TASK_AI_TAKEOVER_STARTED | AI_TAKEOVER | AI | 生成接管原因 |
| AI_TAKEOVER | TASK_REDISPATCH | REDISPATCHING | AI/平台 | 已生成再派发策略 |
| REDISPATCHING | TASK_MATCHING_STARTED | MATCHING | 调度系统 | 新规则已生效 |
| AI_TAKEOVER | TASK_CREATE_AI_SUBTASK | IN_PROGRESS | AI | 子单已创建或 AI 可执行 |
| ACCEPTED | TASK_PREPARE_STARTED | PREPARING | 服务者 | 接单确认已锁定 |
| PREPARING | TASK_START | IN_PROGRESS | 服务者 | 前置准备节点完成 |
| IN_PROGRESS | TASK_SUBMIT | SUBMITTED | 服务者 | 必填证据完整 |
| SUBMITTED | TASK_AI_PRECHECK_START | AI_PRECHECKING | 系统/AI | 交付物存在 |
| AI_PRECHECKING | TASK_AI_PRECHECK_PASS | ACCEPTANCE_PENDING | AI | 无高风险标记 |
| AI_PRECHECKING | TASK_AI_PRECHECK_FAIL | REWORK_REQUIRED | AI/平台 | 写入缺失项 |
| ACCEPTANCE_PENDING | TASK_ACCEPTED_BY_DEMANDER | COMPLETED | 需求方 | 验收通过 |
| ACCEPTANCE_PENDING | TASK_REWORK_REQUIRED | REWORK_REQUIRED | 需求方/平台 | 返工意见明确 |
| ACCEPTANCE_PENDING | TASK_AUTO_ACCEPT | COMPLETED | 系统 | 超时未反馈且 AI 预检通过 |
| REWORK_REQUIRED | TASK_REWORK_START | IN_PROGRESS | 服务者 | 返工节点已生成 |
| COMPLETED | SETTLEMENT_CREATE | SETTLEMENT_PENDING | 系统 | 无未结争议 |
| SETTLEMENT_PENDING | SETTLEMENT_SUCCESS | SETTLED | 系统/财务 | 账本写入成功 |
| SETTLED | TASK_ARCHIVE | ARCHIVED | 系统 | 成长结算完成 |

## 2. 异常状态迁移

| 当前状态 | 触发事件 | 下一个状态 | 说明 |
|---|---|---|---|
| 任意非终态 | TASK_RISK_HOLD | RISK_HOLD | 风控冻结 |
| RISK_HOLD | TASK_RISK_RELEASE | 原状态 | 风控解除后回到冻结前状态 |
| RISK_HOLD | TASK_CANCEL_BY_RISK | CANCELLED | 严重风险取消 |
| 任意执行态 | TASK_OVERDUE | OVERDUE | 节点或任务超时 |
| OVERDUE | TASK_EXTEND_APPROVED | 原执行状态 | 双方同意延期 |
| OVERDUE | TASK_REDISPATCH | REDISPATCHING | 超时后重派 |
| 任意执行态 | TASK_DISPUTE_OPEN | DISPUTED | 开启争议 |
| DISPUTED | TASK_DISPUTE_RESOLVED_COMPLETE | COMPLETED | 仲裁后完成 |
| DISPUTED | TASK_DISPUTE_RESOLVED_REWORK | REWORK_REQUIRED | 仲裁后返工 |
| DISPUTED | TASK_DISPUTE_RESOLVED_CANCEL | CANCELLED | 仲裁后取消 |
| 任意非终态 | TASK_CANCEL_REQUEST | CANCEL_REQUESTED | 一方申请取消 |
| CANCEL_REQUESTED | TASK_CANCEL_APPROVED | CANCELLED | 取消通过 |
| CANCEL_REQUESTED | TASK_CANCEL_REJECTED | 原状态 | 取消驳回 |
| CANCELLED | REFUND_START | REFUNDING | 需要退款 |
| REFUNDING | REFUND_DONE | ARCHIVED | 退款完成并归档 |

## 3. 终态

以下状态为终态：

```text
ARCHIVED
CANCELLED
FAILED
```

终态任务不可再进入执行流程，只能追加：

* 复盘
* 争议补充材料
* 客服备注
* 审计记录
* 知识库沉淀

---

# 十九、角色权限矩阵

## 1. 角色定义

| 角色 | 说明 |
|---|---|
| DEMANDER | 需求方 |
| PROVIDER | 服务者 |
| AI_AGENT | AI 助手/调度 Agent |
| DISPATCH_SYSTEM | 调度系统 |
| PLATFORM_OPERATOR | 平台运营 |
| QUALITY_INSPECTOR | 质检员 |
| RISK_ENGINE | 风控系统 |
| CUSTOMER_SERVICE | 客服/仲裁 |
| FINANCE_SYSTEM | 财务/结算系统 |

## 2. 操作权限

| 操作 | 需求方 | 服务者 | AI | 平台 | 质检 | 风控 | 财务 |
|---|---:|---:|---:|---:|---:|---:|---:|
| 创建需求 | 是 | 否 | 辅助 | 是 | 否 | 否 | 否 |
| 生成流程 | 否 | 否 | 是 | 是 | 否 | 否 | 否 |
| 修改流程模板 | 否 | 否 | 建议 | 是 | 否 | 否 | 否 |
| 发布任务 | 是 | 否 | 否 | 是 | 否 | 否 | 否 |
| 接单 | 否 | 是 | 否 | 否 | 否 | 否 | 否 |
| 取消接单 | 条件 | 条件 | 建议 | 是 | 否 | 条件 | 否 |
| 启动节点 | 否 | 是 | 条件 | 是 | 条件 | 否 | 否 |
| 完成节点 | 条件 | 是 | 条件 | 是 | 条件 | 否 | 否 |
| 创建子单 | 申请 | 申请 | 是 | 是 | 是 | 否 | 否 |
| 启动录像 | 否 | 是 | 提醒 | 否 | 否 | 否 | 否 |
| 查看证据 | 条件 | 条件 | 条件 | 是 | 是 | 是 | 否 |
| 验收任务 | 是 | 否 | 预检 | 是 | 是 | 否 | 否 |
| 发起争议 | 是 | 是 | 建议 | 是 | 是 | 是 | 否 |
| 风控冻结 | 否 | 否 | 建议 | 是 | 否 | 是 | 否 |
| 结算 | 否 | 否 | 否 | 条件 | 否 | 条件 | 是 |
| 成长结算 | 否 | 否 | 计算 | 是 | 是 | 风控影响 | 否 |

## 3. 权限原则

* AI 可以建议，不默认拥有最终处罚权。
* 服务者只能操作自己承接的节点。
* 需求方不能随意修改已锁定流程。
* 平台运营可以介入流程，但必须生成审计日志。
* 风控可以冻结，但解除和处罚需保留复核入口。
* 财务只处理结算，不直接修改任务执行状态。

---

# 二十、标准流程模板

流程模板用于把不同任务快速编排为标准节点。

## 1. 模板 A：线上简单任务

适用：

* 文案整理
* 表格清洗
* 图片标注
* 资料核验
* AI 辅助内容生成

启用节点：

| 节点 | 状态 |
|---|---|
| N00 需求录入 | 启用 |
| N01 AI 需求理解 | 启用 |
| N02 合规与风险分级 | 启用 |
| N03 流程模板生成 | 启用 |
| N04 报酬与结算规则确认 | 启用 |
| N05 任务发布 | 启用 |
| N06 匹配与候选人推送 | 启用 |
| N07 接单确认 | 启用 |
| N08 执行前准备 | 启用 |
| N09 到场/上线确认 | 标灰 |
| N10 录像/证据采集启动 | 标灰 |
| N11 标准执行节点 | 启用 |
| N12 中途检查 | 标灰 |
| N13 交付提交 | 启用 |
| N14 本地 AI 预检评分 | 启用 |
| N15 需求方验收 | 启用 |
| N16 平台质检/抽检 | 标灰 |
| N17 返工/补救 | 条件启用 |
| N18 结算 | 启用 |
| N19 双方评价 | 启用 |
| N20 成长结算 | 启用 |
| N21 知识库沉淀 | 启用 |
| N22 归档 | 启用 |

最小证据：

* 交付文件
* 操作记录
* AI 预检摘要
* 需求方验收结果

## 2. 模板 B：线下标准服务任务

适用：

* 上门维修
* 家具安装
* 家政服务
* 门店巡检
* 社区服务

启用节点：

* N00-N09 全部启用
* N10 根据风险启用
* N11 启用
* N12 根据复杂度启用
* N13-N22 全部启用

最小证据：

* 到场定位
* 到场照片
* 执行过程照片或视频
* 完成照片
* 需求方验收
* AI 预检评分

## 3. 模板 C：高风险线下任务

适用：

* 入户维修
* 夜间服务
* 老人儿童相关服务
* 高金额维修
* 贵重物品相关服务

强制节点：

* N02 合规与风险分级
* N09 到场确认
* N10 录像/证据采集启动
* N12 中途检查
* N14 本地 AI 预检评分
* N16 平台质检/抽检
* N18 结算前风控检查

额外要求：

* 实名认证
* 人脸核验
* 位置水印
* 关键节点视频
* 高风险提示确认
* 必要时购买保险或平台保障

## 4. 模板 D：公益/新手任务

适用：

* 社区公益
* 新人训练
* 低风险公共服务
* 平台技能验证前置任务

特点：

* 低风险
* 强引导
* 强复盘
* 成长权重有限
* 可用于初始声望建立

必须启用：

* AI 任务讲解
* 执行前准备
* 交付提交
* AI 预检
* 成长结算
* 知识库沉淀

灰显：

* 高风险录像
* 平台强质检
* 复杂中途检查

## 5. 模板 E：项目拆解任务

适用：

* 企业门店巡检
* 城市数据采集
* 多人协作项目
* 政府/社区批量任务

特点：

* 主任务只负责项目目标
* 子单负责具体执行
* 必须有质检抽样
* 结算可能分阶段

必须支持：

* 批量子单生成
* 子单进度汇总
* 质检抽样比例
* 项目看板
* 阶段结算

---

# 二十一、节点配置标准

每个节点模板必须配置以下内容。

## 1. 基础配置

```text
node_code
node_name
node_description
sort_order
default_required
greyable
can_skip_after_lock
can_create_subtask
executor_type
```

## 2. 条件配置

```text
enable_condition
grey_condition
start_condition
complete_condition
timeout_rule
rework_rule
cancel_rule
```

示例：

```text
enable_condition:
task.risk_level >= 3 OR task.location_type = "onsite"

grey_condition:
task.location_type = "online" AND task.risk_level <= 1
```

## 3. 证据配置

```text
evidence_required
evidence_type
min_photo_count
video_required
location_required
watermark_required
ai_check_required
human_check_required
```

## 4. 成长配置

```text
skill_mapping
growth_weight
reputation_impact
level_exp_impact
anti_fraud_weight
```

示例：

```text
skill_mapping:
[
  { skill_id: "repair.diagnosis", weight: 0.25 },
  { skill_id: "repair.operation", weight: 0.55 },
  { skill_id: "service.communication", weight: 0.20 }
]
```

---

# 二十二、SLA 与超时规则

## 1. 关键时间字段

```text
latest_accept_time
expected_start_time
expected_end_time
node_deadline
acceptance_deadline
rework_deadline
settlement_deadline
```

## 2. 超时策略

| 超时场景 | 系统动作 | 是否影响声望 |
|---|---|---:|
| 无人接单超时 | 进入 NO_PROVIDER，AI 接管 | 否 |
| 服务者未按时开始 | 提醒，超过阈值可取消/重派 | 是 |
| 节点执行超时 | 节点 OVERDUE，AI 询问原因 | 条件 |
| 需求方验收超时 | 自动验收或平台介入 | 否 |
| 返工超时 | 转平台仲裁或重派 | 是 |
| 结算超时 | 财务告警 | 否 |

## 3. 自动提醒

建议提醒节点：

* 接单后立即发送准备提醒
* 开始前 30 分钟提醒
* 到场前提醒开启证据采集
* 每个节点超时前提醒
* 交付后提醒需求方验收
* 验收超时前提醒自动验收规则

---

# 二十三、流程变更机制

任务接单前，流程可以由 AI 或平台修改。

任务接单后，流程必须锁定。

## 1. 可变更内容

接单后允许变更：

* 时间
* 地点
* 部分节点是否启用
* 交付物补充
* 子单拆分
* 报酬追加
* 返工规则

不允许单方变更：

* 降低服务者报酬
* 增加未付费工作范围
* 取消已要求的关键证据
* 绕过高风险质检
* 删除争议相关记录

## 2. 变更流程

```text
发起变更
→ AI 生成影响说明
→ 对方确认
→ 风险重评
→ 必要时平台审核
→ 生成 FlowChangeLog
→ 更新节点实例
```

## 3. FlowChangeLog

```text
change_id
task_id
flow_instance_id
changed_by
change_type
before_snapshot
after_snapshot
ai_impact_summary
confirmed_by_counterparty
reviewed_by_platform
created_at
```

---

# 二十四、接口清单

以下为研发第一版建议接口，不限定具体 REST 或 RPC 形式。

## 1. 任务与流程

```text
POST /tasks
创建任务草稿

POST /tasks/{task_id}/analyze
AI 分析需求并生成流程建议

POST /tasks/{task_id}/compile-flow
根据模板生成流程实例

GET /tasks/{task_id}/flow
获取任务流程节点

POST /tasks/{task_id}/publish
发布任务

POST /tasks/{task_id}/accept
服务者接单并锁定流程

POST /tasks/{task_id}/start
开始任务

POST /tasks/{task_id}/submit
提交交付物

POST /tasks/{task_id}/cancel-request
申请取消
```

## 2. 节点

```text
POST /task-nodes/{node_id}/start
启动节点

POST /task-nodes/{node_id}/complete
完成节点

POST /task-nodes/{node_id}/skip
申请跳过节点

POST /task-nodes/{node_id}/create-subtask
从节点创建子单

GET /task-nodes/{node_id}/evidence
查看节点证据
```

## 3. 子单

```text
POST /subtasks
创建子单

POST /subtasks/{subtask_id}/accept
接子单

POST /subtasks/{subtask_id}/complete
完成子单

POST /subtasks/{subtask_id}/fail
标记子单失败
```

## 4. 证据与本地 AI

```text
POST /evidence/video-session/start
启动视频证据会话

POST /evidence/video-session/{session_id}/keyframes
上传关键帧

POST /evidence/bundles
提交证据包

POST /ai/local-score
提交本地 AI 检测评分

GET /ai/local-score/{score_id}
查看评分结果
```

## 5. 验收、争议与结算

```text
POST /tasks/{task_id}/ai-precheck
发起 AI 预检

POST /tasks/{task_id}/acceptance/pass
需求方验收通过

POST /tasks/{task_id}/acceptance/rework
需求方要求返工

POST /tasks/{task_id}/disputes
开启争议

POST /tasks/{task_id}/settlement
创建结算

POST /tasks/{task_id}/growth-settlement
执行成长结算
```

## 6. 技能与知识库

```text
GET /users/{user_id}/skill-tree
查看技能树

POST /skills/growth-ledger
写入技能成长记录

GET /users/{user_id}/knowledge-base
查看个人知识库

POST /knowledge/task-review
生成任务复盘

POST /knowledge/growth-path
生成成长路径
```

---

# 二十五、前端页面与交互规范

## 1. 任务详情页

必须展示：

* 任务目标
* 报酬和到账说明
* 等级/声望/技能要求
* 完整流程节点
* 灰显节点及原因
* 证据要求
* 是否需要录像
* AI 适配度说明
* 接单后不可单方修改的条款

## 2. 任务执行页

核心组件：

* 当前节点卡片
* 节点进度条
* 证据采集入口
* AI 助手入口
* 子单状态
* 风险提醒
* 下一步按钮

按钮规则：

* 只有当前可执行节点显示主按钮
* 灰显节点不可点击，但可查看原因
* 阻塞节点显示“查看阻塞原因”
* 子单节点显示“查看子单”
* 风控节点显示“等待平台处理”

## 3. 录像交互

录像前必须展示：

* 为什么需要录像
* 录像用于什么
* 谁可以查看
* 是否上传完整视频
* 如何保护隐私

录像中必须展示：

* 当前节点
* 已录制时长
* 本地 AI 检测提示
* 关键步骤提醒

录像后必须展示：

* 关键帧
* AI 初检结果
* 缺失证据提醒
* 是否需要补拍

## 4. 成长反馈页

任务完成后展示：

* 本次收入
* 等级经验变化
* 声望变化
* 相关技能熟练度变化
* 新增知识库内容
* 下一个推荐任务
* 成长路径下一步

---

# 二十六、本地 AI 检测落地方案

## 1. 第一阶段：规则 + 轻模型

第一版不追求复杂端侧大模型。

可先实现：

* GPS 与时间校验
* 视频时长校验
* 图片清晰度检测
* 关键帧抽取
* OCR 识别
* 简单物体识别
* 音频敏感词检测
* 证据完整性校验

## 2. 第二阶段：任务 SOP 检测

针对高频任务训练轻量模型。

例如：

* 门店巡检：门头、货架、收银台、营业执照
* 家具安装：零件、工具、完成状态
* 维修任务：故障点、拆装过程、完成前后对比
* 公益任务：到场、服务对象确认、活动完成

## 3. 第三阶段：个性化能力评估

结合用户历史任务，判断：

* 本次表现是否优于历史平均
* 哪个节点经常出错
* 哪个技能增长最快
* 是否适合更高难度任务

## 4. 端云协同

建议：

```text
端侧：
实时提醒、隐私保护、关键帧抽取、初步评分

云侧：
复杂模型分析、跨任务比对、风控、成长结算
```

---

# 二十七、数据库约束与审计要求

## 1. 状态不可随意覆盖

所有状态变化必须写入：

```text
TaskStatusLog
NodeStatusLog
```

字段：

```text
log_id
object_type
object_id
from_status
to_status
event_type
operator_type
operator_id
reason
metadata
created_at
```

## 2. 乐观锁

任务、节点、子单建议使用版本号：

```text
version
updated_at
```

更新时必须校验版本，避免并发导致状态错乱。

## 3. 幂等键

关键接口必须支持幂等：

```text
idempotency_key
```

适用：

* 接单
* 提交任务
* 完成节点
* 创建子单
* 结算
* 成长结算

## 4. 不可删除原则

以下数据不允许物理删除：

* 任务流程节点
* 证据包
* 状态日志
* 结算流水
* 成长流水
* 争议记录

只能逻辑隐藏或脱敏。

---

# 二十八、结算与成长的触发顺序

任务完成后不能直接给成长值，必须先完成结算前检查。

标准顺序：

```text
任务验收通过
→ 检查争议状态
→ 检查风控状态
→ 生成结算流水
→ 用户收入入账
→ 生成成长结算任务
→ 计算等级经验
→ 计算声望变化
→ 计算技能熟练度变化
→ 更新个人知识库
→ 归档任务
```

## 1. 收入结算

收入结算只受任务验收和财务规则影响。

## 2. 成长结算

成长结算受更多因素影响：

* 证据完整度
* AI 评分
* 需求方评价
* 平台质检
* 风控结果
* 是否公益任务
* 是否重复低难度任务
* 是否存在投诉

## 3. 延迟成长

以下情况成长值暂缓：

* 争议中
* 风控中
* 等待质检
* 高风险任务未抽检
* 证据缺失

---

# 二十九、测试用例清单

## 1. 正常流程测试

* 线上简单任务从创建到归档
* 线下任务从接单到录像再到结算
* 公益任务完成后只增加有限声望
* 高风险任务必须经过质检

## 2. 灰显节点测试

* 线上任务到场节点自动灰显
* 低风险任务录像节点灰显
* 接单后灰显节点不能被单方改成启用
* 灰显原因前后端一致

## 3. 子单测试

* 节点创建人工子单
* 子单完成后主节点自动完成
* 子单失败后主任务进入 BLOCKED
* 子单产生独立证据包

## 4. AI 接管测试

* 无人接单进入 NO_PROVIDER
* AI 分析无人接单原因
* AI 建议调价后重新派发
* 线上任务生成 AI 子单

## 5. 证据链测试

* 视频会话启动成功
* 关键帧上传成功
* 本地 AI 评分写入
* 证据缺失时无法提交
* 争议时可查看证据包

## 6. 状态机测试

* 非法状态迁移被拒绝
* 重复提交不会重复结算
* 并发接单只有一个成功
* 风控冻结后不能继续执行
* 终态任务不能再次执行

## 7. 成长结算测试

* 技能值按节点权重增加
* 低价值任务达到每日成长上限
* 争议任务暂缓成长
* 质检不通过扣减声望
* 知识库自动生成复盘

---

# 三十、MVP 开发任务拆分

## 1. 后端第一批

优先级 P0：

* 任务表
* 流程模板表
* 节点模板表
* 流程实例表
* 节点实例表
* 状态机服务
* 状态日志
* 接单接口
* 节点完成接口
* 任务提交接口

优先级 P1：

* 子单表
* 证据包表
* 本地 AI 评分表
* 成长流水表
* 知识库更新表
* 争议表
* 结算流水表

## 2. 前端第一批

优先级 P0：

* 任务详情页流程节点展示
* 接单确认页
* 任务执行页
* 节点证据上传
* 交付提交页
* 验收页

优先级 P1：

* 灰显原因展示
* 子单展示
* AI 适配说明
* 本地 AI 评分结果展示
* 成长反馈页

## 3. AI 第一批

优先级 P0：

* 需求分类
* 风险分级
* 流程模板推荐
* 任务说明生成
* 交付物完整性检查

优先级 P1：

* 无人接单原因分析
* 调价/拆单建议
* 本地 AI 检测接入
* 任务复盘生成
* 成长路径生成

## 4. 后台第一批

优先级 P0：

* 任务管理
* 流程模板管理
* 节点配置管理
* 任务审核
* 状态日志查看
* 证据查看

优先级 P1：

* 质检后台
* 争议处理
* 风控冻结/解除
* 成长规则配置
* 子单管理

---

# 三十一、上线验收标准

第一版上线前必须满足：

1. 任意任务都能生成流程实例。
2. 前端能展示启用节点和灰显节点。
3. 接单时能锁定流程快照。
4. 状态机能拒绝非法流转。
5. 节点能上传证据。
6. 任务能完成验收和结算。
7. 成长流水能记录技能变化。
8. 争议时能回看状态日志和证据包。
9. 无人接单时能进入 AI 接管或平台处理。
10. 简单任务不需要的节点不会干扰执行，但仍可见可解释。

---

# 三十二、最终研发共识

研发实现时必须坚持一个核心共识：

任务不是一条订单记录，而是一组有顺序、有责任人、有证据、有评分、有成长结果的节点实例。

因此系统的核心对象不是单个 `Order`，而是：

```text
Task
+ TaskFlowInstance
+ TaskNodeInstance
+ EvidenceBundle
+ SubTask
+ LocalAIScore
+ SkillGrowthLedger
+ KnowledgeUpdateLog
```

只要这个模型成立，平台就能做到：

* 简单任务轻量执行
* 复杂任务标准拆解
* 无人接单自动接管
* 争议有证据可查
* 用户每次劳动都能沉淀成能力资产

