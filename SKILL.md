---
name: cheat-on-content
description: 内容创作预测校准循环。把「感觉」变成可校准预测——打分 → 盲预测 → 发布 → T+3d 复盘 → 进化 rubric。支持视频/文章/播客/短文任何可量化内容。**首次使用必须先说"初始化"或"init"。** 触发词：初始化 / 打分 / 预测 / 已发布 / 复盘 / 升级 rubric / 状态 / 找选题 / 抓热点。
allowed-tools: Read, Write, Edit, Glob, Grep, session_status, memory_search, memory_get, cron, web_search, web_fetch
argument-hint: [draft-path] [— mode: cold-start|calibration]
---

# 网红作弊器 / Cheat on Content (OpenClaw 版)

把内容创作变成**可校准预测循环**：打分 → 预测 → 发布 → 复盘 → 进化 rubric。

> **方法论通用**——任何能被量化（播放/阅读/点击）的内容形态都适用。
> 当前内置 rubric：**观点视频**（评论/时评/议题讨论），7 维由参考博主 25+ 样本拟合。

---

## 三条不可妥协原则

**任何一条被违反，整个循环退化为"凭直觉的自我安慰"。**

### 原则 1：盲预测（Blind Prediction）
预测必须在看到任何真实数据**之前**写完。写完后 `## 预测` 段 immutable，只能往 `## 复盘` 追加。
→ 拒绝模式：「帮我预测但先告诉你播放量你反推」

### 原则 2：升级 = 全量重打（Bump = Full Re-score）
rubric 升级时，校准池所有有实绩数据的样本必须用新公式重打分，新排序与实际排序在 ≥4/5 样本上一致才允许升级。

### 原则 3：rubric 是工作台，不是博物馆
被新数据推翻的观察**直接删掉**，不留"我曾经以为 X 但其实..."的考古层。git history 才是档案。

---

## 路由表

| 用户说 | 调用 sub-skill | 前置条件 |
|---|---|---|
| "初始化" / "init" / "首次使用" | `skills/cheat-init/SKILL.md` | 无（这是入口） |
| "找对标" / "学这个账号" / "learn from" | `skills/cheat-learn-from/SKILL.md` | 已 init |
| "找选题" / "我不知道拍什么" / "seed" | `skills/cheat-seed/SKILL.md` | 已 init |
| "打分这篇 [path]" | `skills/cheat-score/SKILL.md` | rubric_notes.md 存在 |
| "启动预测" / "预测" / "给这稿子打分并预测" | `skills/cheat-predict/SKILL.md` | 已 init + 有最终稿 |
| "拍了 X" / "录完了" | `skills/cheat-shoot/SKILL.md` | 对应预测已写 |
| "已发布" / "发布了" / "发布链接是 X" | `skills/cheat-publish/SKILL.md` | 对应预测文件存在 |
| "复盘" / "T+3d 数据来了" | `skills/cheat-retro/SKILL.md` | 预测文件存在 + 已过 RETRO_WINDOW_DAYS |
| "升级 rubric" / "更新公式" | `skills/cheat-bump/SKILL.md` | 校准池 ≥ 5 个样本 |
| "推荐选题" / "next topic" | `skills/cheat-recommend/SKILL.md` | candidates.md 存在且非空 |
| "抓热点" / "今天有什么可做的" | `skills/cheat-trends/SKILL.md` | trend-sources 已配置 |
| "状态" / "看板" | `skills/cheat-status/SKILL.md` | 任意时刻可调 |
| "迁移" / "schema 版本不对" | `skills/cheat-migrate/SKILL.md` | 已 init；版本升级后 |

---

## Mode Detection（模式检测）

1. 检查 `.cheat-state.json` 是否存在 → 不存在 → 强制路由到 `cheat-init`
2. 检查 `predictions/` 下有完整 `## 复盘` 的文件数 → 决定 `mode: cold-start | calibration`
3. 写入 `.cheat-state.json` 的 `mode` 字段后再路由

```
cold-start：< 5 个有真实数据的样本
  → 简化预测，7 维打分 + 一句话 bet，不强求 bucket 数字

calibration：≥ 5 个样本
  → 解锁完整 7 组件预测
```

---

