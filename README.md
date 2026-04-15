# 👑 Crown Gold Signal

**Premium TradingView Indicator** สำหรับเทรดทอง XAUUSD + Forex majors — สร้างโดย **Crown FX Automation**

[![Pine Script](https://img.shields.io/badge/Pine%20Script-v6-blue.svg)](https://www.tradingview.com/pine-script-docs/)
[![Platform](https://img.shields.io/badge/Platform-TradingView-green.svg)](https://www.tradingview.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](#license)

> *"Signal Indicator สำหรับสายทอง + Forex — Winrate สูง พร้อม TP/SL อัตโนมัติ 4 ระดับ"*

---

## 📦 What's Inside

| File | Purpose |
|------|---------|
| [src/CrownGoldSignal.pine](src/CrownGoldSignal.pine) | **Main indicator** (publish version) |
| [src/CrownGoldSignal_Strategy.pine](src/CrownGoldSignal_Strategy.pine) | **Strategy version** สำหรับ backtest |
| [PRD.md](PRD.md) | Product Requirements Document |
| [CLAUDE.md](CLAUDE.md) | Dev instructions for Claude Code |
| [CHECKLIST.md](CHECKLIST.md) | 30-day launch checklist |

---

## ✨ Features

### 🎯 Signal Engine (3-Condition Confirmation)
สัญญาณจะเกิดเมื่อครบทั้ง 3 เงื่อนไขเท่านั้น:

1. **Trend** — EMA 50 vs EMA 200 + Multi-TF alignment (H1 + H4)
2. **Momentum** — RSI (50-70 BUY / 30-50 SELL) + MACD line > signal
3. **Structure (SMC)** — ราคาแตะ Order Block หรือ FVG หรือมี Break of Structure

### 🛡️ Multi-Level TP/SL System
- **SL**: ATR(14) × 1.5 หรือ swing H/L (เลือกวิธีที่ปลอดภัยกว่า)
- **TP1–TP4**: R:R 1:1 · 1:2 · 1:3 · 1:5
- วาดเส้น horizontal + label บอกราคาทุกระดับ
- Cleanup เส้นเก่าเมื่อเกิด signal ใหม่อัตโนมัติ

### 🧠 Smart Money Concepts (SMC)
- **Order Block** (Bullish + Bearish) วาดเป็นกล่องสี
- **Fair Value Gap (FVG)** 3-candle imbalance detection
- **Break of Structure (BOS)** พร้อม label

### 📐 Auto Fibonacci
- วาด Fib retracement (0, 0.236, 0.382, 0.5, 0.618, 0.786, 1.0) อัตโนมัติจาก swing ล่าสุด
- **Golden Zone** (0.5-0.618) ไฮไลท์สีทอง

### 📊 Multi-TF Dashboard
Info table 17 rows:
- Signal + Entry/SL/TP1–TP4 พร้อมสถานะ ✅/💥
- เทรนด์ของ H1, H4, D1 (arrow up/down)
- RSI, ATR, Session status
- Win/Loss tracker

### ⏰ Session Filter
เทรดเฉพาะ **London (15:00-00:00) + NY (20:00-05:00)** เวลาไทย — ปิดช่วง Asia ที่ sideways

### 🚨 Alert System
- `alertcondition()` แยก: BUY, SELL, TP1-4 hit, SL hit, Pre-alert (2/3 conditions)
- `alert()` ส่ง **JSON webhook** พร้อมใช้กับ Line Notify / Discord / Telegram bot

### 🛡️ Anti-Repaint Guarantee
- `barstate.isconfirmed` บังคับให้ signal เกิดบน closed bar เท่านั้น
- `request.security()` ใช้ `lookahead=barmerge.lookahead_off` ทั้งหมด
- Cross detection ใช้ `close[1]` / `rsi[1]` / `macdLine[1]` ป้องกัน intra-bar flicker
- ทดสอบผ่าน **Bar Replay** — signal ไม่หายไปหลัง bar ปิด

---

## 🚀 Quick Start

### สำหรับลูกค้า (End User)
1. ได้รับ **TradingView username invite** จาก admin ผ่าน Line OA
2. เปิด TradingView → Indicators → เลือก "Invite-only scripts"
3. คลิก **Crown Gold Signal** → Add to chart
4. ตั้งค่า timeframe ที่แนะนำ: **M15 หรือ H1** บน XAUUSD

### สำหรับนักพัฒนา (Dev)
```bash
# Clone repo
git clone https://github.com/thanakitpw/Crown-Gold-Signal.git
cd Crown-Gold-Signal

# เปิด src/CrownGoldSignal.pine ใน TradingView Pine Editor
# Paste → Save → Add to chart
```

---

## 🧪 Testing & Backtest

### Compile Test
เปิด Pine Editor → Paste code → Ctrl+S → ต้องไม่มี error/warning

### Visual Test
- Apply indicator บน XAUUSD M15
- ตรวจ: arrow BUY/SELL, TP/SL lines, OB/FVG boxes, dashboard

### Anti-Repaint Test
1. บันทึก signal บน chart ปัจจุบัน
2. ใช้ **Bar Replay** → ย้อนกลับ 50 bars → เล่น forward
3. Signal ต้องเกิดที่ bar **เดียวกัน** และไม่หายไป

### Backtest (ใช้ `CrownGoldSignal_Strategy.pine`)
| Setting | Value |
|---------|-------|
| Symbol | XAUUSD |
| Timeframe | H1 |
| Period | 2024-01-01 → 2026-12-31 |
| Initial capital | $10,000 |
| Commission | 0.02% |
| Slippage | 2 ticks |

**Target:** Winrate ≥ 85% · Profit Factor ≥ 1.8 · Max DD ≤ 15%

---

## 💰 Pricing

| Tier | Price | Includes |
|------|-------|----------|
| 🆓 **Free** | ฟรี | Signal 1-3 ครั้ง/วัน ใน Line OpenChat |
| 🥉 **Monthly** | **฿599/เดือน** | Full indicator + Dashboard + Alert |
| 🥈 **Yearly** | **฿2,590/ปี** | + VIP Line group + Priority support (ประหยัด 64%) |
| 🥇 **Lifetime** | **฿6,900** | ทุกอย่าง + Future updates ฟรีตลอดชีพ |
| ⭐ **Early Bird** (100 คนแรก) | **฿2,490 Lifetime** | ลด 64% — limited slots |

---

## 🛠️ Architecture

```
src/
├── CrownGoldSignal.pine          # Main indicator (single-file publish version)
├── CrownGoldSignal_Strategy.pine # Strategy version (for backtest)
└── lib/                          # (reserved for future modular refactor)
```

### Code Organization (11 sections in main file)

1. **INPUTS** — 8 grouped panels (🎯 📊 🛡️ 🧠 📐 ⏰ 📱 🎨)
2. **INDICATORS** — EMA, RSI, MACD, ATR
3. **MULTI-TF** — HTF bias via `request.security` (batched tuples)
4. **SMC DETECTION** — OB, FVG, BOS with box/label drawing + cleanup
5. **SESSION FILTER** — Bangkok UTC+7, London + NY
6. **SIGNAL ENGINE** — 3-condition confirmation
7. **RISK MANAGEMENT** — SL/TP calculation + line drawing
8. **AUTO FIBONACCI** — Swing-based levels + Golden Zone
9. **VISUALS** — Arrows + Big labels
10. **DASHBOARD** — 17-row info table (guarded with `barstate.islast`)
11. **ALERTS** — `alertcondition` + JSON webhook via `alert()`

---

## 📋 Development

### Prerequisites
- TradingView account (Premium plan for publish invite-only: $59.95/mo)
- Pine Script v6 knowledge
- Claude Code (optional, instructions in [CLAUDE.md](CLAUDE.md))

### Workflow
1. อ่าน [PRD.md](PRD.md) + [CLAUDE.md](CLAUDE.md)
2. ดู [CHECKLIST.md](CHECKLIST.md) หา task
3. **Invoke skill `pine-script-v6-expert`** ก่อนแก้ `.pine` ทุกครั้ง
4. ก่อน publish → **spawn agent `pine-script-reviewer`** ให้ review
5. Bar Replay test → Strategy backtest → Publish

### Repo Conventions
- **Pine Script v6** เท่านั้น
- **camelCase** functions + variables, `i_` prefix สำหรับ inputs
- English code comments, Thai UI strings
- ใช้ `barstate.isconfirmed` + `lookahead_off` ทุก request.security

---

## 🎯 Roadmap

### ✅ V1.0 (Current)
- 3-condition signal engine
- 4-level TP/SL with line drawing
- SMC (OB + FVG + BOS)
- Auto Fibonacci
- Multi-TF dashboard
- Session filter
- JSON webhook alerts
- Strategy version for backtest

### 🚧 V1.1 (Planned)
- Auto-post signal → Line OpenChat (webhook → Line API)
- Multi-symbol scanner
- Divergence detection
- Retest entry mode

### 🔮 V1.2+
- Trade journal
- Telegram bot integration
- Custom risk profiles
- Payment automation (Stripe/Omise)

---

## 🔒 License

**Proprietary — Licensed to subscribers only.**

© 2026 Crown FX Automation. All rights reserved.
Unauthorized distribution, reverse engineering, or resale is prohibited.

For licensing inquiries: Line OA `@crownfx` (pending)

---

## ⚠️ Disclaimer

การเทรด Forex และทองคำมีความเสี่ยงสูง คุณอาจสูญเสียเงินทั้งหมดที่ลงทุน

- **Past performance is not indicative of future results**
- **Trading involves substantial risk of loss**
- **This indicator is for educational purposes and market analysis only**
- **Not financial advice** — ปรึกษา financial advisor ก่อนลงทุน
- ใช้เงินที่พร้อมจะเสียได้เท่านั้น

---

## 📞 Contact

- 🌐 Website: *(coming soon)*
- 💬 Line OA: *(coming soon)*
- 📘 Facebook: *(coming soon)*
- 📧 Email: agency.bestsolutions@gmail.com

---

**Made with 👑 by Crown FX Automation — Bangkok, Thailand**
