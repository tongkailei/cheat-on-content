---
name: cheat-shoot
description: 登记拍摄完成。预测已拍完但还没发布，buffer +1。触发词："拍了" / "录完了" / "拍完了"
allowed-tools: Read, Write, Glob, session_status
trigger: "^拍了|^录完了|^拍完了|^shot"
---

# Cheat-Shoot：拍摄登记

把预测标记为"已拍完待发布"，buffer +1。

**注意**：这是"拍了但没发布"的状态，不是"已发布"。

---

## 前置检查

1. **确认 .cheat-state.json 存在**
2. **确认有对应的预测文件**：找到用户指定的预测文件

---

## Step 1：识别内容

用户说"拍了 <标题>"或"拍了"，需要找到对应的预测文件。

优先级：
1. 用户明确指定预测标题 → 模糊匹配
2. buffer 中唯一项 → 直接用
3. 列出供选择

---

## Step 2：确认拍摄稿

询问用户最终拍摄稿是否和 `scripts/` 里的草稿一致：

```
📹 拍摄登记

确认：最终拍摄稿和 <草稿路径> 一致吗？

1. 是，和草稿一致
2. 否，有修改（请提供最终稿路径或直接粘贴内容）
```

如果用户说"有修改"，让用户提供新稿子路径，并更新 `videos/<id>/script.md`。

---

## Step 3：创建 videos 目录

```
videos/
└── YYYY-MM-DD_<id>_<short>/
    ├── script.md        # 拍摄稿（cheat-publish 时或现在写入）
    └── report.md        # T+3d 复盘数据（cheat-retro 时写入）
```

---

## Step 4：更新 .cheat-state.json

```json
{
  "lastUpdated": "<当前时间>",
  "lastShootAt": "<当前时间>",
  "buffer": {
    "count": <+1>,
    "items": [<追加新项>]
  }
}
```

---

## Step 5：输出

```
📹 已登记拍摄！

📁 预测文件：<path>
📁 视频目录：<videos/.../script.md>
📦 Buffer：+1（当前共 <n> 个待发布）

⏰ 拍完后说"已发布"（或"发布链接是 <url>"）
📅 发布后 3 天说"复盘"
```

---

## 注意事项

- 区分"拍了"和"发布了"：拍了是 buffer +1，发布是 buffer -1
- 如果用户跳过"拍了"直接说"已发布"，接受但不更新 videos/ 目录
- 拍摄稿用 script.md 保存，方便后续复盘对比