## 项目目录结构（每个 content project）

```
<your-content-project>/
├── .cheat-state.json              # 状态文件（子 skill 共享上下文）
├── rubric_notes.md                # 评分规则的真实来源
├── WORKFLOW.md                     # 5 阶段流程文档
├── STATUS.md                      # 看板（cheat-status 维护）
├── scripts/                        # 拍前的所有草稿
│   └── YYYY-MM-DD_<id>_<short>.md
├── predictions/                    # immutable 预测日志
│   └── YYYY-MM-DD_<id>_<short>.md  # 与 scripts/ 同 id
├── videos/                         # 拍后才建
│   └── YYYY-MM-DD_<id>_<short>/
│       ├── script.md               # 最终拍摄稿
│       └── report.md               # T+3d 数据 + 评论
├── samples/                        # 对标账号分析
│   └── <账号名>/<video-id>/
│       └── meta.md
├── candidates.md                   # 选题池
└── benchmark.md                    # 对标账号信息
```

---

## 子 skill 清单

| Skill | 功能 |
|---|---|
| `cheat-init` | 入口：初始化项目骨架 + rubric |
| `cheat-learn-from` | 导入对标账号，拆 pattern |
| `cheat-seed` | Cold-start 选题启动器 |
| `cheat-score` | 单稿打分（不写文件） |
| `cheat-predict` | 盲预测 + immutable 日志 |
| `cheat-shoot` | 登记拍摄（buffer +1） |
| `cheat-publish` | 发布元数据登记（buffer -1） |
| `cheat-retro` | 数据回收 + 复盘 |
| `cheat-bump` | rubric 升级（含全量重打） |
| `cheat-recommend` | 候选池排序推荐 |
| `cheat-trends` | 热点抓取（日常补充候选池） |
| `cheat-status` | 状态看板（含 buffer 警戒） |
| `cheat-migrate` | schema 升级 |

---

## 预测文件格式（cheat-predict 输出）

```markdown
# 预测：<title>

## 元信息
- 日期：YYYY-MM-DD
- 阶段：predictions
- 模式：cold-start | calibration

## 预测
<!-- 此段 immutable，cheat-retro 前禁止修改 -->

预测播放量：<bucket>
信心指数：<low/medium/high>
锚点：<与哪个已知视频对比>
一句话 bet：<核心假设>

## 评分（cheat-score 输出）
维度1：<score>/10
维度2：<score>/10
...

## 复盘（cheat-retro 填写）
- 实际播放量：<真实数据>
- 预测偏差：<分析>
- rubric 偏差：<评分维度是否需要调整>
- 新观察：<值得加入 rubric 的发现>
```

---

## 评分维度（观点视频 rubric）

| # | 维度 | 说明 |
|---|---|---|
| 1 | 钩子强度 | 前 3 秒能否抓住注意力 |
| 2 | 观点冲击力 | 观点是否鲜明、有辨识度 |
| 3 | 逻辑完整性 | 论证是否自洽、无明显漏洞 |
| 4 | 情绪价值 | 能否引发共鸣或情感反应 |
| 5 | 实用价值 | 看完有没有收获感 |
| 6 | 结构节奏 | 开头/高潮/收尾是否流畅 |
| 7 | 预期管理 | 标题/封面与内容是否匹配 |

---

## 评分等级说明

| 等级 | 分数 | 含义 |
|---|---|---|
| S | 9-10 | 极强，可能成为爆款 |
| A | 7-8 | 强于平均，有传播潜力 |
| B | 5-6 | 中等，稳健但不突出 |
| C | 3-4 | 偏弱，需要改进 |
| D | 1-2 | 明显问题，大概率失败 |

---

## 拒绝场景

以下模式会**直接破坏原则**，无论用户怎么说都拒绝：

- 「帮我预测但先告诉你播放量你来反推」 → 违反原则 #1
- 「跳过校准池重打，直接换公式」 → 违反原则 #2
- 「把历史观察都留着，加时间戳分组」 → 违反原则 #3
- 「删掉这份预测，我想重写」 → 违反原则 #1。写新文件 `_redo.md`，原版必须保留
- 「凭感觉推荐选题」 → 拒绝。本工具不做 gut-feel forecast