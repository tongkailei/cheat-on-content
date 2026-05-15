---
name: cheat-init
description: 初始化内容创作预测项目。创建 rubric_notes.md、WORKFLOW.md、STATUS.md、.cheat-state.json 等项目骨架。如果项目目录已存在，询问用户是新建还是追加。
allowed-tools: Read, Write, Glob, session_status
trigger: "^初始化|^init|^首次使用"
---

# Cheat-Init：初始化项目

检测用户当前目录结构，判断是否已有 cheat-on-content 项目。

## 判断逻辑

1. **如果 `.cheat-state.json` 已存在**：
   - 读取 `mode` 字段
   - 告诉用户项目已初始化，mode 是 cold-start 还是 calibration
   - 询问是否要查看状态（`/cheat-status`）还是重新初始化（会警告数据风险）

2. **如果 `.cheat-state.json` 不存在**：
   - 执行初始化流程

---

## 初始化流程

### Step 1：确认项目目录

询问用户：

```
📁 初始化项目

请告诉我你要在哪个目录初始化（可以是已有目录或新建目录）：

方式 1：指定路径，如 ~/my-channel 或 C:\Users\xxx\my-channel
方式 2：说"这里"，在当前工作目录初始化
```

如果用户说"这里"或类似表述，用当前工作目录。

---

### Step 2：创建目录结构

在目标目录下创建：

```
<project-dir>/
├── .cheat-state.json
├── rubric_notes.md
├── WORKFLOW.md
├── STATUS.md
├── scripts/
├── predictions/
├── videos/
├── samples/
└── benchmark.md
```

---

### Step 3：初始化 .cheat-state.json

```json
{
  "schemaVersion": "1.0.0",
  "mode": "cold-start",
  "createdAt": "<当前时间 ISO>",
  "lastUpdated": "<当前时间 ISO>",
  "projectDir": "<实际路径>",
  "buffer": {
    "count": 0,
    "items": []
  },
  "calibration": {
    "totalSamples": 0,
    "lastBumpAt": null
  },
  "candidates": []
}
```

---

### Step 4：初始化 rubric_notes.md

写入观点视频的 7 维 rubric：

```markdown
# 评分规则 / Rubric Notes

## 观点视频评分维度

| # | 维度 | 权重 | 评分标准 |
|---|---|---|---|
| 1 | 钩子强度 | 20% | 前 3 秒能否抓住注意力 |
| 2 | 观点冲击力 | 20% | 观点是否鲜明、有辨识度 |
| 3 | 逻辑完整性 | 15% | 论证是否自洽、无明显漏洞 |
| 4 | 情绪价值 | 15% | 能否引发共鸣或情感反应 |
| 5 | 实用价值 | 10% | 看完有没有收获感 |
| 6 | 结构节奏 | 10% | 开头/高潮/收尾是否流畅 |
| 7 | 预期管理 | 10% | 标题/封面与内容是否匹配 |

## 评分等级

| 等级 | 分数 | 含义 |
|---|---|---|
| S | 9-10 | 极强，可能成为爆款 |
| A | 7-8 | 强于平均，有传播潜力 |
| B | 5-6 | 中等，稳健但不突出 |
| C | 3-4 | 偏弱，需要改进 |
| D | 1-2 | 明显问题，大概率失败 |

## 加权公式

```
composite = sum(dimension_score * dimension_weight)
```

- S 级（≥9）：值得重点押注
- A 级（≥7）：值得发布
- B 级（5-6）：可以发但别期待太高
- C/D 级（<5）：需要重大修改或放弃

## 冷启动说明

当前处于 cold-start 模式（< 5 个校准样本），预测简化为：
- 7 维打分 + 一句话 bet
- 不强求 bucket 数字（避免 false precision）

## 观察笔记（待积累校准数据后更新）

<!-- 用复盘数据迭代这里 -->

```

---

### Step 5：初始化 WORKFLOW.md

```markdown
# 工作流 / Workflow

## 5 阶段闭环

```
打分 ──→ 盲预测 ──→ 发布 ──→ T+3d 复盘 ──→ 进化 rubric
```

## 阶段说明

### 1. 打分（/cheat-score）
用 rubric 对草稿打 7 维分数，不写文件，输出结果。

### 2. 盲预测（/cheat-predict）
**必须在看到任何真实数据之前写完**。
预测文件写入 `predictions/` 目录，`## 预测` 段 immutable。

### 3. 发布（/cheat-publish）
登记发布，buffer -1。

### 4. T+3d 复盘（/cheat-retro）
3 天后抓取真实数据，对比预测与实际，更新 rubric 笔记。

### 5. 升级 rubric（/cheat-bump）
当校准池 ≥ 5 个样本后，可用新数据更新评分公式。

## 状态命令

- `状态` → /cheat-status 查看看板
- `找选题` → /cheat-seed 冷启动选题
- `抓热点` → /cheat-trends 日常补充候选池

## 三大原则

1. **盲预测**：预测在看到数据前写完，写完不可改
2. **全量重打**：rubric 升级必须用新公式重打所有样本
3. **工作台非博物馆**：被推翻的观察直接删掉
```

---

### Step 6：初始化 STATUS.md

```markdown
# 状态看板 / Status

## Buffer（待发布）

- 数量：0
- 项目：-

## 校准池

- 样本数：0
- 最后升级：-

## 候选池

- 数量：0
- 最近更新：-

## 最近预测

（暂无预测记录）
```

---

### Step 7：初始化 benchmark.md

```markdown
# 对标账号 / Benchmark

## 已导入账号

（暂无对标账号，说"找对标"或"learn from <账号名>"开始导入）
```

---

## 完成输出

初始化完成后，告诉用户：

```
✅ 初始化完成！

项目目录：<project-dir>
模式：cold-start（< 5 个校准样本，预测简化）

下一步：
1. "找对标" → 导入对标账号（强烈建议）
2. "打分这篇 <草稿路径>" → 开始打分
3. "找选题" → 冷启动选题

三大原则：
• 盲预测：预测必须先于数据写完，写完不可改
• 全量重打：rubric 升级要重打所有样本
• 工作台非博物馆：被推翻的观察直接删掉
```

---

## 注意事项

- 如果目标目录已存在文件，**不覆盖**，只创建缺失项
- rubric_notes.md 如果已存在，保留原内容，只在末尾追加缺失部分
- .cheat-state.json 总是覆盖（确保 schema 最新）