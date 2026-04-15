# Crown Gold Signal — Product Requirements Document (PRD)

**Version:** 1.0 Draft
**Date:** 2026-04-15
**Owner:** Crown FX Automation
**Status:** Pre-Development

---

## 1. Product Overview

### 1.1 Product Name
**Crown Gold Signal** (working title — อาจเปลี่ยนภายหลัง)

### 1.2 Product Type
Premium TradingView Indicator (Pine Script v6) — invite-only distribution

### 1.3 One-Liner
> "Signal Indicator สำหรับสายทอง + Forex Winrate 90%+ พร้อม TP/SL อัตโนมัติ 4 ระดับ — ใช้ง่าย แม่นจริง บน TradingView"

### 1.4 Vision
สร้าง product ที่เป็น **category leader ในตลาดไทย** สำหรับ TradingView gold indicator โดยอาศัยจุดแข็ง:
- Multi-confirmation signal แม่นยำ (90%+ claim)
- Visual ชัดเจน มืออาชีพ (TP1-TP4 + SL + Dashboard)
- Community-driven (Line OpenChat + Free signals funnel)
- Subscription revenue model (recurring + lifetime options)

---

## 2. Target Market

### 2.1 Primary Persona
**"นักเทรดมือใหม่ถึงกลาง สายทอง"**
- อายุ: 25-45 ปี
- เทรด XAUUSD เป็นหลัก, Forex majors เป็นรอง
- ใช้ TradingView เป็น charting platform หลัก (Free หรือ Essential plan)
- Timeframe ที่ใช้: M5, M15, H1, H4
- Pain points:
  - ไม่รู้จะเข้าเมื่อไหร่ (ต้องการ arrow ชัดๆ)
  - ไม่รู้จะตั้ง TP/SL ที่ไหน
  - เคยใช้ indicator ฟรี → ไม่แม่น
  - อยากได้ community เทรดด้วยกัน

### 2.2 Secondary Persona
**"เทรดเดอร์ที่ต้องการ signal เสริม"**
- มีระบบของตัวเองแล้ว
- ต้องการ indicator สำหรับ **confirmation** เข้าออเดอร์

### 2.3 Market Size (ไทย)
- ผู้ใช้ TradingView ในไทย: ~500,000+ คน
- สายทอง: ~150,000 คน
- Target conversion (V1): 0.1% = 150 paid customers/ปี

---

## 3. Business Model

### 3.1 Pricing Tiers

| Tier | ราคา | ระยะเวลา | Features |
|------|------|---------|----------|
| **Free** | ฟรี | ตลอดไป | Signal ใน Line OpenChat (manual/auto post) — 1-3 signals/day |
| **Monthly** | 990 บาท/เดือน | 1 เดือน | Full indicator access + Dashboard + Alert |
| **Yearly** | 8,900 บาท/ปี | 12 เดือน (ประหยัด 25%) | + VIP Line group + Priority support |
| **Lifetime** ⭐ | 19,900 บาท | ตลอดชีพ + Updates ฟรี | ทุกอย่าง + Future features + 1-on-1 onboarding |

### 3.2 Launch Promo
- **Early Bird 100 คนแรก:** Lifetime ราคา **4,990 บาท** (ลด 75% จาก 19,900)
- **วิธี create urgency:**
  - Counter "เหลืออีก X คน" บนหน้าเว็บ
  - Deadline: 7-14 วันหลัง launch

### 3.3 Payment Method
- โอนผ่านธนาคารไทย (PromptPay/Bank transfer) — ผ่าน Line OA
- บัตรเครดิต/เดบิต (ผ่าน Stripe หรือ Omise ในเว็บ — V2)
- TrueMoney Wallet (optional)

### 3.4 Revenue Projection (ปีแรก — Conservative)

