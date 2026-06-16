# Card Style Guide

选择组件组合和视觉样式的决策指南。字段写法见 `card-2.0-schema.md`。

---

## 意图 → 组件组合

### 通知类（无交互或只读）

| 用户意图 | 推荐组件组合 | header.template |
|---|---|---|
| 纯文字通知 / 系统公告 | `markdown` + `hr` + `button(open_url)` | `blue` |
| 活动公告（带主视觉图） | `img`（主图）+ `markdown`（时间/地点）+ `column_set`（详情对）+ `button(open_url)` | `turquoise` / `blue` |
| 成功 / 完成状态通知 | `column_set`（关键字段对齐）+ `markdown`（结论）+ `hr` | `green` |
| 审批结果反馈（已通过 / 已拒绝） | `column_set`（申请信息）+ `hr` + `markdown`（审批结论 + icon 状态标识） | `green` / `red` |
| 生日 / 节日祝福 | `img`（主图）+ `column_set`（人名/日期）+ `hr` + `button(open_url)` | `orange` |
| 产品 / 功能上线推广 | `img`（主图）+ `markdown`（亮点）+ `div`（功能列表）+ `button(open_url)` | `blue` / `violet` |
| 多图展示（图集、AI 生成图） | `img_combination` 或 多个 `img` + `markdown`（说明）+ `button(callback)` | `default` |

### 提醒 + 操作类

| 用户意图 | 推荐组件组合 | header.template |
|---|---|---|
| 提醒 + 一键操作 | `markdown`（详情）+ `button(callback)` 单按钮 | `yellow` |
| 告警触发（需立即处理） | `column_set`（告警指标）+ `markdown`（描述）+ `input`（快速备注）+ `button(callback)` | `red` |
| 告警已解决 / 状态变更 | `column_set`（解决时间 / 负责人）+ `markdown`（结论） | `green` |
| 审批待处理（含备注输入） | `column_set`（申请信息）+ `input`（审批意见）+ `button(callback)` × 2（通过 / 拒绝） | `default` |
| 日历 / 日程提醒（含参与人） | `column_set`（时间 / 地点）+ `person_list`（参与人）+ `button(callback)` | `yellow` |
| 危险操作确认 | `markdown`（说明）+ `button(callback)` + `confirm` 弹窗配置 | `red` |

### 数据 / 报告类

| 用户意图 | 推荐组件组合 | header.template |
|---|---|---|
| 日报 / 工作汇报 | `column_set` 多列指标 + `markdown`（进展）+ `hr` 分段 | `blue` / `default` |
| 数据看板（含图表） | `chart` + `table` + `column_set`（指标）+ `markdown`（说明）| `blue` |
| 排行榜 | `column_set` 固定列宽（序号 + 头像 `img` + 名字 + 指标）循环条目 | `grey` |
| 订单 / 工单详情 | `column_set` 多行字段对（label + value）+ `hr` + `button(callback)` | `orange` |

### 表单 / 收集类

| 用户意图 | 推荐组件组合 | header.template |
|---|---|---|
| 纯文字表单收集 | `form`（内含 `input` + `button(form_action_type: submit)`） | `blue` |
| 带下拉选择的表单 | `form`（内含 `select_static` / `select_person` + `input` + `button`） | `wathet` |
| 设备 / 服务反馈 | `form`（内含 `select_static`（满意度）+ `input`（备注）+ `button`） | `yellow` |
| 多步骤进度 / 引导 | `column_set` 横向步骤 + `markdown`（当前状态）+ `button` | `blue` |

### 推荐 / 选择类

| 用户意图 | 推荐组件组合 | header.template |
|---|---|---|
| 推荐列表（带图卡片，可点击） | `interactive_container`（内含 `img` + `markdown`）× N + `button(open_url)` | `blue` |
| AI 引导选项 / 功能菜单 | `markdown`（欢迎语）+ `interactive_container`（内含 `markdown` 选项说明）× N | 无 header |
| Bot 功能引导 / 教程 | `markdown`（步骤说明）+ `hr` + `button` × 2（主操作 / 次操作） | `blue` |
| 服务台 / 多操作入口 | `markdown`（说明）+ `button` × N（各类操作，`type` 区分主次） | 无 header |

### 社交 / 互动类

| 用户意图 | 推荐组件组合 | header.template |
|---|---|---|
| 工作圈 / 社交分享 | `img_combination`（多图）+ `markdown`（正文）+ `button(open_url)` × 2 | `blue` |
| 成交 / 业绩公告 | `img`（庆祝图）+ `markdown`（成绩）+ `column_set`（关键数字） | `green` |
