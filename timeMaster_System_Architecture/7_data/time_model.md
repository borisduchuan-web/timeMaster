# 时间模型（Time Model）

时间不是普通字段，

而是：

系统核心资源。

---

# 一、核心目标

系统需要理解：

* 谁什么时候有空
* 任务什么时候需要执行
* 时间是否冲突
* 调度是否可行

---

# 二、用户时间模型

---

## 可用时间

```plaintext
availability_slots
```

示例：

* 周一 18:00~22:00
* 周末全天

---

## 工作偏好时间

```plaintext
preferred_work_time
```

例如：

* 夜间优先
* 周末优先

---

## 实时状态时间

```plaintext
last_online_time
current_working_until
```

---

# 三、任务时间模型

---

## 时间窗口

```plaintext
start_time
end_time
```

---

## 紧急程度

```plaintext
priority_level
```

包括：

* 延时
* 实时
* 紧急

---

## 响应时间要求

```plaintext
max_response_time
```

---

# 四、调度时间模型（核心🔥）

系统实时计算：

---

## 是否时间冲突

---

## 是否能准时到达

---

## 当前是否有空闲窗口

---

## 当前任务负载

---

# 五、未来扩展（预留）

未来可能增加：

* AI时间预测
* 行为习惯学习
* 自动时间优化

当前阶段：

采用规则计算。

---

总结：

时间是系统最核心的调度维度。
