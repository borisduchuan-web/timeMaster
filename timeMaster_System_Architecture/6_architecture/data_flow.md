# 数据流转（Data Flow）

系统核心是：

“事件驱动的实时调度流”。

---

# 一、工作模式切换流（核心🔥）

用户开启：

“开始接单”

客户端
→ API
→ User Module
→ Redis 更新 work_mode
→ 调度系统实时生效

---

# 二、任务发布流

用户发布任务：

客户端
→ API
→ Task Module
→ MySQL
→ 调度中心

---

# 三、实时调度流

调度系统：

1. 获取任务
2. 获取在线用户
3. 过滤工作模式用户
4. 计算技能匹配
5. 计算距离
6. 生成候选列表
7. 推送任务

---

# 四、抢单流

服务者抢单：

客户端
→ API
→ Redis 分布式锁
→ Order Module
→ 创建订单

防止：

* 重复抢单
* 并发问题

---

# 五、订单状态流

状态变化：

待匹配
→ 已推送
→ 已接单
→ 服务中
→ 已完成

状态同步：

* MySQL
* Redis
* WebSocket

---

# 六、实时状态流（核心🔥）

系统实时维护：

* online_status
* work_mode
* current_location
* current_load

调度系统优先读取 Redis。

---

# 七、消息通知流

任务变化：

→ Message Module
→ Push Service
→ App客户端

---

# 八、未来AI数据流（预留）

行为数据：

→ Event Stream
→ AI分析层
→ 推荐优化

当前阶段仅记录事件。
