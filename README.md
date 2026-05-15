# cheat-on-content

**内容创作预测校准循环** — 把「感觉」变成可校准的预测。

> 把内容创作从「凭直觉」变成「可量化 → 可预测 → 可复盘 → 可进化」的闭环系统。支持视频/文章/播客/短文案任何可量化内容形态。

---

## 核心理念

内容创作本质上是**预测问题**：
- 发布前：预测播放量 / 互动率
- 发布后：用真实数据校准预测能力
- 多次循环后：rubric（评分规则）越来越准，预测越来越接近现实

**不是帮你想选题，而是帮你校准「好选题长什么样」的直觉。**

---

## 三条不可妥协原则

### 原则 1：盲预测（Blind Prediction）
预测必须在看到任何真实数据**之前**写完。写完后 `## 预测` 段 immutable，只能往 `## 复盘` 追加。
- ❌ "先告诉你实际播放量，你反推评分"
- ✅ 写完预测 → 发布 → 等 3 天 → 复盘

### 原则 2：升级 = 全量重打（Bump = Full Re-score）
rubric 升级时，校准池所有有实绩数据的样本必须用新公式重打分，新排序与实际排序在 ≥4/5 样本上一致才允许升级。

### 原则 3：rubric 是工作台，不是博物馆
被新数据推翻的观察**直接删掉**，不留考古层。git history 才是档案。

---

## 快速开始

### 首次使用

```
你：初始化 / init
→ 调用 cheat-init，创建项目骨架 + 默认 rubric（观点视频 7 维）
```

### 日常流程

| 场景 | 你说 | 系统做 |
|------|------|--------|
| 找选题 | `找选题` / `seed` | 冷启动选题提案 |
| 对标学习 | `学这个账号 @xxx` | 拆解账号爆款 pattern |
| 打分草稿 | `打分这篇 [path]` | 7 维度评分（不写文件） |
| 盲预测 | `预测` / `启动预测` | 写 immutable 预测日志 |
| 拍摄完成 | `拍了 X` / `录完了` | 更新 buffer 计数 |
| 发布上线 | `已发布` / `发布链接是 X` | 登记发布元数据 |
| 3 天后复盘 | `复盘` | 回收数据，分析偏差，升级 rubric |
| 查看状态 | `状态` / `看板` | 展示 buffer / 预测 / 候选池状态 |

---

## 项目结构

```
<content-project>/
├── .cheat-state.json          # 全局状态（子 skill 共享）
├── rubric_notes.md            # 评分规则（真实来源）
├── STATUS.md                  # 看板（buffer 警戒线）
├── WORKFLOW.md                # 5 阶段流程文档
├── scripts/                   # 拍前草稿
├── predictions/               # 预测日志（immutable）
├── videos/                    # 拍后素材 + 数据报告
├── samples/                   # 对标账号分析
├── candidates.md              # 选题候选池
└── benchmark.md              # 对标账号信息
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

**评分等级：S(9-10) / A(7-8) / B(5-6) / C(3-4) / D(1-2)**

---

## 模式说明

系统有两种运行模式，根据你的校准池样本数量自动切换：

- **cold-start（< 5 个有真实数据的样本）**
  → 简化预测：7 维打分 + 一句话 bet，不强求 bucket 数字

- **calibration（≥ 5 个样本）**
  → 解锁完整 7 组件预测：播放量 bucket + 信心指数 + 锚点对比 + 一句话 bet

---

## 子 skill 清单

| Skill | 触发词 | 功能 |
|-------|--------|------|
| `cheat-init` | 初始化 / init | 入口：初始化项目骨架 + rubric |
| `cheat-learn-from` | 学这个账号 / learn from | 导入对标账号，拆 pattern |
| `cheat-seed` | 找选题 / seed | Cold-start 选题启动器 |
| `cheat-score` | 打分这篇 [path] | 单稿打分（不写文件） |
| `cheat-predict` | 预测 / 启动预测 | 盲预测 + immutable 日志 |
| `cheat-shoot` | 拍了 / 录完了 | 登记拍摄（buffer +1） |
| `cheat-publish` | 已发布 / 发布链接 | 发布元数据登记（buffer -1） |
| `cheat-retro` | 复盘 / T+3d | 数据回收 + 复盘 |
| `cheat-bump` | 升级 rubric / 更新公式 | rubric 升级（含全量重打） |
| `cheat-recommend` | 推荐选题 / next topic | 候选池排序推荐 |
| `cheat-trends` | 抓热点 / 今天有什么可做 | 热点抓取（补充候选池） |
| `cheat-status` | 状态 / 看板 | 状态看板（含 buffer 警戒） |
| `cheat-migrate` | 迁移 / schema 版本不对 | schema 版本升级 |

---

## 预测文件格式

```markdown
# 预测：<title>

## 元信息
- 日期：YYYY-MM-DD
- 阶段：predictions
- 模式：cold-start | calibration

## 预测（immutable）
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

## 使用示例

### 完整流程

```
你：初始化
→ 创建项目骨架，默认 rubric（观点视频）

你：学这个账号 @某个博主
→ 抓取爆款视频，拆解 pattern，存入 samples/

你：找选题
→ 根据对标账号 pattern + 候选池，推荐 3 个方向

你：打分这篇 ./scripts/2026-05-16_001.md
→ 7 维度评分，输出打分结果（不写文件）

你：预测
→ 盲写预测日志，immutable，存入 predictions/

你：拍了 001
→ 更新 buffer，STATUS.md +1

你：已发布，链接是 https://...
→ 登记发布信息，buffer -1

（3 天后）

你：复盘
→ 输入实际数据，分析预测偏差，更新 rubric_notes.md
```

---

## 安装方式

把这个 skill 放入你的 OpenClaw workspace skills 目录：

```bash
cd ~/.openclaw/workspace/<your-agent>/skills/
git clone https://github.com/tongkailei/cheat-on-content.git
```

然后说「初始化」开始使用。

---

## 适用人群

- **短视频创作者**（抖音/B站/小红书）想校准「爆款直觉」
- **内容运营**想从感性创作升级为数据驱动创作
- **创作者**想建立可积累的内容方法论，而不是每次从零开始

---

## License

MIT