| Month | Monthly Subs | Yearly | Lifetime | Revenue |
|-------|-------------|--------|----------|---------|
| 1 (Launch) | 20 | 5 | 30 (early bird @4,990) | ~238,350 บาท |
| 2-3 | 40 | 10 | 10 | ~278,400 บาท |
| 4-6 | 60 | 15 | 15 | ~478,050 บาท |
| 7-12 | 100/เดือน | 30/ปี | 10/เดือน | ~2,262,000 บาท |
| **Total ปี 1** | | | | **~3.2M บาท** |

---

## 4. Distribution & Funnel

### 4.1 Sales Funnel

```
┌─────────────────────────────────────────────────────────────┐
│  AWARENESS                                                   │
│  ├─ Facebook Page (organic + paid ads)                       │
│  ├─ TikTok/Reels (signal clips + backtest replay)            │
│  ├─ YouTube (tutorials + free signals)                       │
│  └─ เว็บไซต์ (Landing page + SEO)                            │
└────────────────┬────────────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────────────────────┐
│  INTEREST  →  Line OpenChat (Free community)                 │
│  ├─ Free signals 1-3 ครั้ง/วัน                              │
│  ├─ Educational content                                      │
│  └─ Testimonials + win screenshots                           │
└────────────────┬────────────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────────────────────┐
│  DECISION  →  Line OA (1-on-1)                               │
│  ├─ ตอบคำถาม                                                 │
│  ├─ แสดง backtest + live demo                                │
│  └─ Close การขาย                                             │
└────────────────┬────────────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────────────────────┐
│  PURCHASE  →  โอนเงิน → ส่ง TradingView username             │
│  └─ Admin เพิ่ม invite บน TradingView (manual)              │
└────────────────┬────────────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────────────────────┐
│  RETENTION  →  VIP Line Group + Monthly updates              │
└─────────────────────────────────────────────────────────────┘
```

### 4.2 Free Signal Strategy (Line OpenChat)
- **ความถี่:** 1-3 signals/วัน (XAUUSD เท่านั้น)
- **วิธีส่ง:**
  - **Phase 1 (MVP):** Admin พิมพ์ส่งเอง (manual) — ใช้ indicator เป็นตัวช่วยตัดสินใจ
  - **Phase 2 (V1.1):** Auto-post จาก TradingView alert → Webhook → Line API
- **Format:**
  ```
  🟢 XAUUSD BUY SIGNAL
  Entry: 3,935.00
  SL: 3,906.31
  TP1: 3,963.66 (1:1)
  TP2: 3,992.35 (1:2)
  TP3: 4,021.03 (1:3)

  ✨ อยากได้ signal ครบทุก pair + dashboard → ทัก Line OA
  ```

### 4.3 Channels

| Channel | วัตถุประสงค์ | Content Type |
|---------|-------------|---------------|
| Facebook Page | Awareness + Traffic | Signal result, testimonial, backtest clip |
| TikTok | Viral + Lead gen | ลูกศรเข้า/ออก real-time, Bar Replay clips |
| YouTube | Education + Trust | Tutorial การใช้งาน, วิเคราะห์ทอง รายสัปดาห์ |
| เว็บไซต์ | Conversion + Brand | Landing page, pricing, demo video, Line OA link |
| Line OpenChat | Community + Free tier | Free signals, discussions, market news |
| Line OA | Sales + Support | 1-on-1 closing, onboarding |

---

## 5. Product Features

### 5.1 Core Features (MVP — V1.0)

#### 5.1.1 Signal Engine (3-Condition Confirmation)
**Condition 1 — Trend (HTF Filter):**
- EMA 50 > EMA 200 บน current timeframe (BUY)
- Price above EMA 200 บน H1/H4 (HTF bias)

**Condition 2 — Momentum:**
- RSI (14) ระหว่าง 50-70 สำหรับ BUY, 30-50 สำหรับ SELL
- MACD line > Signal line (BUY)

**Condition 3 — Structure (SMC):**
- ราคาอยู่ใน/แตะ Order Block zone หรือ FVG (Fair Value Gap)
- หรือ Break of Structure (BOS) ล่าสุด

