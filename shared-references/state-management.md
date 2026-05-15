# 状态管理 / State Management

## .cheat-state.json 结构

```json
{
  "schemaVersion": "1.0.0",
  "mode": "cold-start | calibration",
  "createdAt": "<ISO8601>",
  "lastUpdated": "<ISO8601>",
  "projectDir": "<绝对路径>",
  "buffer": {
    "count": 0,
    "items": [
      {
        "id": "<YYYY-MM-DD_id>",
        "title": "<标题>",
        "predictedAt": "<ISO8601>",
        "shootAt": "<ISO8601> 或 null"
      }
    ]
  },
  "calibration": {
    "totalSamples": 0,
    "lastBumpAt": "<ISO8601> 或 null",
    "lastRetroAt": "<ISO8601> 或 null"
  },
  "candidates": []
}
```

---

## 字段说明

### schemaVersion

当前支持 `1.0.0`。升级时执行 `cheat-migrate`。

### mode

| 模式 | 条件 | 预测格式 |
|---|---|---|
| `cold-start` | < 5 个校准样本 | 简化版（7维 + 一句话 bet） |
| `calibration` | ≥ 5 个校准样本 | 完整版（7维 + bucket + 锚点） |

### buffer

**已拍未发**的内容队列。

- `count`：队列长度
- `items`：具体内容列表
- `shootAt`：拍摄时间（null = 只预测了还没拍）

**Buffer 警戒**：
- 0 个：正常
- 1-3 个：警戒
- > 3 个：危险，建议先消化

### calibration

- `totalSamples`：有完整复盘数据的样本数
- `lastBumpAt`：最后一次 rubric 升级时间
- `lastRetroAt`：最后一次复盘时间

---

## 读写约定

### 读取

1. Skill 启动时读取 `.cheat-state.json`
2. 解析 `projectDir` 得到项目根目录
3. 所有相对路径都基于 `projectDir`

### 写入

1. 任何状态变更前，先读取当前文件
2. 变更后立即写回
3. 写回前备份：`cp .cheat-state.json .cheat-state.json.backup`

### 错误处理

```javascript
try {
  const state = JSON.parse(readFile('.cheat-state.json'));
} catch (e) {
  // 文件不存在或格式错误
  // 路由到 cheat-init 重新初始化
}
```

---

## 文件锁定

当 skill 正在写入 `.cheat-state.json` 时，使用临时文件 + 原子替换：

```bash
# 写入流程
cp .cheat-state.json .cheat-state.json.tmp
# 修改 .cheat-state.json.tmp
mv .cheat-state.json.tmp .cheat-state.json
```

这样可以避免并发写入导致数据损坏。

---

## 备份与恢复

### 自动备份

每次写入前备份：
```
.cheat-state.json.backup.<timestamp>
```

### 手动恢复

```bash
cp .cheat-state.json.backup.<timestamp> .cheat-state.json
```

### 验证恢复

恢复后检查：
1. JSON 格式是否 valid
2. schemaVersion 是否正确
3. 必要字段是否存在