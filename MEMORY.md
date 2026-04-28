# MEMORY.md - 长期记忆

这是小恶龙的长期记忆文件，保存重要的学习、决策和事件。

---

## 用户信息

- **姓名:** 佟学 (小佟)
- **Telegram ID:** 8425256771
- **背景:** 熟悉短视频创作，有技术背景，关注内容变现
- **时区:** Asia/Shanghai

---

## 我的身份

- **名称:** 小恶龙
- **形态:** 资深编导（龙形态）
- **Emoji:** 🐉
- **定位:** 短视频内容创作专家，专注抖音、小红书、视频号等平台

### 核心能力
- ✅ 爆款选题策划
- ✅ 30秒/60秒脚本撰写（含口播+画面描述）
- ✅ 分镜头脚本（景别、运镜、BGM建议）
- ✅ 数据复盘与优化建议
- ❌ 不负责剪辑实操（但可指导剪辑逻辑）

### 编导能力要求
- 文案能力：抓眼球、有情绪、促行动的脚本
- 信息提炼与故事化表达
- 网感敏锐：抖音重节奏、小红书重干货/审美
- 镜头语言：理解景别、运镜、构图对情绪的影响

---

## 系统配置

### 模型配置 (2026-04-11)
- **当前模型:** GLM-5 (custom-api-lkeap-cloud-tencent-com/glm-5-0)
- **配置路径:** `~/.openclaw/openclaw.json`

### Telegram Bots
| Bot Token 后缀 | Agent | 用途 |
|---------------|-------|------|
| main_bot | main | 主助手 |
| xiaoe_bot | xiaoe | 小恶龙 |
| small_balloons_bot | small_balloons | 小气球 |
| novel_bot | novel | 小说创作 |

### 工作区路径
| Agent | 工作区 |
|-------|--------|
| main | ~/.openclaw/workspace |
| xiaoe | ~/.openclaw/workspace-xiaoe |
| small_balloons | ~/.openclaw/workspace-small-balloons |
| novel | ~/.openclaw/workspace-novel |

---

## 历史脚本案例

### 抚仙湖麒麟山脚本 (2026-04-03)
**标题:** 《昆明周边这个小众山头，俯瞰抚仙湖太绝了》
**时长:** 约23秒
**目标人群:** 20-35岁
**结构:**
- 开头钩子 3秒：无人机视角翻越山脊
- 徒步出发 5秒：山脊步道画面
- 登顶震撼 10秒：抚仙湖全景
- 情绪收尾 5秒：引导关注

**情绪关键词:** 秘境、治愈、逃离城市、出片

### 昆明蓝花楹选题 (2026-04-09)
1. 「昆明蓝花楹地图｜这5个地方拍到腿软」
2. 「蓝花楹下男朋友拍照实录｜气到笑出声」
3. 「2026昆明蓝花楹盛花期预测｜最后一周」
4. 蓝花楹打卡教程类

**完播技巧:** 结尾"最后这个地方99%的人不知道"

### 宝丰湿地公园选题 (2026-04-03)
Top 5 高赞帖子:
1. 昆明一些免费的漂亮公园（合集）- 4800赞
2. 宝丰湿地公园，昆明人的城市鱼缸 - 2605赞
3. 昆明 🌸| 有被这个湿地公园美到 - 894赞

### 禄劝神仙坝选题 (2026-04-28)
**核心卖点:** 离昆明2小时，草甸+杜鹃花，人少小众

5个选题方向:
1. 「偶然刷到一个地名，叫神仙坝」- 发现式开场
2. 「看到一个名字叫神仙坝」- 悬念感
3. 「百度搜了个地名」- 搜索动机
4. 「朋友发了一张照片」- 社交传播
5. 「刷小红书看到神仙坝」- 平台验证

**最终脚本:** 选用选题1，links风格，60秒
- 开场：手机地图画面，"偶然刷到一个地名，叫神仙坝"
- 中段：徒步进山 → 草甸全景 → 杜鹃花特写
- 结尾："禄劝神仙坝，杜鹃花不挤，人也不挤"

**关键调整:**
- 杜鹃花稀疏 → 转化为卖点（"不挤"）
- 花期诚实 → 增强可信度

---

## 重要决策

### 2026-04-08: 删除其他模型，只保留 MiniMax
- 删除了 Moonshot (Kimi)、Gemma 等模型配置
- 设置 contextWindow=200k, maxTokens=32k

### 2026-04-08: 配置 Telegram 私有网络访问
- 添加 `channels.telegram.network.dangerouslyAllowPrivateNetwork: true`
- 解决 Telegram 媒体下载被阻止的问题

### 2026-04-11: 删除重叠功能 Skills
- 删除 git-notes-memory（与 memory-system-v2 功能重叠）
- 删除 ontology（与 memory-system-v2 功能重叠）
- 保留 memory-system-v2 作为主要记忆系统

---

## 重要事件

### 2026-04-03: OpenClaw 升级
- 从 v2026.3.28 升级到 v2026.4.1
- 安装 self-improving skill
- 配置 Tavily API Key

### 2026-04-10: novel agent 绑定
- 创建 novel_bot
- 绑定到 novel agent
- 修复配置错误

---

## 工作原则

1. 拒绝空洞理论，只提供可落地的脚本、分镜或优化方案
2. 所有建议基于平台算法逻辑（抖音3秒完播、小红书干货密度）
3. 如果用户需求模糊，主动追问：账号类型？目标人群？转化目标？
4. 不承诺"必爆"，但提供经过验证的内容模型
5. 每日自省：回顾脚本输出，提取高频需求，更新 short_video_tips.md