**→ Arrow จะขึ้นเมื่อครบ 3/3 เงื่อนไขเท่านั้น** (แม่นยำ + กรอง false signal)

#### 5.1.2 Multi-Level TP/SL System
- **SL:** คำนวณจาก ATR(14) × 1.5 หรือ swing low/high (เลือกวิธีที่ safer)
- **TP1:** R:R 1:1 — ปิด 30% ของ position
- **TP2:** R:R 1:2 — ปิด 30%
- **TP3:** R:R 1:3 — ปิด 25%
- **TP4:** R:R 1:5 — ปิด 15% (runner)
- แสดงเป็น **horizontal line + price label** บนชาร์ต
- สีต่างกัน: TP = เขียว, SL = แดง, Entry = น้ำเงิน

#### 5.1.3 Info Dashboard (มุมขวาบน)
```
┌──────────────────────────────┐
│  CROWN GOLD SIGNAL           │
├──────────────┬───────────────┤
│ Signal       │ 🟢 BUY        │
│ Entry        │ 3,935.00      │
│ SL           │ 3,906.31      │
│ TP1 (1:1)    │ 3,963.66      │
│ TP2 (1:2)    │ 3,992.35      │
│ TP3 (1:3)    │ 4,021.03      │
│ TP4 (1:5)    │ 4,078.40      │
├──────────────┼───────────────┤
│ Trend M15    │ 🟢 Bullish    │
│ Trend H1     │ 🟢 Bullish    │
│ Trend H4     │ 🟢 Bullish    │
│ RSI (14)     │ 58            │
│ ATR (14)     │ 28.7          │
├──────────────┼───────────────┤
│ Risk         │ 1.5%          │
│ Lot Suggest  │ 0.15          │
│ Win Rate     │ 90.5%         │
└──────────────┴───────────────┘
```

#### 5.1.4 Alert System
- Alert เมื่อเกิด signal ใหม่ (BUY/SELL)
- Alert เมื่อชน TP1/TP2/TP3/TP4
- Alert เมื่อชน SL
- รองรับ: Popup, Sound, Email, SMS (ตาม TradingView plan), Webhook
- Webhook → Line/Discord/Telegram (setup guide สำหรับลูกค้า)

#### 5.1.5 Symbols & Timeframes Support
- **Primary:** XAUUSD (Gold)
- **Secondary:** EURUSD, GBPUSD, USDJPY, XAGUSD
- **Timeframes:** M5, M15, H1, H4 (Optimized)
- ใช้งานบน TF อื่นได้ แต่ผลอาจต่างไปจาก backtest

### 5.2 Premium Features (V1.0)

#### 5.2.1 SMC Visualization
- Order Block zones (bullish/bearish) — กล่องสีน้ำเงิน/ชมพู
- Fair Value Gap (FVG) — กล่องสีเทา
- BOS (Break of Structure) labels
- Liquidity zones (Equal Highs/Lows)

#### 5.2.2 Auto Fibonacci
- วาด Fib retracement จาก swing high/low ล่าสุดอัตโนมัติ
- แสดงเลเวล: 0, 0.236, 0.382, 0.5, 0.618, 0.786, 1.0
- Highlight **Golden Zone** (0.5-0.618)
- Update อัตโนมัติเมื่อเกิด new swing

#### 5.2.3 Multi-TF Trend Table (ใน Dashboard)
- แสดง trend direction ของ M15 / H1 / H4 / D1 พร้อมกัน
- ช่วยให้รู้ bias ก่อนเข้าออเดอร์

### 5.3 Future Features (V1.1+)

| Feature | Priority | Release |
|---------|----------|---------|
| Auto-post signal to Line API | High | V1.1 |
| Multi-symbol scanner (table) | Medium | V1.1 |
| Trade journal (log signals + results) | Medium | V1.2 |
| Divergence detection | Low | V1.2 |
| Custom risk profiles | Low | V1.3 |
| Telegram bot integration | Medium | V1.2 |

---

## 6. Technical Specifications

