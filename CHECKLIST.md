# CHECKLIST.md — Crown Gold Signal

**Last Updated:** 2026-04-15
**Status Legend:** ⬜ Not started · 🟡 In progress · ✅ Done · ⏸️ Blocked · ❌ Cancelled

---

## Phase 1: Core Indicator Development (Pine Script)

### 1.1 Project Skeleton
- ⬜ สร้าง `src/CrownGoldSignal.pine` พร้อม `//@version=6` header + copyright comment
- ⬜ สร้าง `src/lib/` folder + empty files: `signal_engine.pine`, `smc.pine`, `fibonacci.pine`, `dashboard.pine`, `risk.pine`, `session.pine`
- ⬜ สร้าง `src/CrownGoldSignal_Strategy.pine` (strategy version stub)
- ⬜ ตั้งค่า `indicator()` declaration: title, shorttitle, overlay=true, max_lines_count=500, max_boxes_count=500, max_labels_count=500

### 1.2 Input Panel (Input Settings)
- ⬜ Group "🎯 Signal Settings" — EMA fast (50), EMA slow (200), RSI length (14), MACD (12/26/9)
- ⬜ Group "📊 Multi-Timeframe" — HTF1 (H1), HTF2 (H4) dropdown selection
- ⬜ Group "🛡️ Risk Management" — ATR length (14), ATR multiplier (1.5), R:R ratios (1/2/3/5)
- ⬜ Group "🧠 SMC Settings" — Enable OB (bool), Enable FVG (bool), OB lookback (20)
- ⬜ Group "📐 Fibonacci" — Enable Fib (bool), Show Golden Zone (bool)
- ⬜ Group "⏰ Session Filter" — Enable Session Filter (bool), London/NY toggle
- ⬜ Group "📱 Dashboard" — Show dashboard (bool), Position dropdown
- ⬜ Group "🎨 Visual" — Entry/SL/TP colors, Line styles
- ⬜ ใส่ tooltip ทุก input ให้ลูกค้าเข้าใจ

### 1.3 Signal Engine (Core Logic) — `lib/signal_engine.pine`
- ⬜ Condition 1: Trend filter — EMA50 > EMA200 + HTF alignment via `request.security()` with `lookahead=barmerge.lookahead_off`
- ⬜ Condition 2: Momentum — RSI range check (50-70 BUY, 30-50 SELL) + MACD line > signal
- ⬜ Condition 3: Structure — price touches latest OB or FVG zone
- ⬜ Combine 3/3 → `isBuySignal`, `isSellSignal` booleans
- ⬜ Guard: use `barstate.isconfirmed` เพื่อป้องกัน repaint
- ⬜ Guard: ใช้ `close[1]` แทน `close` ใน cross detection
- ⬜ Track last signal (var) → ห้าม print signal ซ้ำบน bar เดียวกัน

### 1.4 SMC Detection — `lib/smc.pine`
- ⬜ Bullish Order Block detection (last down candle before up impulse)
- ⬜ Bearish Order Block detection (last up candle before down impulse)
- ⬜ Bullish FVG: `low[0] > high[2]`
- ⬜ Bearish FVG: `high[0] < low[2]`
- ⬜ BOS detection (break swing high/low)
- ⬜ วาด OB เป็น `box.new()` สีเขียว/แดง transparent
- ⬜ วาด FVG เป็น `box.new()` สีเทา
- ⬜ Cleanup old boxes (เก็บ array + ลบตัวเก่าเกิน 10 zones)

### 1.5 Risk Management — `lib/risk.pine`
- ⬜ Function `calculateSL(isBuy, atr, swingHigh, swingLow)` → pick farther from entry
- ⬜ Function `calculateTPLevels(entry, sl)` → return [TP1, TP2, TP3, TP4]
- ⬜ Draw SL line (red) + label
- ⬜ Draw Entry line (blue) + label
- ⬜ Draw TP1-TP4 lines (green gradient) + labels with price
- ⬜ Line extend to right → `line.new(..., extend=extend.right)`
- ⬜ Cleanup old lines/labels เมื่อ signal ใหม่เกิด (ใช้ array management)

### 1.6 Session Filter — `lib/session.pine`
- ⬜ Define London session (15:00-00:00 Bangkok time)
- ⬜ Define NY session (20:00-05:00 Bangkok time)
- ⬜ Function `isActiveSession()` → bool
- ⬜ Integrate into signal engine (skip signal outside session if enabled)

