<div align="center">
  <img src="assets/hero-banner.png" alt="Wolf Ultimate SNR Trading System" width="100%" style="border-radius: 8px; margin-bottom: 20px;" />

  # 🐺 Wolf Ultimate v1.0 — TradingView Indicator

  > A professional-grade Pine Script v5 indicator implementing the full Wolf (Market Structure, Narrative & Reversal) methodology across **5 interconnected modules**.

  ![Pine Script](https://img.shields.io/badge/Pine%20Script-v5-blue?logo=tradingview)
  ![Modules](https://img.shields.io/badge/Modules-5-green)
  ![Status](https://img.shields.io/badge/Status-Production-brightgreen)
  ![License](https://img.shields.io/badge/License-MIT-blue.svg)
</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Module 1: Foundation (SNR & Trendlines)](#module-1-foundation-snr--trendlines)
- [Module 2: Breakouts & Pattern Detection](#module-2-breakouts--pattern-detection)
- [Module 3: MTF Storyline Tracker](#module-3-mtf-storyline-tracker)
- [Module 4: Setup & Entry Engine](#module-4-setup--entry-engine)
- [Module 5: LTF Confirmations & Sniper Score](#module-5-ltf-confirmations--sniper-score)
- [Installation](#installation)
- [Configuration](#configuration)
- [Technical Constraints](#technical-constraints)
- [Best Practices](#best-practices)

---

## Overview

The Wolf Ultimate indicator is a complete trading system that:

1. **Maps the battlefield** — Auto-detects A-shape resistance, V-shape support, and Gap levels using candle body pricing
2. **Identifies reversals** — Scans for Quasimodo (QM) patterns with auto-labeled sub-levels (Apex, LS, SBR/RBS, ERS)
3. **Reads the narrative** — Tracks Monthly, Weekly, and Daily storylines with cross-timeframe confirmation
4. **Generates setups** — Phase-aware entry engine with a refinement algorithm that drills into 30M/15M data
5. **Confirms entries** — Lower-timeframe trigger system with a Sniper Score rated 0–10

---

## Module 1: Foundation (SNR & Trendlines)

### A-Shape Detection (Resistance)
Detects when a **bullish candle is followed by a bearish candle**, forming a peak. The resistance level is placed at the **highest body close/open** of the two candles — not the wick.

### V-Shape Detection (Support)
Detects when a **bearish candle is followed by a bullish candle**, forming a trough. The support level is placed at the **lowest body close/open** of the two candles.

### Gap Detection
Identifies **bullish gaps** (two consecutive bullish candles with `low > high[1]`) and **bearish gaps** (two consecutive bearish candles with `high < low[1]`). Drawn as semi-transparent boxes.

### Freshness Filter
Every level is tracked for price interaction:

| State | Condition | Visual |
|---|---|---|
| **Fresh** | Never touched since formation | Solid bright line |
| **Unfresh** | Wick touched but body didn't break | Dashed gray line |
| **Broken** | Body closed through the level | Removed from chart |

### Dynamic Trendlines
- Auto-drawn connecting consecutive **A-shapes** (resistance trendline) or **V-shapes** (support trendline)
- **Touch counter** tracks interactions (max configurable, default: 5)
- **3rd touch** highlighted with ⚡ marker — strongest breakout point
- Trendline marked as broken when body closes beyond it

---

## Module 2: Breakouts & Pattern Detection

### Swing Point Engine
Uses `ta.pivothigh()` and `ta.pivotlow()` with configurable left/right bars (default: 5). Stores the last 20 swing points for pattern analysis.

### Valid Breakout Filter

| Type | Condition | Reliability |
|---|---|---|
| **External BOS** | Body closes beyond the last A/V shape formed before the SNR level | ✅ HIGH — bold `▲ BOS` / `▼ BOS` label |
| **Internal BOS** | Body crosses a swing point between A/V shapes | ⚠️ LOW — subtle `int▲` / `int▼` label |

### Quasimodo (QM) Scanner

**Bearish QM:** `H1 → L1 → HH (>H1) → LL (<L1)`
**Bullish QM:** `L1 → H1 → LL (<L1) → HH (>H1)`

Pattern is drawn with orange connecting lines between the swing points.

### QM Sub-Levels (Auto-Labeled)

| Sub-Level | Color | Description |
|---|---|---|
| **APEX** | 🟡 Gold | The extreme point of the QM head |
| **LS** | 🔵 Blue | Left Shoulder — first swing |
| **SBR/RBS** | 🟣 Purple | Support Becomes Resistance / Resistance Becomes Support |
| **ERS** | 🔷 Cyan | Early Right Shoulder — mini A/V shape before the breakout |

---

## Module 3: MTF Storyline Tracker

### Storyline Rules

| Storyline | Confirmed By | Logic |
|---|---|---|
| **Monthly** | Daily breakout | Daily candle body closes beyond Monthly A/V level |
| **Weekly** | 4H breakout | 4H candle body closes beyond Weekly A/V level |
| **Daily** | 1H breakout | 1H candle body closes beyond Daily A/V level |

### Classic vs. Advanced Mode

| Mode | Condition | Primary Checkpoints |
|---|---|---|
| **Classic** | Fresh SNR levels exist in current zone | SNR levels (A/V shapes) |
| **Advanced** | All fresh levels exhausted | HTF Trendlines |

### Three-Phase Background Coloring

| Phase | Color | Trigger |
|---|---|---|
| **Start** | 🟢 Green / 🔴 Red | QM pattern confirmed + initial breakout |
| **Middle** | 🔵 Blue | Continuation — HH/HL (bull) or LH/LL (bear) |
| **Ending** | 🟡 Yellow | Price reaches major HTF SNR or trendline exhaustion |

### Dashboard
Dark-themed table (top-right) displaying:
- Monthly / Weekly / Daily storyline direction (▲ Bull / ▼ Bear)
- Current phase (Start / Middle / Ending)
- Classic / Advanced mode
- Active QM pattern count
- Sniper Score (when in entry zone)

---

## Module 4: Setup & Entry Engine

> 📚 **Detailed Guide:** Check out the [Wolf Entry Setups Guide](docs/ENTRY_SETUPS.md) for a comprehensive breakdown of execution rules, LTF triggers, and structural validation.

### Phase 1 — QMS Setups (Start Phase)
During the Start phase, the indicator watches the QM pattern's internal levels:
- **Apex** (gold), **LS** (blue), **SBR/RBS** (purple), **ERS** (cyan)

### Refinement Algorithm
If the HTF Apex shows a **long wick** (>60% of candle range is wick), the indicator scans **30M and 15M** data to find the freshest unmitigated A/V shape within the wick range → replaces the HTF entry with a **sniper-refined level**.

### Phase 2 & 3 — Continuation Setups
During the Middle/Ending phases, the indicator stops looking for reversals and highlights:
- **C.APEX** — Continuation Apex (latest A/V in trend direction)
- **C.GAP** — Continuation Gap

### Alert System
Fires alerts with full context: setup type, direction, price level, and current phase.

---

## Module 5: LTF Confirmations & Sniper Score

When price enters an **HTF entry zone** (within 2.5 ATR of an active setup level), the indicator checks lower timeframes for confirmation triggers.

### Confirmation Triggers

| Trigger | Data Source | Logic |
|---|---|---|
| **Candle Rejection** | 5M intrabar | Engulfing candle with body >60% of range, rejecting the level |
| **Breaking Gap** | 5M intrabar | Gap forms then gets filled on the next bar |
| **Mini QM** | 1M intrabar | 3-point reversal pattern on intrabar data |
| **5M EMA Break** | 5M `request.security` | Engulfing candle breaks and closes past the 5-period EMA |

### Sniper Score (0–10)

Each trigger earns points based on **proximity to the HTF entry level**:

| Proximity | Points |
|---|---|
| Very tight (>80% ATR proximity) | +3 |
| Good (>50%) | +2 |
| Acceptable (>20%) | +1 |
| **Cluster bonus** (3+ triggers found) | +2 |

Displayed as `🎯 Sniper: X/10` with color coding:
- **Green** (8+): High conviction
- **Yellow** (5-7): Moderate
- **Red** (1-4): Low conviction

---

## Installation

1. Open **TradingView** → Pine Script Editor
2. Copy the contents of `Wolf_Ultimate.pine`
3. Paste into the editor → Click **Add to Chart**
4. Configure settings via the ⚙️ Settings panel

---

## Configuration

### Module 1: Foundation
| Setting | Default | Description |
|---|---|---|
| Show A-Shape Levels | ✅ | Toggle resistance levels |
| Show V-Shape Levels | ✅ | Toggle support levels |
| Show Gap Levels | ✅ | Toggle gap zones |
| Max Active Levels | 25 | Rolling cap on visible levels |
| Trendline Max Touches | 5 | Mark exhausted after N touches |

### Module 2: Breakouts
| Setting | Default | Description |
|---|---|---|
| Pivot Left/Right Bars | 5 | Sensitivity of swing detection |
| Show BOS Labels | ✅ | Toggle breakout labels |
| Show QM Patterns | ✅ | Toggle Quasimodo detection |

### Module 3: Storyline
| Setting | Default | Description |
|---|---|---|
| Show Dashboard | ✅ | Toggle the info table |
| Dashboard Position | Top Right | Table placement |
| Phase BG Opacity | 92 | Background transparency (0-100) |

### Module 4: Setups
| Setting | Default | Description |
|---|---|---|
| Show Setup Lines | ✅ | Toggle entry level lines |
| Enable Refinement | ✅ | Toggle the 30M/15M refinement |

### Module 5: Confirmations
| Setting | Default | Description |
|---|---|---|
| LTF EMA Length | 5 | Period for the 5M EMA trigger |
| Show Sniper Score | ✅ | Toggle score display |
| Min Score for Alert | 5 | Minimum score to fire alert |

---

## Technical Constraints

| Resource | Used | Limit |
|---|---|---|
| `request.security()` calls | 11 | 40 max |
| `request.security_lower_tf()` calls | 2 | (shared with above) |
| **Total request.\*** | **13** | **40 max ✅** |
| Lines / Labels / Boxes | Dynamic cleanup | 500 max each ✅ |
| Active levels cap | 25 (configurable) | — |
| Active QM patterns cap | 5 | — |
| Active trendlines cap | 20 | — |
| Compiled tokens | ~50K estimated | 80K max ✅ |

---

## Best Practices

### Recommended Timeframes

| Style | Chart TF | Why |
|---|---|---|
| **Intraday** | 1H | Full MTF storyline + all LTF triggers active |
| **Swing** | 4H | Best balance of HTF context + execution |
| **Scalping** | 15M | Works, but LTF triggers limited |
| **Position** | Daily | Strong storyline signals, no LTF intrabar |

### Tips
- **Lower pivot bars** (3) = more QM detections, more noise
- **Higher pivot bars** (7-10) = only major QM patterns
- Increase **Max Active Levels** to 30-40 on Daily/4H charts
- Lower **Phase BG Opacity** to 85-88 for more visible phase coloring
- Set **Min Sniper Score** to 3 for learning, 7+ for live trading

---

## License

This indicator is provided as-is for educational and personal trading use.

---

*Built with 🐺 precision by the Wolf pack.*
