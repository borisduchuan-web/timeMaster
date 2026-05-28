# 信誉模型（Reputation Model）

信誉系统用于：

建立平台信任。

---

# 一、信誉目标

系统需要判断：

* 谁更可靠
* 谁更稳定
* 谁更值得优先调度

---

# 二、核心信誉指标

---

## 服务评分

```plaintext
average_rating
```

---

## 完成率

```plaintext
completion_rate
```

---

## 取消率

```plaintext
cancel_rate
```

---

## 投诉率

```plaintext
complaint_rate
```

---

## 响应速度

```plaintext
average_response_time
```

---

# 三、信誉等级

系统动态生成：

```plaintext
信誉等级
```

例如：

* Lv1
* Lv2
* Lv3

---

# 四、信誉用途

信誉数据影响：

* 调度优先级
* 推荐排序
* 可接任务等级

---

# 五、新用户机制（关键🔥）

系统避免：

新用户完全无法接单。

因此：

会提供：

* 新手任务
* 低风险任务
* 成长型推荐

---

# 六、未来扩展（预留）

未来可能增加：

* AI信誉分析
* 多维行为信用
* 风险预测

当前阶段：

采用规则信誉系统。
