---
name: fund-investment-analysis
description: Use when analyzing Chinese mutual fund portfolios, generating buy/sell/hold signals, assessing position sizing, or evaluating cross-asset diversification (QDII, A-stock, gold, bonds)
---

# Fund Investment Analysis

## Overview

Multi-dimensional rules engine for Chinese mutual funds. Outputs signal (buy/sell/hold), position advice, and risk warnings per fund. Covers QDII, A-stock sector funds, gold ETFs, and mixed funds.

## Core Dimensions

### 1. Asset Class Detection
```
QDII:     name contains QDII|纳斯达克|纳指|标普|日经|日本|德国|DAX|越南|新兴市场|全球
Gold:     name contains 黄金|上海金
A-Stock:  everything else
Bond:     name contains 债券|债|纯债
```

### 2. Momentum Signals (based on 估算涨幅 gzzl)
| Condition | Signal | Action |
|-----------|--------|--------|
| gzzl > 5% | 🔴 减仓 | Short-term overheating, lock profit |
| gzzl 3-5% | 🟠 观望 | Elevated, don't chase |
| gzzl -2 to 3% | 🟡 持有 | Normal range |
| gzzl -4 to -2% | 🟢 关注 | Dip forming |
| gzzl < -4% | 🟢 加仓 | Oversold, accumulate |

### 3. Asset-Class Specific Rules

**US Stocks (纳斯达克/标普):**
- Long-term uptrend bias — hold by default
- gzzl < -1.5% → buy signal (buy the dip)
- gzzl > 5% → consider trim but don't exit fully
- Rationale: US equities structural bull, 20-year CAGR ~10%

**Japan (日经/日本):**
- gzzl < -2% → buy signal
- Default hold — reasonable valuations vs US
- Watch JPY/USD for currency impact

**Europe (德国/DAX):**
- Default hold — manufacturing powerhouse
- Watch EU energy policy and China demand

**Vietnam/Emerging Markets:**
- gzzl > 5% → sell (high vol, lock gains)
- gzzl < -2% → buy (dip entry)
- Higher risk premium required

**Gold (黄金/上海金):**
- Core hedge asset, 5-15% of portfolio
- gzzl < -1.5% → buy (gold dips are rare, seize them)
- Default hold — inflation hedge, crisis insurance
- Don't sell unless >20% portfolio weight

**A-Stock Sector Funds:**
- Policy-aligned sectors (新能源, 储能, 电池, 有色, 稀土, 机器人, 医药, 互联网, 港股通):
  - gzzl < -1% → buy (policy tailwind + dip)
  - Hold by default — state-backed industries
- Non-policy sectors:
  - gzzl > 4% → sell
  - More cautious, tighter stops

### 4. Position Sizing

| Amount | Advice |
|--------|--------|
| >5000元 | ⚠️ 重仓单基 — 减配30%, diversify |
| 2000-5000元 | ⚠️ 偏高 — 减配10-20% |
| 500-2000元 | ✅ 标准仓位 |
| 100-500元 | 💡 轻仓 — 可增配 |
| <100元 | ⚠️ 过轻 — 意义不大,考虑清仓或加仓 |

### 5. Portfolio-Level Checks

**Diversification:**
- Single fund max: 25% of total portfolio
- Single asset class max: 60% of total
- Gold allocation: 5-15% ideal
- QDII total: 30-70% range is healthy

**Risk Flags:**
- >50% in single country → concentration risk
- No gold → no hedge
- All A-stock → no global diversification
- >3 same-sector funds → overlap waste

## Analysis Output Format

Per fund:
```
代码: 000001
名称: 某某基金
类型: QDII/美股科技
信号: 🟢 加仓 / 🟡 持有 / 🔴 减仓
仓位: 增配X% / 维持 / 减配X%
理由: [1-2 specific reasons]
```

Portfolio summary:
```
总资产: ¥X
QDII占比: X% | A股占比: X% | 黄金: X%
集中度风险: 低/中/高
建议: [1-2 actionable recommendations]
```

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Chasing gzzl>3% funds | Never buy into strength >3% |
| Panic selling on -2% dip | This is normal volatility |
| Gold as growth asset | Gold is insurance, not growth |
| Ignoring overlap | Two Nasdaq funds = same bet |
| Equal-weighting everything | Conviction matters, size accordingly |