## 内容创作经验

### 开场方式库
- **逃离式:** "有时候，我就是想逃离一下"（慎用，用户反馈太多）
- **发现式:** "偶然刷到一个地名..." / "看到一个名字叫..."
- **悬念式:** "你猜，离昆明两小时车程，能有什么？"
- **提问式:** "你有多久没见过这样的绿色了？"
- **反差式:** "本来只是想...没想到..."
- **画面切入:** 前5秒纯画面，不说话

### links风格要点
- 口播像朋友聊天，有呼吸感
- 画面节奏慢，每镜头停留3-5秒
- 文案有留白，不堆砌
- 结尾不硬转，用画面和文案留余韵
- 保留环境音（鸟叫、水流、风声）

### 花期/景点诚实原则
- 不夸大花期，诚实说"稀稀落落"
- 转化劣势为卖点："杜鹃花不挤，人也不挤"
- 提到盛花期情况，增加可信度

---

---

## 更新日志
- 2026-04-28: 添加禄劝神仙坝选题案例，整理开场方式库、links风格要点、花期诚实原则
- 2026-04-12: 初始化 MEMORY.md，整合 memory/ 目录、workspace 主记忆文件及历史对话

## Promoted From Short-Term Memory (2026-04-18)

<!-- openclaw-memory-promotion:memory:memory/2026-04-10.md:63:79 -->
- - Candidate: User: Conversation info (untrusted metadata): ```json { "message_id": "336", "sender_id": "8425256771", "sender": "佟学", "timestamp": "Thu 2026-04-09 18:12 GMT+8" } ``` Sender (untrusted metadata): ```json { "label": "佟学 (8425256771)", "id": "8425256771", "name": "佟学" } ``` 给我5个昆明 - confidence: 0.00 - evidence: memory/.dreams/session-corpus/2026-04-09.txt:1-1 - recalls: 0 - status: staged - Candidate: Assistant: 给小佟5个昆明蓝花楹爆款选题🐉 --- ** 1️⃣ 「昆明蓝花楹地图｜这5个地方拍到腿软」** - 教大家怎么找机位 - 教场中路、盘龙江边、联盟路… - 完播点：结尾“最后这个地方99%的人不知道” --- **2️⃣ 「蓝花楹下男朋友拍照实录｜气到笑出声」** - 痛点：男朋友拍的照和预期差距太大 - 结尾：甩一张“正确示范”反转 - 完播点：气笑了还想看 --- **3️⃣ 「2026昆明蓝花楹盛花期预测｜最后一周」** - 赶在花期快结束前推 - 蹭“最后几天”紧迫感 - 完播点：提醒粉丝赶紧去 --- **4️⃣ 「蓝 - confidence: 0.00 - evidence: memory/.dreams/session-corpus/2026-04-09.txt:2-2 - recalls: 0 - status: staged <!-- openclaw:dreaming:light:end --> ## REM Sleep <!-- openclaw:dreaming:rem:start --> ### Reflections - Theme: `reflections` kept surfacing across 42 memories. - confidence: 1.00 [score=0.908 recalls=5 avg=1.000 source=memory/2026-04-10.md:63-79]
<!-- openclaw-memory-promotion:memory:memory/2026-04-11.md:120:134 -->
- - evidence: memory/2026-04-10.md:62-65 - recalls: 0 - status: staged - Candidate: Reflections: Theme: `大家` kept surfacing across 1 memories.; confidence: 1.00; evidence: memory/.dreams/session-corpus/2026-04-09.txt:2-2; note: reflection - confidence: 0.00 - evidence: memory/2026-04-10.md:18-21 - recalls: 0 - status: staged - Candidate: User: Conversation info (untrusted metadata): ```json { "message_id": "336", "sender_id": "8425256771", "sender": "佟学", "timestamp": "Thu 2026-04-09 18:12 GMT+8" } ``` Sender (untrusted metadata): ```json { "label": "佟学 (8425256771)", "id": "8425256771", "name": "佟学" } ``` 给我5个昆明 - confidence: 0.00 - evidence: memory/.dreams/session-corpus/2026-04-09.txt:1-1 - recalls: 0 - status: staged - Candidate: Assistant: 给小佟5个昆明蓝花楹爆款选题🐉 --- ** 1️⃣ 「昆明蓝花楹地图｜这5个地方拍到腿软」** - 教大家怎么找机位 - 教场中路、盘龙江边、联盟路… - 完播点：结尾“最后这个地方99%的人不知道” --- **2️⃣ 「蓝花楹下男朋友拍照实录｜气到笑出声」** - 痛点：男朋友拍的照和预期差距太大 - 结尾：甩一张“正确示范”反转 - 完播点：气笑了还想看 --- **3️⃣ 「2026昆明蓝花楹盛花期预测｜最后一周」** - 赶在花期快结束前推 - 蹭“最后几天”紧迫感 - 完播点：提醒粉丝赶紧去 --- **4️⃣ 「蓝 - confidence: 0.00 [score=0.859 recalls=4 avg=1.000 source=memory/2026-04-11.md:120-134]

## Promoted From Short-Term Memory (2026-04-25)

<!-- openclaw-memory-promotion:memory:memory/2026-04-18.md:327:329 -->
- - status: staged [score=0.809 recalls=0 avg=0.620 source=memory/2026-04-18.md:307-307]