### 6.1 Platform
- **TradingView** (exclusively — no MT4/MT5 in V1)

### 6.2 Language
- **Pine Script v6** (latest — ใช้ความสามารถใหม่ทั้งหมด)

### 6.3 Distribution Method
- **Invite-only script** — ลูกค้าส่ง TradingView username → Admin กด "Add User" manually
- Script จะซ่อน source code → ป้องกัน piracy

### 6.4 File Structure (ตั้งใจให้ clean)
```
Crown Gold Signal/
├── PRD.md                          # This document
├── CLAUDE.md                       # Instructions for Claude Code
├── CHECKLIST.md                    # Day-by-day development tasks
├── README.md                       # Project overview
├── src/
│   ├── CrownGoldSignal.pine        # Main indicator (single file for TradingView)
│   ├── CrownGoldSignal_Strategy.pine  # Strategy version (for backtesting)
│   └── lib/
│       ├── signal_engine.pine      # 3-condition logic
│       ├── smc.pine                # Order Block + FVG detection
│       ├── fibonacci.pine          # Auto fib
│       ├── dashboard.pine          # UI table
│       └── risk.pine               # SL/TP/Lot calculation
├── docs/
│   ├── user_manual.md              # คู่มือลูกค้า (ไทย)
│   ├── backtest_report.md          # ผล backtest (marketing material)
│   └── setup_guide.md              # วิธี setup alert/webhook
├── marketing/
│   ├── landing_page_copy.md        # Copy สำหรับเว็บไซต์
│   ├── facebook_ads.md             # Ad copy
│   ├── line_oa_scripts.md          # Script ตอบลูกค้า
│   └── pricing_page.md             # Pricing + FAQ
└── assets/
    ├── screenshots/                # Screenshots สำหรับ marketing
    └── demo_videos/                # Clip แนะนำ
```

**หมายเหตุ:** TradingView ไม่รองรับ multi-file includes → ตอน publish ต้อง merge `lib/*.pine` เข้า main file โดยใช้ build script หรือ manual copy

### 6.5 Key Pine Script Features ที่ใช้
- `indicator()` / `strategy()` declaration
- `request.security()` — multi-TF data
- `table.new()` — Dashboard UI
- `line.new()`, `box.new()`, `label.new()` — TP/SL visualization
- `alertcondition()` / `alert()` — Alert system
- `ta.ema()`, `ta.rsi()`, `ta.macd()`, `ta.atr()` — Indicators
- Custom SMC detection functions

---

## 7. Marketing & Branding

### 7.1 Brand Positioning
> "Premium TradingView Signal Indicator สำหรับสายทองไทย — Winrate 90%+ ใช้งานง่าย เห็น TP/SL ชัดเจน"

### 7.2 Key Marketing Claims (Tier A — Aggressive)
- ✅ **"Winrate 90%+"** (จาก backtest — ต้องมีหลักฐาน screenshot)
- ✅ **"4 TP ชัดเจน เห็นภาพ"**
- ✅ **"ใช้บน TradingView ไม่ต้องลง MT4/MT5"**
- ✅ **"เริ่มต้นแค่ 990 บาท/เดือน"**
- ✅ **"Community Line OpenChat สายทองที่ active ที่สุด"**

### 7.3 Differentiation จากคู่แข่ง (Long Trade Academy — Early Edge Gold)

| Feature | Early Edge Gold | **Crown Gold Signal** |
|---------|-----------------|----------------------|
| Platform | MT5 | **TradingView** ✅ (user-friendly) |
| Pricing | 3,500-17,900 บาท | **990/ปี/Lifetime** ✅ (flexible) |
| Free tier | ❌ | **✅ Free signals ใน OpenChat** |
| Multi-TF Dashboard | Limited | **✅ Full M15/H1/H4/D1** |
| SMC overlay | ❌ | **✅ Order Block + FVG** |
| Auto Fibonacci | ❌ | **✅ Auto draw** |
| Community | Private | **✅ Line OpenChat สาธารณะ** |

