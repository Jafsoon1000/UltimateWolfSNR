<div align="center">
  <img src="assets/hero-banner.png" alt="Wolf Ultimate SNR Trading System" width="100%" style="border-radius: 8px; margin-bottom: 20px;" />

  # Wolf Ultimate v1.0 — TradingView Indicator

  > A professional Pine Script v5 indicator implementing the Wolf methodology for market structure, narrative, and reversal analysis.

  ![Pine Script](https://img.shields.io/badge/Pine%20Script-v5-blue?logo=tradingview)
  ![Modules](https://img.shields.io/badge/Modules-5-green)
  ![Status](https://img.shields.io/badge/Status-Production-brightgreen)
  ![License](https://img.shields.io/badge/License-MIT-blue.svg)
</div>

---

## Overview

Wolf Ultimate is a comprehensive TradingView indicator designed to support structured market analysis and trade execution. It combines five complementary modules to deliver:

- automated support and resistance detection,
- breakout and Quasimodo pattern identification,
- multi-timeframe narrative tracking,
- entry refinement logic,
- lower-timeframe confirmation scoring.

This indicator is intended for traders who require both higher timeframe context and lower timeframe validation.

---

## Key Features

- Automatic A/V support and resistance detection using candle body structure
- Freshness tracking for levels, including fresh, unfresh, and broken states
- Dynamic trendlines with touch counting and breakout signals
- Quasimodo pattern detection with sub-level labelling
- Multi-timeframe storyline tracker for Monthly, Weekly, and Daily context
- Setup and entry engine with 30M/15M refinement
- Lower-timeframe confirmation triggers and a graded conviction score
- Configurable alerts and display options

---

## Modules

### Module 1 — Foundation: SNR & Trendlines

Detects price structure with:

- A-shape resistance and V-shape support levels,
- gap zones for bullish and bearish continuation,
- freshness state filtering,
- trendline construction and break detection.

### Module 2 — Breakouts & Pattern Detection

Analyzes swing points and validates breakouts using body-based logic. It also identifies Quasimodo patterns and labels their structural components for clearer interpretation.

### Module 3 — MTF Storyline Tracker

Tracks narrative direction across timeframes. This module identifies consistent Monthly, Weekly, and Daily signals and adapts between classic support/resistance analysis and higher timeframe trendline structure.

### Module 4 — Setup & Entry Engine

Generates valid entry zones using high timeframe structure and refinement rules. It can refine candidate levels using 30M and 15M data when a high timeframe structure level contains excessive wick energy.

### Module 5 — LTF Confirmations & Sniper Score

Provides lower-timeframe verification through rejection patterns, gap behavior, micro-patterns, and EMA interactions. It combines these inputs into a single conviction score from 0 to 10.

---

## Installation

1. Open TradingView and launch the Pine Script Editor.
2. Copy the contents of `Wolf_Ultimate.pine`.
3. Paste the script into TradingView and click **Add to Chart**.
4. Configure the indicator through the settings panel.

---

## Configuration

### Foundation

| Setting | Default | Purpose |
|---|---|---|
| Show A-Shape Levels | ✅ | Display resistance structure |
| Show V-Shape Levels | ✅ | Display support structure |
| Show Gap Levels | ✅ | Display gap zones |
| Max Active Levels | 25 | Limit visible levels |
| Trendline Max Touches | 5 | Define trendline exhaustion threshold |

### Breakouts

| Setting | Default | Purpose |
|---|---|---|
| Pivot Left/Right Bars | 5 | Swing detection sensitivity |
| Show BOS Labels | ✅ | Display breakout labels |
| Show QM Patterns | ✅ | Display Quasimodo patterns |

### Storyline

| Setting | Default | Purpose |
|---|---|---|
| Show Dashboard | ✅ | Display summary information |
| Dashboard Position | Top Right | Dashboard placement |
| Phase BG Opacity | 92 | Control phase background transparency |

### Setups

| Setting | Default | Purpose |
|---|---|---|
| Show Setup Lines | ✅ | Display entry level lines |
| Enable Refinement | ✅ | Enable 30M/15M entry refinement |

### Confirmations

| Setting | Default | Purpose |
|---|---|---|
| LTF EMA Length | 5 | EMA period for lower-timeframe confirmation |
| Show Sniper Score | ✅ | Display conviction score |
| Min Score for Alert | 5 | Minimum score required to trigger alerts |

---

## Technical Details

- `request.security()` calls used: 11 of 40 available.
- Total `request.*` calls: 13 of 40 available.
- Active levels cap: 25 (configurable).
- Active Quasimodo patterns cap: 5.
- Active trendlines cap: 20.
- Estimated compiled token usage: ~50K (below Pine Script limits).

---

## Best Practices

- Use 1H and 4H charts for the best combination of context and execution precision.
- Use lower pivot settings for more aggressive detection and higher settings for cleaner structure.
- Increase `Max Active Levels` on higher timeframes where zone persistence is more important.
- Lower `Phase BG Opacity` when phase coloring is too prominent.
- Refer to `docs/ENTRY_SETUPS.md` for entry rules, setup validation, and execution examples.

---

## License

This project is released under the MIT License.

---

*Designed for structured analysis, disciplined execution, and professional trade support.*
