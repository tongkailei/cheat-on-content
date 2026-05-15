---
name: cheat-publish
description: 登记内容发布。标记预测对应的内容已发布，buffer -1。触发词："已发布" / "发布了" / "发布链接是"
allowed-tools: Read, Write, Glob, session_status
trigger: "^已发布|^发布了|^发布链接"
---

# Cheat-Publish：发布登记

把 buffer 中的内容标记为"已发布"，记录发布链接和时间。

---

## 前置检查

1. **确认 .cheat-state.json 存在**：不在则路由到 `cheat-init`
2. **确认 buffer 非空**：如果没有待发布内容，告知用户

---

## Step 1：识别要发布的内容

用户可能说：
- "已发布" → 列出 buffer 中的项目供选择
- "发布链接是 https://..." → 提取链接，查找对应的预测文件
- "已发布 https://..." → 同上

如果用户没说具体哪个，按以下优先级处理：
1. 如果 buffer 只有 1 个，直接用它
2. 如果 buffer 多个，列出让用户选择

---

## Step 2：收集发布信息

需要记录：
- **发布链接**：用户提供的 URL
- **发布时间**：如果用户没说，用当前时间
- **平台**：从 URL 推断（抖音/B站/视频号/YouTube/小红书/...）

---

## Step 3：更新预测文件

找到对应的预测文件 `predictions/YYYY-MM-DD_*.md`，追加：

```markdown
## 发布记录

- 发布时间：<YYYY-MM-DD HH:mm>
- 发布链接：<URL>
- 平台：<platform>
```

---

## Step 4：更新 .cheat-state.json

从 buffer 中移除该项：

```json
{
  "lastUpdated": "<当前时间>",
  "lastPublishAt": "<当前时间>",
  "buffer": {
    "count": <-1>,
    "items": [<移除该项>]
  }
}
```

---

## Step 5：更新 STATUS.md

更新 Buffer 区域和"最近发布"区域。

---

## Step 6：设置 T+3d 复盘提醒

用 cron 设置 3 天后的复盘提醒：

```
3 天后提醒复盘：<标题>
- 预测文件：<path>
- 触发词："复盘" 或 "T+3d 数据来了"
```

---

## 输出

```
✅ 已发布！

📁 预测文件：<path>
🔗 链接：<URL>
📅 发布时间：<YYYY-MM-DD HH:mm>
⏰ 3 天后复盘，届时说"复盘"或"复盘 <标题>"

💡 提示：复盘时需要抓取真实数据（播放量、点赞、评论等）
   说"复盘"后我会引导你收集这些数据
```

---

## 特殊场景

### 用户先说"拍了"再说"已发布"
"拍了"会调用 `cheat-shoot`（buffer +1），"已发布"是确认发布（buffer -1）。两个都做才是完整流程。

### 用户跳过"拍了"直接说"已发布"
可以接受，但提示用户应该养成"拍了 → 已发布"的习惯，方便追踪。

### 没有对应预测文件
告知用户：只有在 `cheat-predict` 之后才能复盘，没有预测就没法对比。询问是否要补一个预测。