### 7.4 Content Marketing Plan (Pre-launch 4 สัปดาห์)
- **Week -4:** ประกาศในเพจ "กำลังพัฒนา" + teaser video
- **Week -3:** แชร์ backtest results + early bird signup form (เก็บ email)
- **Week -2:** Live demo ในกลุ่ม + interview beta testers
- **Week -1:** Countdown + urgency (เหลือ 7 วัน) + waiting list
- **Launch Day:** เปิดขาย early bird 100 คนแรก

---

## 8. Success Metrics (KPIs)

### 8.1 Development KPIs
- Pine Script compile ไม่มี error/warning
- Backtest winrate บน XAUUSD H1 ช่วง 2024-2026 ≥ 85%
- Backtest Profit Factor ≥ 1.8
- Max Drawdown ≤ 15%

### 8.2 Business KPIs (Year 1)
- Paid customers: **300 คน** (conservative) → 600 (stretch)
- MRR (Month 12): **≥ 100,000 บาท**
- Line OpenChat members: **≥ 3,000 คน**
- Page followers: **≥ 10,000 คน**
- Refund rate: **< 5%**

### 8.3 Customer KPIs
- Customer satisfaction (CSAT): **≥ 4.5/5**
- Churn rate (monthly subs): **< 15%**
- Upgrade rate (Monthly → Yearly/Lifetime): **≥ 20%**

---

## 9. Risks & Mitigation

| Risk | Impact | Mitigation |
|------|--------|-----------|
| Winrate ไม่ถึง 90% จริง | High | ปรับ parameter จน backtest ผ่าน + disclaimer "past performance ≠ future" |
| TradingView ban script | Critical | ปฏิบัติตาม House Rules, ไม่ทำ spam/misleading |
| Piracy (share script) | Medium | Invite-only + track usage + ToS strong |
| คู่แข่งทำตาม | Medium | Speed to market + community lock-in + brand |
| Line OA ถูก block | Medium | Multi-channel (Facebook DM, เว็บฟอร์ม) backup |
| Refund request เยอะ | Medium | Policy ชัดเจน: 7-day refund, ห้าม refund หลังใช้ signal ทำกำไรแล้ว |

---

## 10. Timeline (High-Level)

| Phase | Duration | Deliverables |
|-------|----------|--------------|
| **Day 1-3: Core Development** | 3 วัน | Signal Engine + TP/SL + Dashboard + Alert (MVP) |
| **Day 4-5: Premium Features** | 2 วัน | SMC + Auto Fibo + Multi-TF + Strategy version |
| **Day 6-7: Testing & Optimization** | 2 วัน | Backtest + Parameter tuning + Bug fix |
| **Day 8-10: Marketing Assets** | 3 วัน | Landing page + Ads + Line OA scripts + Demo video |
| **Day 11-14: Pre-launch** | 4 วัน | Teaser + Waitlist + Beta test |
| **Day 15: Launch** | 1 วัน | Open Early Bird + Go live |
| **Day 16-30: Post-launch** | 15 วัน | Support + Iterate + Community building |

**Total: ~30 วัน จาก zero → launched**

---

## 11. Appendix

### 11.1 References
- Long Trade Academy — Early Edge Gold (reference competitor)
- LuxAlgo — SMC Indicator (reference for SMC logic)
- TradingView Pine Script v6 Docs: https://www.tradingview.com/pine-script-docs/
- MQL5 Article on SMC: https://www.mql5.com/en/articles/16340

### 11.2 Glossary
- **SMC:** Smart Money Concepts — institutional trading framework
- **FVG:** Fair Value Gap — price imbalance zone
- **BOS:** Break of Structure — trend reversal signal
- **CHoCH:** Change of Character — early trend change
- **R:R:** Risk-to-Reward ratio
- **HTF:** Higher Timeframe
- **TF:** Timeframe
- **OA:** Official Account (Line)

---

**เอกสารนี้เป็น living document — จะอัปเดตตาม progress และ feedback**