### 1.7 Dashboard UI — `lib/dashboard.pine`
- ⬜ `table.new(position.top_right, 2, 16)` with dark background
- ⬜ Header row: "👑 CROWN GOLD SIGNAL" (gold color #f7b500)
- ⬜ Row: Signal (🟢 BUY / 🔴 SELL / ⚪ WAIT)
- ⬜ Row: Entry, SL, TP1, TP2, TP3, TP4 (with prices)
- ⬜ Row: Trend M15 / H1 / H4 / D1 (arrows up/down)
- ⬜ Row: RSI value, ATR value
- ⬜ Row: Session status (London/NY/Off)
- ⬜ Row: Last signal result (TP hit / SL hit / Running)
- ⬜ Update เฉพาะ `barstate.islast` เพื่อ performance

### 1.8 Visual Markers
- ⬜ Arrow BUY: `plotshape(isBuySignal, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.normal)`
- ⬜ Arrow SELL: `plotshape(isSellSignal, style=shape.triangledown, location=location.abovebar, color=color.red, size=size.normal)`
- ⬜ Big label "BUY NOW" / "SELL NOW" ด้วย `label.new()` ขนาดใหญ่

### 1.9 Auto Fibonacci — `lib/fibonacci.pine`
- ⬜ Detect latest swing high + swing low (lookback 50-100 bars)
- ⬜ Draw Fib levels: 0, 0.236, 0.382, 0.5, 0.618, 0.786, 1.0
- ⬜ Highlight Golden Zone (0.5-0.618) ด้วย `box.new()` transparent
- ⬜ Auto-update เมื่อ new swing เกิด (cleanup เส้นเก่า)

### 1.10 Alert System
- ⬜ `alertcondition(isBuySignal, "Crown Gold BUY", "...")`
- ⬜ `alertcondition(isSellSignal, "Crown Gold SELL", "...")`
- ⬜ `alertcondition(tp1Hit, ...)`, TP2/TP3/TP4 hits
- ⬜ `alertcondition(slHit, "SL Hit", "...")`
- ⬜ Pre-alert: 2/3 conditions met → "กำลังจะมี signal"
- ⬜ JSON webhook message format (Line/Discord-ready)
  ```json
  {"symbol":"{{ticker}}","side":"BUY","entry":3935.00,"sl":3906.31,"tp1":3963.66,...}
  ```

### 1.11 Strategy Version (for Backtest)
- ⬜ Copy main logic → `CrownGoldSignal_Strategy.pine`
- ⬜ Replace `indicator()` with `strategy()`
- ⬜ `strategy.entry()` on buy/sell signals
- ⬜ `strategy.exit()` for TP/SL (partial close: 30%/30%/25%/15%)
- ⬜ Config: initial_capital=10000, commission=0.02%, slippage=2 ticks

---

## Phase 2: Testing & QA

### 2.1 Compile Test
- ⬜ Pine Editor save ไม่มี error
- ⬜ Add to chart ไม่มี runtime error
- ⬜ Merge lib/*.pine → single `CrownGoldSignal.pine` (manual copy หรือ build script)

### 2.2 Visual Test
- ⬜ XAUUSD M15 — signals วางถูกตำแหน่ง
- ⬜ XAUUSD H1 — ทดสอบซ้ำ
- ⬜ EURUSD, GBPUSD, USDJPY — signal ทำงานได้
- ⬜ Dashboard แสดงข้อมูลครบ + update realtime
- ⬜ TP/SL lines แสดงถูก + extend ขวา + label ราคาชัด
- ⬜ SMC boxes (OB/FVG) แสดงถูก
- ⬜ Fib levels update เมื่อ swing ใหม่

### 2.3 Anti-Repaint Test (CRITICAL)
- ⬜ บันทึก signal positions บน current chart
- ⬜ Bar Replay ย้อนกลับ 50 bars → เล่น forward
- ⬜ Signal ต้องเกิดที่ bar เดียวกัน — **ไม่หายไป**
- ⬜ ถ้าหาย → debug `lookahead`, `barstate.isconfirmed`, `close[1]` usage

### 2.4 Alert Test
- ⬜ Create alert บน TradingView → trigger ได้
- ⬜ Test webhook → ส่งถึง Discord/Line ได้จริง
- ⬜ JSON format parse ได้ถูก

### 2.5 Backtest (Strategy Version)
- ⬜ XAUUSD H1, 2024-01-01 ถึง 2026-04-15
- ⬜ Target: Winrate ≥ 85%, PF ≥ 1.8, Max DD ≤ 15%
- ⬜ ถ้าไม่ผ่าน → tune parameters
- ⬜ Screenshot ผลเก็บไว้ทำ marketing
- ⬜ Run XAUUSD M15 + H4 (extra timeframes)
- ⬜ Run EURUSD H1 (confirm robustness)

---

## Phase 3: Publishing

### 3.1 Pre-Publish
- ⬜ ใส่ copyright header ทุกไฟล์
- ⬜ ลบ debug code / unused variables
- ⬜ Review input defaults ให้เหมาะกับมือใหม่
- ⬜ เขียน description สำหรับ TradingView publish page
- ⬜ Screenshot chart สวยๆ 3-5 รูป (สำหรับ TradingView listing)

### 3.2 TradingView Invite-Only Publish
- ⬜ Admin มี TradingView Premium plan ($59.95/mo)
- ⬜ Pine Editor → "Publish Script" → เลือก "Invite-only"
- ⬜ กรอก description + tags (Gold, XAUUSD, Signal, SMC, Thai)
- ⬜ Submit → รอ review (1-3 วัน)
- ⬜ หลัง approve → test "Manage Access" เพิ่ม/ลบ user

---

## Phase 4: Documentation

### 4.1 Customer-Facing Docs (ไทย)
- ⬜ `docs/user_manual.md` — วิธีใช้ indicator, อธิบาย signal, input settings
- ⬜ `docs/setup_guide.md` — วิธี add script, setup alert, setup webhook
- ⬜ `docs/backtest_report.md` — ผล backtest + disclaimer + screenshots
- ⬜ FAQ document — คำถามที่มือใหม่ถามบ่อย

### 4.2 Internal Docs
- ⬜ Version history (changelog)
- ⬜ Admin guide — วิธี invite/revoke ลูกค้า
- ⬜ Support script — ตอบปัญหาทางเทคนิคยอดฮิต

---

## Phase 5: Marketing Assets

### 5.1 Landing Page
- ⬜ `marketing/landing_page_copy.md` — hero, features, pricing, testimonial, CTA
- ⬜ เลือก domain + hosting (Webflow/Framer/WordPress)
- ⬜ ใส่ pricing: 599฿/เดือน, 2,590฿/ปี, Lifetime TBD
- ⬜ Early Bird counter (เหลือ X/100 คน)
- ⬜ Line OA button (prominent CTA)
- ⬜ Demo video embed (30-60 วินาที)
- ⬜ Disclaimer footer (past performance, trading risk)

### 5.2 Social Media Content
- ⬜ `marketing/facebook_ads.md` — ad copy x3 variations
- ⬜ TikTok scripts x5 (signal clips, bar replay, testimonial)
- ⬜ YouTube intro video — "Crown Gold Signal คืออะไร" (3-5 นาที)
- ⬜ Facebook Page cover + profile
- ⬜ Post schedule — 14 วันแรก (pre-launch teaser)

### 5.3 Line Assets
- ⬜ `marketing/line_oa_scripts.md` — scripts ตอบลูกค้า 20 sceniarios
- ⬜ Line OpenChat rules + welcome message
- ⬜ Auto-reply templates ใน Line OA
- ⬜ Rich menu design สำหรับ Line OA

### 5.4 Brand Assets
- ⬜ Logo Crown Gold Signal (หรือใช้ emoji 👑 ชั่วคราว)
- ⬜ Color palette + typography guidelines
- ⬜ Screenshots สวยๆ ของ indicator บน chart
- ⬜ Before/After mockup (ก่อน/หลังใช้ indicator)

### 5.5 Pricing Page
- ⬜ `marketing/pricing_page.md` — 3 tiers side-by-side
- ⬜ FAQ section (refund, update, compatibility)
- ⬜ Payment method instructions (PromptPay/Bank transfer)
- ⬜ Terms of Service + Refund Policy

---

## Phase 6: Launch Operations

### 6.1 Pre-Launch
- ⬜ Beta tester recruitment (5-10 คน) จาก Line OpenChat
- ⬜ Beta test 1-2 สัปดาห์ — เก็บ feedback
- ⬜ แก้ bug จาก beta feedback
- ⬜ Waitlist collection (email form) — ก่อน launch 2 สัปดาห์

### 6.2 Launch Day
- ⬜ Post ประกาศ launch บน Facebook + TikTok + YouTube
- ⬜ Email blast ไป waitlist
- ⬜ Live demo ใน Line OpenChat
- ⬜ Early Bird counter เปิด (100 คน @ราคา lifetime ลดพิเศษ)
- ⬜ Admin standby ตอบคำถาม + ส่ง invite

### 6.3 Post-Launch (7-30 วัน)
- ⬜ Daily: ตอบคำถามใน Line OA + OpenChat
- ⬜ Weekly: Post signal performance recap
- ⬜ Collect testimonials (ขออนุญาตใช้)
- ⬜ Track KPIs: customers, MRR, OpenChat members, refund rate
- ⬜ Plan V1.1 features based on feedback

---

## Phase 7: V1.1+ (Future)

### 7.1 Automation
- ⬜ Auto-post signal ไป Line OpenChat (webhook → Line API)
- ⬜ Payment automation (Stripe/Omise integration)
- ⬜ Auto-invite บน TradingView (API ถ้ามี หรือ RPA)
- ⬜ Customer dashboard (subscription status)

### 7.2 New Features
- ⬜ Multi-symbol scanner
- ⬜ Trade journal
- ⬜ Telegram bot
- ⬜ Divergence detection
- ⬜ Smart retest entry

---

## Open Questions / Decisions Needed

- ❓ Lifetime price ใหม่ (แนะนำ 5,900-7,900฿)
- ❓ Early Bird Lifetime price ใหม่ (แนะนำ 1,990-2,990฿)
- ❓ Domain name สำหรับเว็บไซต์
- ❓ Logo design — ทำเองหรือจ้าง?
- ❓ Payment processor สำหรับ V1 — PromptPay manual ก่อน?
- ❓ Refund policy details (7 วัน, เงื่อนไข?)
