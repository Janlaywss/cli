# 发送 Interactive 卡片工作流

用户需要发送一张飞书互动卡片时，遵循本工作流。每次都必须严格按步骤执行。

---

## Step 1：分析意图，输出设计方案

**目标**：在动手写 JSON 之前，先明确所有决策并告知用户。Step 2 的文档加载量取决于这里的组件列表，所以要尽量在这一步想清楚。

分析以下内容并向用户简要说明：

1. **版本**：Card 2.0 支持的组件更丰富，**推荐使用 Card 2.0**；仅当用户明确要求 1.0 时才用 1.0。
2. **组件组合**：在 `lark-im-card-style.md` 「意图 → 组件组合」表里匹配最接近的意图行，参考推荐组件组合和该行的 `header.template` 颜色（部分行为"无 header"）。推荐组合仅供参考，**最终选型以符合用户意图为准**；使用 Card 2.0 时，可同时参考 `card-2.0-schema.md` 中的组件概述来补充或调整组件选择。
3. **交互类型**（若有）：是否含会回调服务端的交互组件，以及是否有纯跳转（open_url）。回调分两类：① `select` / `multi_select` / `input` / `picker` / `overflow` 操作即默认回调；② `button` / `checker` / `interactive_container` 需显式配置 `behaviors`；`form` 提交统一回调。细则见 Step 5。

> 输出示例："Card 2.0，header green，组件：`column_set` / `column` / `markdown` / `hr`，无交互。"

---

## Step 2：按需加载组件文档

> ⚠️ **仅 Card 2.0 适用**：`card-2.0-schema.md`、`components/` 明细、`examples/` 都是 2.0 结构。若 Step 1 定为 **Card 1.0**（含 Step 4 降级场景），这些**不可参考**，跳过本步，直接按 1.0 结构构造。

**目标**：只读 Step 1 列出的组件对应的明细文件（同级 `components/` 目录），不全量加载。

1. 阅读 `card-2.0-schema.md` —— 同时满足两个目的：① 了解组件概述，辅助 Step 1 的组件选型；② 找到各组件的明细文档路由链接。**仅读一次，不重复加载。**
2. 按路由逐个读取 `components/<tag>.md`（如 `components/column_set.md`、`components/button.md`）
3. 在本文件同级的 `examples/` 目录找 1～2 个与当前场景相似的 JSON 文件，读取后作为结构参考

```bash
ls examples/   # 相对本文件所在目录；只读最相似的 1～2 个
```

---

## Step 3：构造卡片 JSON

按 Step 2 中对应版本的根结构骨架构造卡片，组件选型遵循 Step 1 的设计方案。

- Card 2.0 必须有 `"schema": "2.0"`，否则卡片不渲染
- `form` 容器内按钮用 `form_action_type: "submit"`，不写 `behaviors`
- `column_set` 的子节点只能是 `column`，不能直接放其他组件

---

## Step 4：发送卡片

```bash
# 发送到群聊
lark-cli im +messages-send --chat-id oc_xxx --msg-type interactive --content '<card_json>'

# 发送给指定用户（私聊）
lark-cli im +messages-send --user-id ou_xxx --msg-type interactive --content '<card_json>'
```

**发送失败时**：先对照下方常见失败列表排查，若能匹配则按对应处理方式修复后重新发送；否则根据错误信息修复 JSON 后重新发送。最多尝试 **3 次**。若 3 次后仍失败，**降级为 Card 1.0 卡片**重新构造并发送。**不参考之前发送 2.0 的记忆**，完全根据用户意图重新构造 1.0 卡片。1.0 无本地参考文档（components/、examples/ 均为 2.0）。
**常见失败列表**

| # | 错误信息 | 处理方式 |
|---|---|---|
| 1 | `there is an invalid user resource (at/person) in your card` | 卡片中含有 at/person 组件，但使用了无效的用户 ID。询问用户其真实的 open_id / user_id，替换后重新发送。 |

---

## Step 5：交互回调（可选）

若卡片含**会回调服务端的交互组件**，则**支持**监听 `card.action.trigger` 回调（是否监听由实际需求决定，非必须）：

**需显式配置 `behaviors: [{type:"callback"}]` 才会回调：**
- `button`（带 callback behavior）
- `checker` —— 未配置 behaviors 时仅本地勾选生效，不触发服务端回调
- `interactive_container` —— behaviors 为必填，支持 callback / open_url

**选中 / 输入即默认回调，无需显式 `behaviors`：**
- `select_static` / `multi_select_static` / `select_person` / `multi_select_person`
- `overflow` / `input` / `date_picker` / `picker_time` / `picker_datetime`

**form 提交统一回调（按钮用 `form_action_type: "submit"`，无需 behaviors）：**
- form 内所有表单组件的值通过 `action.form_value` 一次性回传

> 纯 `open_url` 跳转按钮在客户端本地跳转，不回调服务端。

如需处理回调（监听事件、读取字段、更新卡片），见 `lark-im-card-action-reply.md`。

---

## 执行清单

- [ ] Step 1：分析意图，输出设计方案（版本 / 颜色 / 组件）
- [ ] Step 2：读 schema.md + 相关 example
- [ ] Step 3：构造 JSON，核查常见错误
- [ ] Step 4：发送，失败则 debug 直到成功
- [ ] Step 5：若有交互，参考 card-action-reply.md
