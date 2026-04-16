<div align="center">

# UZI-Skill

*"51 个投资大佬帮你看盘，巴菲特和赵老哥终于坐在了同一张桌子上。"*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://python.org)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.com/product/claude-code)
[![Dimensions](https://img.shields.io/badge/Dimensions-22-brightgreen)]()
[![Investors](https://img.shields.io/badge/Investors-51-orange)]()
[![Methods](https://img.shields.io/badge/Institutional%20Methods-17-red)]()

A 股 / 港股 / 美股 · 个股深度分析引擎

[安装](#安装) · [用法](#用法) · [评审团](#-51-位评审团) · [机构方法](#-17-种机构级方法) · [报告样例](#-报告长什么样) · [FAQ](#-faq)

</div>

---

## 这是啥

一句话：输入一只股票，Claude 变成你的私人分析师，跑完 22 个维度的数据、调 17 种华尔街分析模型、让 51 个投资风格完全不同的大佬各自打分，最后吐出一份 600KB 的 Bloomberg 风格报告。

```
/analyze-stock 国盾量子
```

5-8 分钟后你会得到：
- **一份 HTML 报告** — 可以直接用浏览器打开，自包含，离线也能看
- **一张朋友圈竖图** — 1080×1920，直接发
- **一张微信群战报** — 1920×1080
- **一段话摘要** — 复制粘贴就能发群里

## 为什么做这个

之前看一只票的流程：东方财富翻基本面 → 同花顺看 K 线 → 雪球刷大 V 说了啥 → 研报系统找卖方观点 → Excel 算个 DCF → 结果买进去还是亏。

这些活儿本质上就是"搜集信息 → 多角度分析 → 给个结论"，让 AI 全干了不行吗？

市面上看了一圈，要么是输出三段废话的 GPT wrapper，要么是用不起的机构终端。Anthropic 出了个 [financial-services-plugins](https://github.com/anthropics/financial-services-plugins)，方法论很好（DCF / Comps / LBO 那套），但完全是美股视角 + 全要付费数据源。

所以自己搓了一个。**全免费数据源，零 API key，A 股直接能跑。**

---

## 安装

### Claude Code（推荐）

```bash
# 添加 marketplace
/plugin marketplace add wbh604/UZI-Skill

# 安装
/plugin install stock-deep-analyzer@float-future-stock-analyzer
```

### Codex / 其他 Agent（Skills 方式）

如果你用 OpenAI Codex、Devin 或其他支持 Skills 的 agent，可以直接引用 skill 文件：

```bash
# 克隆仓库
git clone https://github.com/wbh604/UZI-Skill.git

# 把 skills/ 目录链接到你的 agent 工作区
# Codex:
cp -r UZI-Skill/skills/ .claude/skills/

# 或直接在 agent 配置里引用 SKILL.md 路径
# skills/deep-analysis/SKILL.md  ← 主分析工作流
# skills/investor-panel/SKILL.md ← 51 评委规则引擎
# skills/lhb-analyzer/SKILL.md   ← 龙虎榜游资匹配
# skills/trap-detector/SKILL.md  ← 杀猪盘检测
```

### Python 依赖

```bash
cd UZI-Skill
pip install -r requirements.txt

# 如果要生成朋友圈 PNG（可选）
playwright install chromium
```

---

## 用法

### 完整深度分析（5-8 分钟）

```
/analyze-stock 水晶光电
/analyze-stock 002273
/analyze-stock 00700.HK
/analyze-stock AAPL
```

### 专项命令

| 命令 | 干嘛的 |
|---|---|
| `/dcf 600519` | DCF 估值 · WACC + 5×5 敏感性表 |
| `/comps 002273` | 同行对标 · PE/PB 分位分析 |
| `/lbo 600519` | LBO 测试 · PE 买方能赚多少 IRR |
| `/initiate 002273` | 机构首次覆盖报告 · JPM/GS 格式 |
| `/ic-memo 002273` | 投委会备忘录 · 三情景回报 |
| `/earnings 002273` | 财报解读 · beat/miss 检测 |
| `/catalysts 002273` | 催化剂日历 · 未来 60 天 |
| `/thesis 002273` | 投资逻辑追踪 · 5 支柱监控 |
| `/screen 002273` | 5 套量化筛选 · value/growth/quality |
| `/dd 002273` | 尽调清单 · 5 工作流 21 项 |
| `/quick-scan 002273` | 30 秒速判 |
| `/panel-only 600519` | 只看 51 评委投票 |
| `/scan-trap 002273` | 杀猪盘排查 |

---

## 🎭 51 位评审团

不是模板话术。每个人有自己的**量化规则集**（共 180 条），给出的建议必须引用具体命中了哪条：

| 组 | 风格 | 人数 | 代表人物 |
|---|---|---|---|
| A | 经典价值 | 6 | 巴菲特 · 格雷厄姆 · 芒格 · 费雪 · 邓普顿 · 卡拉曼 |
| B | 成长投资 | 4 | 林奇 · 欧奈尔 · 蒂尔 · 木头姐 |
| C | 宏观对冲 | 5 | 索罗斯 · 达里奥 · 霍华德马克斯 · 德鲁肯米勒 · 罗伯逊 |
| D | 技术趋势 | 4 | 利弗莫尔 · 米内尔维尼 · 达瓦斯 · 江恩 |
| E | 中国价投 | 6 | 段永平 · 张坤 · 朱少醒 · 谢治宇 · 冯柳 · 邓晓峰 |
| F | A 股游资 | 23 | 章盟主 · 赵老哥 · 炒股养家 · 佛山无影脚 · 北京炒家 · 鑫多多 … |
| G | 量化系统 | 3 | 西蒙斯 · 索普 · 大卫·肖 |

**举个例子**：

> **巴菲特** 给水晶光电打 62 分 · 中性
> "观望：护城河 27/40 可见；但 ROE 5 年最低 6.7%，达标率仅 0/5"
> ✅ 资产负债率 30% 保守 · ❌ ROE 5 年最低 6.7%

> **木头姐** 给国盾量子打 100 分 · 看多
> "量子通信处于 S 曲线拐点，TAM 每年 >30% 增长——买它就是买未来！"
> ✅ 属于颠覆式创新平台 · ✅ 行业增速 35%

> **卡拉曼** 给水晶光电打 0 分 · 看空
> "看空核心：无 30% 安全边际"

---

## 📐 17 种机构级方法

从 [anthropics/financial-services-plugins](https://github.com/anthropics/financial-services-plugins) 移植方法论，适配了 A 股参数（rf=2.5% / ERP=6% / 税率 25% / 终值 g=2.5%）：

**估值建模**
- DCF（WACC 拆解 + 两段 FCF + Gordon Growth 终值 + 5×5 敏感性热力图）
- Comps 同行对标（PE / PB / EV-EBITDA 分位 + 隐含目标价）
- 三表预测（5 年 IS / BS / CF 联动）
- Quick LBO（PE 基金视角 IRR 交叉校验）
- 并购增厚/摊薄模型

**研究工作流**
- 首次覆盖报告（JPM/GS/MS 格式 · 评级 + 目标价 + 论点 + 风险）
- 财报 beat/miss 解读
- 催化剂日历（真实事件提取 + 未来预排 + 影响分级）
- 投资逻辑追踪（5 支柱健康度）
- 晨报 · 量化筛选 · 行业综述

**深度决策**
- IC 投委会备忘录（8 章节 · Bull/Base/Bear 三情景）
- Porter 五力 + BCG 矩阵
- DD 尽调清单（5 工作流 21 项 · 自动标注完成状态）
- 单位经济学 · 价值创造计划 · 组合再平衡

---

## 📸 报告长什么样

跑完之后你会得到一个 ~600KB 的 HTML 文件，里面包含：

- 综合评分仪表盘（总分 + 定调 + 杀猪盘等级）
- 多空大分歧辩论（Top Bull vs Top Bear 互喷 3 轮，引用数字）
- 51 人审判席（灯牌 + 聊天室两种视图）
- 机构级估值建模区（DCF 敏感性热力图 + Comps 分位表 + LBO 卡 + 首次覆盖 + IC Memo + 催化剂时间线 + Porter 雷达图）
- 22 维深度卡（每维有独立可视化：K 线蜡烛图 / PE Band / 雷达图 / 供应链流程图 / 温度计 / 环形图…）
- 四派系买入区间
- 朋友圈竖图 + 战报横图（Playwright 截图）

---

## 🔧 数据源

全部免费，零 API key：

| 数据 | 主源 | 备用 |
|---|---|---|
| 实时行情 / PE / 市值 | 东方财富 push2 | 雪球 → 腾讯 → 新浪 → 百度 |
| 财报历史 | akshare | 雪球 f10 |
| K 线 / 技术指标 | akshare | yfinance |
| 龙虎榜 / 北向 / 两融 | akshare | 东财 |
| 研报 / 公告 | 巨潮 cninfo + akshare | 同花顺 |
| 港股 | akshare hk | yfinance |
| 美股 | yfinance | akshare us |
| 宏观 / 政策 / 舆情 / 杀猪盘 | DuckDuckGo web search | — |

多层 fallback 链 — 一个源挂了自动切下一个。

---

## 📁 项目结构

```
UZI-Skill/
├── .claude-plugin/
│   ├── plugin.json              # 插件清单
│   └── marketplace.json         # Marketplace 配置
├── commands/                    # 14 个 slash commands
├── skills/
│   ├── deep-analysis/           # ★ 主工作流 (6 Task)
│   │   ├── SKILL.md             # Claude 分析师手册
│   │   ├── references/          # 方法论文档 (8 篇)
│   │   ├── assets/              # HTML 模板 + 51 张头像
│   │   └── scripts/
│   │       ├── lib/             # 15 个核心模块
│   │       │   ├── fin_models.py         # DCF/Comps/LBO/3-Stmt/Merger
│   │       │   ├── research_workflow.py  # 7 种研究产物
│   │       │   ├── deep_analysis_methods.py # 6 种 PE/IB/WM 方法
│   │       │   ├── investor_criteria.py  # 51人 × 180 条规则
│   │       │   ├── investor_evaluator.py # 规则引擎
│   │       │   ├── stock_features.py     # 108 标准化特征
│   │       │   └── ...
│   │       ├── fetch_*.py       # 22 个维度 fetcher
│   │       ├── compute_deep_methods.py  # 机构建模计算
│   │       ├── assemble_report.py       # HTML 装配
│   │       └── run_real_test.py         # 主流水线
│   ├── investor-panel/          # 评审团 skill
│   ├── lhb-analyzer/            # 龙虎榜 skill
│   └── trap-detector/           # 杀猪盘 skill
├── requirements.txt
├── LICENSE
└── README.md
```

---

## 🧠 设计理念

**Claude 是分析师，不是脚本搬运工。**

脚本负责采集数据和计算（22 维 fetcher + 17 种模型），但最终的判断——"这只票到底能不能买"——必须 Claude 自己给。

具体来说 Claude 要做三件事情：
1. **审查假设**：DCF 默认用 stage1=10%、beta=1.0，但半导体公司应该用 22% / 1.4，Claude 要自己判断和调整
2. **写定性评语**：每个维度不是只给个分数，还要写"数据背后的故事是什么"
3. **构建叙事**：多空辩论、估值三角验证（DCF 说高估但 LBO 说能赚的时候，这个冲突本身就是信息）

这些写在 `SKILL.md` 里，作为 Claude 的硬性约束。

---

## ❓ FAQ

**Q: 跑一次要多久？**
A: 5-8 分钟，主要是数据采集慢（22 个维度要调十几个 API）。纯计算的机构建模部分 < 1 秒。

**Q: 需要付费数据源吗？**
A: 不需要。全部免费源（akshare / yfinance / DuckDuckGo / 巨潮 / 东方财富 / 雪球），零 API key。

**Q: 港股美股能用吗？**
A: 能。`/analyze-stock 00700.HK` 或 `/analyze-stock AAPL`。

**Q: 数据准不准？**
A: 实时数据走东方财富 / 雪球，财报走巨潮 / akshare，和你在东方财富 App 上看到的一样。但 web search 质量不稳定（DuckDuckGo 中文搜索有时会返回无关结果），所以 Claude 会做二次审查。

**Q: 能当投资建议吗？**
A: 不能。这是工具不是神仙，51 个大佬的意见都是规则引擎模拟的，不代表真人观点。买不买你自己决定。

---

## 🤝 致谢

- [anthropics/financial-services-plugins](https://github.com/anthropics/financial-services-plugins) — 机构级分析方法论
- [akshare](https://github.com/akfamily/akshare) — A 股数据引擎
- [titanwings/colleague-skill](https://github.com/titanwings/colleague-skill) — Skill 架构参考
- [virattt/ai-hedge-fund](https://github.com/virattt/ai-hedge-fund) — Pydantic Signal 模式
- [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) — 多空辩论循环

---

## ⚠️ 免责声明

本工具由 AI 模型基于公开数据生成分析报告。所有评分、建议、模拟评语均为算法输出，不代表任何真实投资者的实际观点。**不构成投资建议**，投资有风险，入市需谨慎。

---

<div align="center">

MIT License · Made by Float Future · O.o

</div>
