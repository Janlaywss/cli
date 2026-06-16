# 卡片 2.0 组件大纲

Card 2.0 组件按**容器 / 展示 / 交互**三类，均通过 `tag` 字段声明。先在下表按用途选组件，再点明细看字段：有明细文件的点 `components/<tag>.md`（完整字段+示例+易错点），低频组件点链接看官方文档。

## 容器类（布局 / 组织交互）

| 组件 | 用途 |
|---|---|
| [column_set](components/column_set.md) | 横向分栏，多列图文对齐（数据表、字段对、列表） |
| [collapsible_panel](components/collapsible_panel.md) | 折叠面板，收纳备注/长文本等次要信息 |
| [form](components/form.md) | 表单容器，批量录入表单项后一次提交 |
| [interactive_container](components/interactive_container.md) | 整块可点击区域，可统一定义样式与交互 |
| [循环容器](components/recycling_container.md) | 批量渲染同版式不同数据（仅搭建工具） |

## 展示类（无交互）

| 组件 | 用途 |
|---|---|
| [header](components/header.md) | 卡片标题区：主/副标题、后缀标签、主题色 |
| [div](components/div.md) | 普通文本，带前缀图标、字段对 |
| [markdown](components/markdown.md) | 富文本，最常用；@人、彩色、链接、列表、表格等 |
| [img](components/img.md) | 单图 |
| [img_combination](components/img_combination.md) | 多图拼排（双图/三图/宫格） |
| [person](components/person.md) | 单个人员头像/姓名 |
| [person_list](components/person_list.md) | 多个人员头像/姓名 |
| [chart](components/chart.md) | VChart 图表（折线/柱/饼/词云等） |
| [table](components/table.md) | 多列数据表（只能放根节点） |
| [hr](components/hr.md) | 分割线 |

## 交互类

| 组件 | 用途 |
|---|---|
| [button](components/button.md) | 按钮：回调 / 跳转 / 表单提交 |
| [input](components/input.md) | 文本输入框（多嵌在 form 内） |
| [overflow](components/overflow.md) | 折叠按钮组，收纳多个操作 |
| [select_static](components/select_static.md) | 下拉单选 |
| [multi_select_static](components/multi_select_static.md) | 下拉多选 |
| [select_person](components/select_person.md) | 人员单选 |
| [multi_select_person](components/multi_select_person.md) | 人员多选 |
| [date_picker](components/date_picker.md) | 日期选择器 |
| [picker_time](components/picker_time.md) | 时间选择器 |
| [picker_datetime](components/picker_datetime.md) | 日期时间选择器 |
| [select_img](components/select_img.md) | 图片选择（单/多选） |
| [checker](components/checker.md) | 勾选器，任务勾选回调 |
