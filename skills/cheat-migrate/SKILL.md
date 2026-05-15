---
name: cheat-migrate
description: Schema 迁移。当 skill 版本升级后，更新项目的状态文件结构。触发词："迁移" / "schema 版本不对" / "migrate"
allowed-tools: Read, Write, Glob, session_status
trigger: "^迁移|^schema|^版本不对|^migrate"
---

# Cheat-Migrate：Schema 迁移

当 cheat-on-content skill 升级后，更新项目的 `.cheat-state.json` 和相关文件。

---

## 前置检查

1. **确认 .cheat-state.json 存在**
2. 读取 `schemaVersion` 字段
3. 与当前 skill 支持的 schema 版本对比

---

## 迁移逻辑

| 当前版本 | → 目标版本 | 迁移内容 |
|---|---|---|
| 1.0.0 | 1.1.0 | 新增 candidates 数组、calibration 对象 |
| 1.1.0 | 1.2.0 | 新增 buffer.items 结构变更 |
| ... | ... | ... |

---

## 迁移步骤

### Step 1：检测是否需要迁移

读取 `.cheat-state.json`：

```json
{
  "schemaVersion": "1.0.0",
  ...
}
```

如果 `schemaVersion` < 当前 skill 支持的版本，执行迁移。

---

### Step 2：备份

在执行迁移前，先备份原文件：

```
.cheat-state.json → .cheat-state.json.backup.<timestamp>
```

---

### Step 3：执行迁移

根据版本差异，执行对应的迁移脚本。

### Step 4：验证

读取新文件，确保：
- schemaVersion 已更新
- 所有必要字段存在
- 数据完整性未破坏

---

## 输出

```
✅ 迁移完成！

📁 文件：.cheat-state.json
迁移：<旧版本> → <新版本>
备份：<备份文件路径>

🔍 验证通过

⚠️ 注意：
- 如有问题，可以回滚：cp <备份文件> .cheat-state.json
- 建议重启当前 session
```

---

## 常见问题

### schemaVersion 不存在（旧版格式）

执行 v1.0.0 迁移，把旧格式转换为新格式。

### 迁移失败

保留备份，让用户手动处理或联系 skill 维护者。