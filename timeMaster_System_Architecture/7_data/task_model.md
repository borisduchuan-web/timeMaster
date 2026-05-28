# 任务数据模型（Task Model）

任务（Task）：

是 timeMaster 中最核心的数据对象之一。

它不是：

简单的信息发布记录。

而是：

现实世界需求在系统中的结构化表达。

---

# 一、核心思想（核心🔥）

传统平台中的任务：

通常只是：

```plaintext
标题 + 描述 + 价格
```

但 timeMaster 中的任务：

必须能够被系统：

---

## 理解

---

## 匹配

---

## 调度

---

## 分级

---

## 追踪

---

## 分析

---

因此：

任务模型必须同时承载：

---

## 业务信息

---

## 时间信息

---

## 空间信息

---

## 能力要求

---

## 调度状态

---

## 风险等级

---

# 二、任务模型目标

任务模型需要解决：

---

## 这个任务是什么

---

## 谁发布的

---

## 什么时候需要完成

---

## 在哪里完成

---

## 需要什么能力

---

## 有多紧急

---

## 当前处于什么状态

---

## 是否已经进入调度

---

# 三、任务基础结构

---

## 基础字段

```plaintext
task_id
publisher_id
title
description
service_id
service_category
```

说明：

* task_id：任务唯一标识
* publisher_id：任务发布者
* title：任务标题
* description：任务描述
* service_id：关联服务类型
* service_category：服务分类

---

# 四、任务时间结构（核心🔥）

时间是任务模型中最重要的部分之一。

---

## 时间字段

```plaintext
created_time
published_time
expected_start_time
expected_end_time
latest_accept_time
actual_start_time
actual_end_time
```

---

## 字段说明

* created_time：创建时间
* published_time：正式发布时间
* expected_start_time：期望开始时间
* expected_end_time：期望结束时间
* latest_accept_time：最晚接单时间
* actual_start_time：实际开始时间
* actual_end_time：实际结束时间

---

# 五、任务优先级结构（核心🔥）

任务必须支持不同紧急程度。

---

## 优先级字段

```plaintext
priority_level
priority_type
max_response_time
```

---

## 示例优先级

```plaintext
deferred      延时任务
realtime      实时任务
urgent        紧急任务
emergency     求救任务
```

---

## 字段说明

* priority_level：数值优先级
* priority_type：任务优先级类型
* max_response_time：最大允许响应时间

---

# 六、任务空间结构（核心🔥）

现实世界任务通常与地点强相关。

---

## 地点字段

```plaintext
location_type
address
longitude
latitude
city_code
district_code
service_radius
```

---

## 字段说明

* location_type：线上 / 线下 / 上门 / 多地点
* address：任务地址
* longitude：经度
* latitude：纬度
* city_code：城市编码
* district_code：区域编码
* service_radius：可接受服务范围

---

# 七、任务能力要求结构（核心🔥）

任务必须明确：

需要什么样的人完成。

---

## 能力字段

```plaintext
required_skills
required_capability_level
required_certifications
required_tools
```

---

## 字段说明

* required_skills：所需技能标签
* required_capability_level：最低能力等级
* required_certifications：需要的证书
* required_tools：需要的工具或设备

---

# 八、任务价格结构

任务价格不仅取决于内容，

也取决于：

时间、距离、紧急程度。

---

## 价格字段

```plaintext
budget_amount
estimated_price
final_price
platform_fee_rate
```

---

## 字段说明

* budget_amount：用户预算
* estimated_price：系统预估价格
* final_price：最终成交价格
* platform_fee_rate：平台抽佣比例

---

# 九、任务调度结构（核心🔥）

任务是否进入调度系统，

以及调度进度，

必须被记录。

---

## 调度字段

```plaintext
dispatch_status
dispatch_round
matched_provider_count
last_dispatch_time
dispatch_expire_time
```

---

## 示例状态

```plaintext
not_dispatched
dispatching
matched
dispatch_failed
expired
```

---

## 字段说明

* dispatch_status：调度状态
* dispatch_round：当前第几轮调度
* matched_provider_count：匹配到的服务者数量
* last_dispatch_time：最近一次调度时间
* dispatch_expire_time：调度过期时间

---

# 十、任务状态结构（核心🔥）

任务状态用于描述任务生命周期。

---

## 状态字段

```plaintext
task_status
```

---

## 示例状态

```plaintext
draft
published
matching
accepted
in_progress
completed
cancelled
timeout
closed
```

---

# 十一、任务风险结构

任务可能存在不同风险等级。

---

## 风险字段

```plaintext
risk_level
risk_tags
audit_status
```

---

## 字段说明

* risk_level：风险等级
* risk_tags：风险标签
* audit_status：审核状态

---

## 审核状态示例

```plaintext
pending
approved
rejected
manual_review
```

---

# 十二、任务参与者结构

任务不一定只有发布者和执行者。

未来可能存在：

被服务人、干系人、协助者。

---

## 参与者字段

```plaintext
demander_id
provider_id
target_person_id
stakeholder_ids
```

---

## 字段说明

* demander_id：需求方
* provider_id：最终执行者
* target_person_id：被服务对象
* stakeholder_ids：相关干系人

---

# 十三、任务内容附件

部分任务需要图片、视频、文件。

---

## 附件字段

```plaintext
attachments
media_type
before_images
after_images
```

---

## 说明

用于：

* 描述任务
* 服务前后对比
* 纠纷处理
* 能力案例积累

---

# 十四、任务结果结构

任务完成后，

需要记录结果。

---

## 结果字段

```plaintext
completion_result
completion_note
completion_media
quality_score
```

---

# 十五、任务事件记录（重要🔥）

任务会经历多个状态变化。

因此：

需要事件记录。

---

## 事件字段

```plaintext
task_event_logs
```

记录：

* 创建
* 发布
* 调度
* 接单
* 开始
* 完成
* 取消
* 超时

---

# 十六、任务与订单关系

任务：

描述需求。

订单：

描述交易与执行关系。

---

## 关系说明

一个任务：

通常生成一个订单。

未来：

复杂任务可能生成：

多个订单。

---

# 十七、任务与技能中心关系（核心🔥）

任务完成后：

会反向影响：

用户技能中心。

例如：

---

## 增加技能经验

---

## 更新能力可信度

---

## 形成服务案例

---

## 影响推荐排序

---

# 十八、任务与数字人关系（未来🔥）

长期来看：

任务记录：

会成为：

数字人系统的重要数据来源。

因为：

它能反映：

---

## 用户真实能力

---

## 时间习惯

---

## 服务稳定性

---

## 行为模式

---

# 十九、MVP阶段建议字段

MVP阶段不需要一次性实现全部字段。

建议优先实现：

```plaintext
task_id
publisher_id
title
description
service_id
priority_type
task_status
expected_start_time
expected_end_time
address
longitude
latitude
budget_amount
dispatch_status
created_time
updated_time
```

---

# 二十、未来扩展字段

未来可逐步增加：

```plaintext
required_skills
required_certifications
risk_tags
task_event_logs
completion_media
quality_score
stakeholder_ids
```

---

# 二十一、设计原则（核心🔥）

任务模型必须：

---

## 可调度

---

## 可追踪

---

## 可分级

---

## 可审核

---

## 可扩展

---

## 可反哺能力系统

---

# 总结

Task Model：

本质上：

不是任务表设计。

而是：

现实世界需求进入 timeMaster 后，

被系统理解、调度、执行、沉淀的核心数据结构。
