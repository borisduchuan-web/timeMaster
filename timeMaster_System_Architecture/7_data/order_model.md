# 订单模型（Order Model）

订单是：

任务执行关系的核心载体。

---

# 一、订单核心目标

记录：

* 谁发布
* 谁执行
* 什么时间
* 什么状态
* 是否完成

---

# 二、订单基础结构

---

## 基础信息

```plaintext
order_id
task_id
demander_id
provider_id
```

---

## 时间信息（核心🔥）

```plaintext
create_time
accept_time
start_time
finish_time
```

---

## 任务属性

```plaintext
task_priority
service_type
task_location
```

---

## 状态信息

```plaintext
order_status
cancel_reason
```

状态包括：

* 待匹配
* 已推送
* 已接单
* 服务中
* 已完成
* 已取消

---

## 定价信息

```plaintext
service_price
platform_fee
provider_income
```

---

## 评价信息

```plaintext
demander_rating
provider_rating
```

---

# 三、实时调度字段（核心🔥）

```plaintext
dispatch_attempts
response_time
estimated_arrival_time
```

用于：

调度优化与数据分析。

---

# 四、订单事件记录（后期）

预留：

```plaintext
order_event_logs
```

用于：

事件追踪与AI分析。

---

# 五、核心设计思想

订单不仅是：

“交易记录”。

更是：

“调度行为记录”。
