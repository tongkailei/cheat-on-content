# cheat-on-content

**You're reading this. The skill predicted it.**

A workflow that turns every post into a calibrated experiment �?score, blind-predict, retro, evolve. The future doesn't reward effort, it rewards those who see the pattern first.

---

## What it does

Content creation is a **prediction problem**:
- Before publish �?predict plays / engagement
- After publish �?calibrate against real data
- Over time �?your rubric gets sharper, predictions get more accurate

Not a tool to "come up with ideas" �?it's a tool to **calibrate your intuition of what makes content work**.

---

## Three Non-Negotiable Principles

### Principle 1: Blind Prediction
The prediction must be written **before** seeing any real data. After writing, the `## 预测` section is immutable �?you can only append to `## 复盘`.
- �?"Let me tell you the actual plays first, then you reverse-engineer the score"
- �?Write prediction �?publish �?wait 3 days �?retro

### Principle 2: Bump = Full Re-score
When upgrading the rubric, **all** calibrated samples with real performance data must be re-scored with the new formula. New ranking must match actual ranking in �?/5 samples before the upgrade is allowed.

### Principle 3: Rubric is a Workbench, Not a Museum
Observations that get contradicted by new data are **deleted directly** �?no archaeological layer of "I used to think X but actually..." Git history is the archive.

---

## Quick Start

### First Time

```
你：初始�?/ init
�?cheat-init creates project skeleton + default rubric (opinion video 7-dim)
```

### Daily Flow

| Scenario | You say | System does |
|----------|---------|-------------|
| Find topics | `找选题` / `seed` | Cold-start topic proposal |
| Learn from account | `学这个账�?@xxx` | Dissect viral patterns |
| Score a draft | `打分这篇 [path]` | 7-dim scoring (no file written) |
| Blind predict | `预测` / `启动预测` | Write immutable prediction log |
| Done shooting | `拍了 X` / `录完了` | Update buffer count |
| Published | `已发布` / `发布链接�?X` | Register publish metadata |
| 3 days later retro | `复盘` | Collect data, analyze偏差, bump rubric |
| Check status | `状态` / `看板` | Show buffer / prediction / candidate pool status |
| Catch trends | `抓热点` | Scrape trends to supplement candidate pool |

---

## Project Structure

```
<content-project>/
├── .cheat-state.json          # Global state (shared across sub-skills)
├── rubric_notes.md            # Scoring rules (source of truth)
├── STATUS.md                  # Dashboard (buffer alerts)
├── WORKFLOW.md                # 5-phase process doc
├── scripts/                   # Pre-shoot drafts
├── predictions/               # Prediction logs (immutable)
├── videos/                    # Post-shoot footage + data reports
├── samples/                   # Benchmark account analysis
├── candidates.md              # Topic candidate pool
└── benchmark.md              # Benchmark account info
```

---

## Scoring Dimensions (Opinion Video Rubric)

| # | Dimension | Description |
|---|-----------|-------------|
| 1 | Hook Power (ER) | Can it grab attention in first 3 seconds? |
| 2 | Viewpoint Impact (SR) | Is the opinion sharp and distinctive? |
| 3 | Logic Completeness (QL) | Is the argument coherent with no obvious gaps? |
| 4 | Emotional Value (NA) | Can it evoke resonance or emotional reaction? |
| 5 | Practical Value (AB) | Does the viewer feel they've learned something? |
| 6 | Structure & Rhythm (SAT) | Does opening/climax/ending flow smoothly? |
| 7 | Expectation Management (HP) | Do title/thumbnail match the content? |

**Grades: S(9-10) / A(7-8) / B(5-6) / C(3-4) / D(1-2)**

---

## Dual Mode System

The system auto-switches between two modes based on your calibration pool size:

- **cold-start (< 5 samples with real data)**
  �?Simplified prediction: 7-dim scoring + one-line bet, no bucket numbers

- **calibration (�?5 samples)**
  �?Full 7-component prediction: play bucket + confidence index + anchor comparison + one-line bet

---

## Sub-Skill Reference

| Skill | Trigger | Function |
|-------|---------|----------|
| `cheat-init` | 初始�?/ init | Entry: init project skeleton + rubric |
| `cheat-learn-from` | 学这个账�?/ learn from | Import benchmark account, dissect patterns |
| `cheat-seed` | 找选题 / seed | Cold-start topic launcher |
| `cheat-score` | 打分这篇 [path] | Single draft scoring (no file written) |
| `cheat-predict` | 预测 / 启动预测 | Blind prediction + immutable log |
| `cheat-shoot` | 拍了 / 录完�?| Register shoot (buffer +1) |
| `cheat-publish` | 已发�?/ 发布链接 | Publish metadata registration (buffer -1) |
| `cheat-retro` | 复盘 / T+3d | Data collection + retrospective |
| `cheat-bump` | 升级 rubric / 更新公式 | Rubric upgrade (incl. full re-scoring) |
| `cheat-recommend` | 推荐选题 / next topic | Candidate pool ranking + recommendation |
| `cheat-trends` | 抓热�?/ 今天有什么可�?| Trend scraping (supplements candidate pool) |
| `cheat-status` | 状�?/ 看板 | Status dashboard (incl. buffer alerts) |
| `cheat-migrate` | 迁移 / schema 版本不对 | Schema version upgrade |

---

## Prediction File Format

```markdown
# 预测�?title>

## 元信�?- 日期：YYYY-MM-DD
- 阶段：predictions
- 模式：cold-start | calibration

## 预测 (immutable)
预测播放量：<bucket>
信心指数�?low/medium/high>
锚点�?与哪个已知视频对�?
一句话 bet�?核心假设>

## 评分 (cheat-score output)
维度1�?score>/10
维度2�?score>/10
...

## 复盘 (cheat-retro fills in)
- 实际播放量：<真实数据>
- 预测偏差�?分析>
- rubric 偏差�?评分维度是否需要调�?
- 新观察：<值得加入 rubric 的发�?
```

---

## Full Usage Example

```
你：初始�?�?Creates project skeleton, default rubric (opinion video)

你：学这个账�?@某个博主
�?Scrapes viral videos, dissects patterns, stores in samples/

你：找选题
�?Based on benchmark patterns + candidate pool, recommends 3 directions

你：打分这篇 ./scripts/2026-05-16_001.md
�?7-dim scoring, outputs score result (no file written)

你：预测
�?Writes blind prediction log, immutable, stored in predictions/

你：拍了 001
�?Updates buffer, STATUS.md +1

你：已发布，链接�?https://...
�?Registers publish info, buffer -1

(3 days later)

你：复盘
�?Inputs real data, analyzes prediction deviation, updates rubric_notes.md
```

---

## Installation

Add this skill to your OpenClaw workspace skills directory:

```bash
cd ~/.openclaw/workspace/<your-agent>/skills/
git clone https://github.com/tongkailei/cheat-on-content.git
```

Or use install.sh:

```bash
bash install.sh
```

Then say 「初始化�?to begin.

---

## Who it's for

- **Short video creators** (Douyin/Bilibili/Xiaohongshu) who want to calibrate their "viral intuition"
- **Content operators** transitioning from gut-feel creation to data-driven creation
- **Creators** who want to build an accumulable content methodology instead of starting from zero each time

---

## License

MIT
