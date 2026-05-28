# 用户模型（User Model）

系统采用：

“统一用户模型 + 动态角色”

设计。

用户只有一个身份：

User。

是否接单：

由工作状态决定。

---

# 一、核心目标

系统不仅记录：

“用户是谁”，

还记录：

* 用户会什么
* 用户什么时候有空
* 用户当前是否可调度

---

# 二、核心用户结构

---

## 基础信息

```plaintext
user_id
nickname
avatar
gender
birthday
phone
```

---

## 身份状态

```plaintext
实名认证状态
认证等级
账号状态
```

---

## 动态角色状态（核心🔥）

```plaintext
work_mode
online_status
current_load
```

说明：

* work_mode：是否开启接单
* online_status：是否在线
* current_load：当前任务负载

---

## 技能能力数据（核心🔥）

```plaintext
skill_tags
capability_level
skill_experience
```

说明：

系统不仅记录：

“会不会”，

还记录：

“熟练程度”。

---

## 时间数据（核心🔥）

```plaintext
availability_schedule
preferred_work_time
```

说明：

时间是系统核心资源。

---

## 地理数据

```plaintext
current_location
service_radius
home_city
```

---

## 信誉数据

```plaintext
rating
complete_rate
cancel_rate
complaint_count
```

---

## 收入数据

```plaintext
wallet_balance
total_income
withdraw_status
```

---

# 三、用户行为数据（后期）

预留：

```plaintext
behavior_tags
preference_tags
activity_patterns
```

当前阶段仅预留。

---

# 四、核心设计思想

用户模型核心不是：

“静态身份”。

而是：

“动态能力 + 动态状态”。

---

# 五、未来扩展（预留）

未来可能扩展：

* 数字人画像
* AI能力分析
* 多维行为模型

当前阶段不实现。
