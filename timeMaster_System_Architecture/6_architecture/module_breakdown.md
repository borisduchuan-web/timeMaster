# 模块拆分（Module Breakdown）

系统采用：

“统一用户模型 + 模块化架构”。

---

# 一、用户模块（User Module）

系统核心基础模块。

---

## 职责

* 用户注册
* 登录认证
* 身份信息
* 技能管理
* 工作模式管理
* 在线状态管理

---

## 核心设计

用户只有一个身份：

User。

是否接单：

由“工作模式”决定。

---

## 核心状态

* online_status
* work_mode
* availability
* current_load

---

# 二、任务模块（Task Module）

职责：

* 发布任务
* 编辑任务
* 取消任务
* 管理任务状态

---

## 核心字段

* priority
* service_type
* start_time
* location

---

# 三、订单模块（Order Module）

职责：

* 接单
* 抢单
* 状态流转
* 完成确认

---

# 四、调度模块（Scheduling Module）【核心🔥】

系统核心模块。

---

## 职责

* 匹配服务者
* 实时调度
* 优先级计算
* 任务广播

---

## 调度依据

系统实时计算：

* 技能
* 时间
* 距离
* 工作模式
* 在线状态
* 当前负载

---

# 五、状态同步模块（Presence Module）

专门维护：

* 在线状态
* 工作状态
* 地理位置
* 心跳状态

这是实时调度基础。

---

# 六、消息模块（Message Module）

职责：

* 推送通知
* 抢单通知
* 状态同步
* 聊天

---

# 七、支付模块（Payment Module）

职责：

* 支付
* 分账
* 提现
* 退款

---

# 八、评价模块（Reputation Module）

职责：

* 服务评分
* 用户信誉
* 历史行为记录

---

# 九、风控模块（Risk Control Module）

职责：

* 异常检测
* 虚假订单识别
* 作弊识别

---

# 十、后台管理模块（Admin Module）

职责：

* 用户审核
* 调度监控
* 数据统计
* 风险处理

---

# 十一、未来扩展模块（Future Modules）

预留：

* 数字人系统
* AI行为分析
* 智能推荐
* 硬件接入
