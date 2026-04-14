# MSNR Entry Setups Strategy

This document outlines the entry models, structural rules, and execution conditions strictly utilizing the MSNR (Malaysian SNR) framework. The `MSNR_Entry_Setups.pine` indicator is built specifically to highlight these setups on Lower Timeframes (LTF) like 1m, 5m, and 15m.

## 1. Core Structural Concepts
Before taking any entries, it is vital to distinguish the structural validity of the setup when price touches an HTF (Higher Timeframe) level. 

### External Breakout (Valid)
An external breakout occurs when the price breaks the **last A-shape level (for bullish setups)** or **V-shape level (for bearish setups)** that had formed *before* the price touched the fresh SNR level or trendline. This breakout confirms a genuine structural shift.

### Internal Breakout (Invalid / Noise)
An internal breakout occurs when the price breaks an A-shape or V-shape level that formed *after* the price had already touched the fresh SNR level. This is considered internal noise, and the breakout is ignored by the indicator.

---

## 2. Category 1: QMS Setups (Catching the Early Trend)
These entry models are used at the very beginning of a storyline when a Quasimodo (QM) pattern is forming.

### SBR / RBS (Support Becomes Resistance / Resistance Becomes Support)
- **Bullish (RBS):** The first "A-shape" resistance formed just before the drop to the Apex. Price breaks above it, making it the new RBS line.
- **Bearish (SBR):** The first "V-shape" support formed just before the rise to the Apex. Price breaks below it, making it the new SBR line.
- *Execution:* Enter on the pullback to test the SBR/RBS line.

### Left Shoulder (LS) Fallback
The level formed just before the apex of the QM pattern.
- *Execution:* If price fails to hold at the SBR/RBS line, this acts as the secondary/fallback entry point. A strong engulfing reversal from the LS is required.

### Advanced Setups (Monitored Visually)
- **Apex Setup:** Absolute turning point where the price initially reverses.
- **Early Right Shoulder (ERS):** A small extra "mini A/V" formed just before the breakout.
- **GAP QMS & Failed QM:** Trading HTF gaps and trading the immediate reversal when an established QM structure breaks the wrong way.

---

## 3. Category 2: Continuation Setups (Riding the Momentum)
Used in the middle and ending phases of a storyline.

### 30m / 15m Mini Storyline Setups (C.SNR)
When a 30m structure perfectly aligns with a 15m structure, it triggers a Continuation SNR (C.SNR) setup. These are prioritized for day traders/scalpers because the confirmation windows are significantly faster than 4H structures.

### MTF Gap Alignments
Gaps are strictly traded only when multiple timeframes overlap perfectly:
- **4H Gap Alignment:** The 4H gap MUST overlap with a 1H Gap + a 1H Classic (A/V) + a 30m Classic.
- **1H Gap Alignment:** The 1H gap MUST overlap with a 30m Classic + a 15m Classic.

---

## 4. LTF Execution Triggers (The Sniper Entry)
Never enter a trade blindly just because the price hits an SBR, LS, or C.SNR line. Once the price reaches the highlighted setup zone, you drop to the 5m or 1m chart to wait for a strict execution trigger.

The indicator visualizes these with `🚀 EXECUTE` markers:
1. **5Min EMA Break:** Entering immediately after a candle violently breaks and closes past the 5-period Exponential Moving Average (EMA).
2. **Engulfing Rejection:** Entering after a strong engulfing candle rejects your established level (e.g., at the Left Shoulder).
3. **Trendline Breakout:** (Manual) Entering after an engulfing candle breaks a short-term 1Min or 5Min visual trendline drawn out of the retracement.
4. **Breaking Gap:** (Manual) Entering when price pulls back to retest a newly broken LTF gap.
