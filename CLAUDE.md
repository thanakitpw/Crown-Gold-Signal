# CLAUDE.md — Crown Gold Signal (TradingView Indicator)

## Project
สร้าง **Premium TradingView Indicator** ชื่อ **Crown Gold Signal** แบรนด์ Crown FX Automation
สำหรับ signal trading ทอง (XAUUSD) + Forex majors — winrate claim 90%+ ขายแบบ subscription

## Tech Stack
- **Language:** Pine Script **v6** (latest)
- **Platform:** TradingView (exclusively — ไม่ทำ MT4/MT5)
- **Distribution:** Invite-only script บน TradingView
- **Editor:** TradingView Pine Editor (web-based) หรือ local editor
- **No external dependencies** — pure Pine Script

## Business Context (สำคัญมาก — ต้องเข้าใจก่อนเขียนโค้ด)

### Target User
- **Primary:** นักเทรดมือใหม่-กลาง สายทอง (XAUUSD) ในประเทศไทย
- **Device/Platform:** TradingView (Free หรือ Essential plan)
- **Language:** ไทย (UI label/comment สามารถใช้ไทยได้ใน string literals)

### Pricing Model
- **Free tier:** Signal ฟรีใน Line OpenChat (1-3 ครั้ง/วัน)
- **Monthly:** 990 บาท/เดือน
- **Yearly:** 8,900 บาท/ปี
- **Lifetime:** 19,900 บาท (Early Bird 100 คนแรก: 4,990 บาท)

### Marketing Tone
- **Tier A — Aggressive marketing** (Winrate 90%+)
- **Claim ต้องมีหลักฐาน** (backtest screenshot) แต่โทน marketing แรง
- ใช้ urgency + scarcity (early bird, limited slots)

### Distribution Funnel
```
Facebook/TikTok/YouTube → เว็บไซต์ → Line OA → Line OpenChat → Subscription
```

## File Structure

```
Crown Gold Signal/
├── PRD.md                          # Product requirements (อ่านเข้าใจก่อนเขียน)
├── CLAUDE.md                       # This file
├── CHECKLIST.md                    # Day-by-day tasks (ยังไม่สร้าง - สร้างใน session ถัดไป)
├── README.md                       # Project overview
├── src/
│   ├── CrownGoldSignal.pine        # Main indicator (single-file build)
│   ├── CrownGoldSignal_Strategy.pine  # Strategy version (for backtest)
│   └── lib/                        # Modular source (ใช้ตอนพัฒนา, merge ตอน publish)
│       ├── signal_engine.pine      # 3-condition signal logic
│       ├── smc.pine                # Order Block + FVG
│       ├── fibonacci.pine          # Auto fib retracement
│       ├── dashboard.pine          # Table UI
│       └── risk.pine               # SL/TP/Lot calculation
├── docs/
│   ├── user_manual.md              # คู่มือลูกค้า (ไทย)
│   ├── backtest_report.md          # ผล backtest (marketing)
│   └── setup_guide.md              # Alert/webhook setup
├── marketing/
│   ├── landing_page_copy.md
│   ├── facebook_ads.md
│   ├── line_oa_scripts.md
│   └── pricing_page.md
└── assets/
    ├── screenshots/
    └── demo_videos/
```

**⚠️ TradingView limitation:** ไม่รองรับ `import` ข้ามไฟล์ (ยกเว้น library) → ตอนเขียน dev ใช้ `lib/` แยกเพื่อ maintain ง่าย แต่ตอน publish ต้อง **merge เข้า single file** `CrownGoldSignal.pine`

## Architecture Rules

### General
- **Pine Script v6 เท่านั้น** — ใช้ `//@version=6` header ทุกไฟล์
- **Single responsibility per module** — แต่ละไฟล์ใน `lib/` ทำหน้าที่เดียว
- Main `CrownGoldSignal.pine` = publish-ready (merged all modules)
- **ใช้ const และ input ให้เยอะ** — ลูกค้าปรับแต่งได้ แต่มี default ที่ดี
- **ใส่ copyright/license comment ด้านบน** ทุกไฟล์ publish:
  ```pine
  // © 2026 Crown FX Automation — Crown Gold Signal
  // Licensed to subscribers only. Unauthorized distribution prohibited.
  ```

### Signal Logic
- **3-condition confirmation** — ลูกศรขึ้นเมื่อครบ 3/3 เท่านั้น:
  1. **Trend:** EMA 50 > EMA 200 (BUY) + HTF alignment
  2. **Momentum:** RSI 50-70 (BUY) + MACD line > signal
  3. **Structure:** แตะ Order Block หรือ FVG zone ล่าสุด
- ใช้ **closed bar เท่านั้น** (`barstate.isconfirmed`) เพื่อป้องกัน repainting
- **ห้าม repaint** — ถ้า signal เคย print แล้ว ต้องไม่หายไปหลัง bar ปิด
- Multi-TF ใช้ `request.security()` พร้อม `lookahead=barmerge.lookahead_off`

### TP/SL System
- **SL:** `ATR(14) × 1.5` OR swing low/high (pick safer one — farther from entry)
- **TP1:** 1× SL distance (R:R 1:1)
- **TP2:** 2× SL distance (R:R 1:2)
- **TP3:** 3× SL distance (R:R 1:3)
- **TP4:** 5× SL distance (R:R 1:5)
- Draw เป็น `line.new()` ขยายไปขวา + `label.new()` บอกราคา
- **Cleanup เส้นเก่าเมื่อ signal ใหม่เกิด** — ใช้ `line.delete()` / ใช้ array management

### Dashboard
- ใช้ `table.new(position.top_right, columns, rows)` — ไม่เกิน 15-20 rows
- Update เฉพาะตอน `barstate.islast` (ประหยัด performance)
- สีสวย: พื้นหลังเข้ม + text อ่อน, highlight BUY = เขียว / SELL = แดง
- แสดง: Signal, Entry, SL, TP1-TP4, Multi-TF trend, RSI, ATR, Lot suggest, Winrate

### Alert
- สร้าง `alertcondition()` แยกแต่ละ event:
  - New BUY signal
  - New SELL signal
  - Hit TP1 / TP2 / TP3 / TP4
  - Hit SL
- **ใช้ `alert()` สำหรับ webhook** (ส่งไป Line/Discord/Telegram)
- Alert message format: JSON-ready สำหรับ webhook parsing

### SMC Detection
- **Order Block (OB):** bullish/bearish candle ก่อน impulsive move
  - Bullish OB: last down candle ก่อน up move ที่ทำ new high
  - Bearish OB: last up candle ก่อน down move ที่ทำ new low
- **Fair Value Gap (FVG):**
  - Bullish FVG: candle[0].low > candle[2].high
  - Bearish FVG: candle[0].high < candle[2].low
- **BOS/CHoCH:** เทียบกับ swing high/low ล่าสุด
- วาดเป็น `box.new()` + label

### Performance
- **ประหยัด request.security() calls** — TradingView จำกัด 40 calls/script
- ใช้ `var` สำหรับ variable ที่ไม่ต้อง recompute ทุก bar
- Array cleanup — ลบ element เก่าเพื่อไม่ให้ memory ล้น
- Heavy calculation ให้ทำเฉพาะ `barstate.islast` หรือเมื่อ signal เกิด

### Anti-Repaint Rules (สำคัญมาก — ห้ามผิด)
1. **ใช้ `close[1]` แทน `close`** สำหรับ cross detection
2. **`request.security()` ต้อง `lookahead=barmerge.lookahead_off`**
3. **Signal ต้องเกิดบน closed bar** (`barstate.isconfirmed`)
4. **ห้ามใช้ `barstate.isrealtime` ตัดสินใจ signal**
5. Test ด้วย Bar Replay — signal ต้องตรงกับ backtest (ไม่หายไปหลัง bar ปิด)

## Coding Standards

### Naming
- **Functions:** camelCase → `calculateTPLevels()`, `detectOrderBlock()`
- **Variables:** camelCase → `entryPrice`, `slDistance`, `currentATR`
- **Inputs:** descriptive + group → `i_rsiLength`, `i_atrMultiplier`
- **Constants:** UPPER_CASE → `MAX_BARS_BACK`, `DEFAULT_RISK_PERCENT`

### Inputs (Group + Tooltip ทุกตัว)
```pine
// Example
i_emaTrend = input.int(200, "EMA Trend", minval=10, maxval=500,
     group="Trend Settings", tooltip="EMA period for trend identification")
```

**Group ที่ต้องมี:**
- "🎯 Signal Settings" — RSI, EMA, MACD periods
- "📊 Multi-Timeframe" — HTF selection
- "🛡️ Risk Management" — ATR multiplier, R:R ratios
- "🧠 SMC Settings" — OB/FVG toggles
- "📐 Fibonacci" — enable/disable, levels
- "📱 Dashboard" — show/hide, position
- "🎨 Visual" — colors, line styles

### Comments
- **English เป็นหลัก** สำหรับ code logic
- **ไทย OK** สำหรับ UI strings (input label, table text)
- อธิบาย **WHY** ไม่ใช่ WHAT
- ทุก function ใส่ doc comment ข้างบน:
  ```pine
  // @function Calculate TP levels based on SL distance and R:R ratios
  // @param entry float - Entry price
  // @param sl float - Stop loss price
  // @returns [float, float, float, float] - TP1, TP2, TP3, TP4
  calculateTPLevels(entry, sl) =>
      ...
  ```

### Error Handling
- **Validate inputs** — ใช้ `minval`/`maxval`
- **Null check** ก่อนใช้ array/value จาก `request.security()`
- **ถ้า calculation ไม่ได้** (เช่น ATR = na) → skip signal (อย่า print arrow)

## Visual Design Guidelines

### Colors (ต้อง professional + อ่านง่ายบนพื้นชาร์ตเข้ม/สว่าง)
- **Entry:** `color.new(color.blue, 0)` — น้ำเงินเข้ม
- **SL:** `color.new(color.red, 20)` — แดง
- **TP1:** `color.new(color.green, 50)` — เขียวอ่อน
- **TP2:** `color.new(color.green, 30)`
- **TP3:** `color.new(color.green, 10)` — เขียวเข้มขึ้น
- **TP4:** `color.new(color.lime, 0)` — เขียวสว่าง (runner)
- **Bull OB:** `color.new(#26a69a, 80)` — เขียว transparent
- **Bear OB:** `color.new(#ef5350, 80)` — แดง transparent
- **FVG:** `color.new(color.gray, 70)`
- **Arrow BUY:** `color.green` (triangleup)
- **Arrow SELL:** `color.red` (triangledown)

### Arrow
- ใช้ `plotshape()` ไม่ใช่ `plot()`
- Style: `shape.triangleup` / `shape.triangledown`
- Size: `size.normal` หรือ `size.large`
- Location: `location.belowbar` (BUY), `location.abovebar` (SELL)
- พร้อม text label: "BUY" / "SELL" ถ้ามีพื้นที่

### Dashboard Table
- Background: `color.new(#1e222d, 10)` (พื้นเข้ม)
- Header: `color.new(#f7b500, 0)` (ทอง — ตรงกับ brand Crown Gold)
- Text normal: `color.white`
- BUY row highlight: `color.new(color.green, 80)`
- SELL row highlight: `color.new(color.red, 80)`

## How to Test

### Compile Test
1. เปิด TradingView → Pine Editor
2. Paste code → กด "Save" (Ctrl+S)
3. ถ้า error → แก้ให้ clean
4. Add to chart → ตรวจสอบไม่มี error ที่ runtime

### Visual Test
1. เปิดชาร์ต XAUUSD M15 → Apply indicator
2. ตรวจสอบ:
   - [ ] ลูกศรขึ้นถูกตำแหน่ง
   - [ ] TP/SL เส้นแสดงถูก
   - [ ] Dashboard แสดงข้อมูลครบ
   - [ ] Alert trigger ได้
3. ทดสอบกับ symbols อื่น: EURUSD, GBPUSD, USDJPY

### Backtest
1. เปลี่ยนเป็น **Strategy version** (`CrownGoldSignal_Strategy.pine`)
2. Add to chart → Strategy Tester tab
3. **Setting มาตรฐาน:**
   - Symbol: XAUUSD
   - Timeframe: H1 (primary)
   - Period: 2024-01-01 ถึง 2026-04-15
   - Initial capital: $10,000
   - Commission: 0.02% หรือ $0.50/lot
   - Pyramiding: 0
4. **ดูผล:**
   - Net Profit ≥ +50%
   - Winrate ≥ 85%
   - Profit Factor ≥ 1.8
   - Max DD ≤ 15%
5. Screenshot ผลเก็บไว้ทำ marketing

### Anti-Repaint Test (สำคัญ!)
1. ดู signal บน chart ปัจจุบัน
2. ใช้ **Bar Replay** เลื่อนกลับไป bar นั้น
3. เล่น forward → signal ต้องเกิดที่ bar **เดียวกัน** และ **ไม่หายไป**
4. ถ้า signal หาย = **มี repaint bug → ต้องแก้**

## Development Priority

### Must Have (Day 1-3)
1. `CrownGoldSignal.pine` — main structure + input panel
2. `signal_engine.pine` — 3-condition logic
3. `risk.pine` — SL/TP calculation (4 levels)
4. Draw TP/SL lines + labels บน chart
5. Arrow BUY/SELL
6. Alert conditions (basic)

### Should Have (Day 4-5)
7. `dashboard.pine` — Info table
8. `smc.pine` — Order Block + FVG detection + visualization
9. Multi-TF trend indicator
10. `CrownGoldSignal_Strategy.pine` — strategy version

### Nice to Have (Day 6-7)
11. `fibonacci.pine` — Auto fib
12. Advanced alert (webhook-ready JSON)
13. Backtest optimization + screenshot

### Post-Launch (V1.1+)
- Line API webhook integration
- Multi-symbol scanner
- Trade journal
- Telegram bot

## Common Pitfalls

### Pine Script Gotchas
- **`series float` vs `simple float`** — บาง function รับแค่ `simple` type → ต้องใช้ `simple int/float`
- **`request.security()` lookahead** — ต้องใส่ `barmerge.lookahead_off` เสมอ (ไม่งั้น repaint)
- **Array limit:** TradingView จำกัด 100,000 elements → จัดการ cleanup
- **`var` variables:** initialize ครั้งเดียว — ใช้สำหรับ state ที่ persist
- **`plot()` ต้อง return type เดียวกัน** — ถ้าใช้ `na` ต้อง consistent
- **Color transparency:** `color.new(color.red, 50)` — 0 = เต็ม, 100 = โปร่งใส (สลับจาก common sense!)

### TradingView Limits (Free plan ลูกค้า)
- ~5,000 historical bars เท่านั้น
- 1 alert/chart
- 1 chart/tab
- → แนะนำลูกค้าอัปเกรด Essential ($14.95/mo) ในหน้าขาย

### Publishing to TradingView
1. Pine Editor → "Publish Script"
2. เลือก "Invite-only" (ต้องมี Premium plan ของ admin เอง = $59.95/mo)
3. ใส่ description + screenshots + tags
4. รอ review (1-3 วัน)
5. หลัง approve → manage invites ผ่าน "Manage Access"

## Workflow

### เมื่อเริ่ม session
1. อ่าน [PRD.md](PRD.md) section ที่เกี่ยวข้อง
2. อ่าน `CHECKLIST.md` (ถ้ามี) → หา task ต่อไป
3. **Invoke skill ที่เกี่ยวข้อง** ก่อนเขียนโค้ด:
   - **⚠️ Pine Script: MUST invoke `pine-script-v6-expert` skill ก่อนเขียน/แก้/review ไฟล์ `.pine` ทุกครั้ง — ห้ามข้าม** (ครอบคลุม anti-repaint, SMC detection, multi-TF, alert/webhook, publish workflow)
   - สำหรับ backtest: `backtesting-frameworks`, `quant-analyst`, `risk-metrics-calculation`
   - สำหรับ review code: `code-review-excellence`, `simplify`, `find-bugs`
   - สำหรับ marketing: `copywriting`, `landing-page-generator`, `marketing-psychology`, `ad-creative`
   - สำหรับ pricing: `pricing-strategy`
   - สำหรับ launch: `launch-strategy`, `micro-saas-launcher`
4. ทำงาน → test compile → visual test
5. Update CHECKLIST.md status

### เมื่อจะ publish `.pine` script (MANDATORY gate)
1. **Spawn `pine-script-reviewer` agent** ให้ review file ก่อน — `Agent(subagent_type="pine-script-reviewer", prompt="Review src/CrownGoldSignal.pine for publish-readiness")`
2. ถ้า verdict = `BLOCK PUBLISH` → แก้ตาม Critical Issues → rerun review
3. ถ้า verdict = `APPROVE` หรือ `APPROVE WITH CHANGES` → publish ได้
4. **ห้าม publish โดยไม่ผ่าน agent review** เพราะขายให้ลูกค้าเสียเงิน — false signal ทำลาย trust

### เมื่อต้อง research คู่แข่ง/docs
- ใช้ `Agent(subagent_type="Explore", ...)` แทนการ search เอง (ประหยัด context)

### เมื่อติด stuck
- Invoke `brainstorming` หรือ `multi-agent-brainstorming`
- ดู reference indicator บน TradingView public library
- ปรึกษา Pine Script docs: https://www.tradingview.com/pine-script-docs/

## Quick Start for Claude Code

เมื่อเริ่มทำงาน:
1. **อ่าน PRD.md ทั้งหมด** — เข้าใจ spec + business context
2. **ตรวจสอบ CHECKLIST.md** (ถ้ามี) — หา task ปัจจุบัน
3. **เริ่มจาก structure skeleton:**
   - สร้าง `src/CrownGoldSignal.pine` — version header + input panel + main OnBar logic
4. **Build incrementally:**
   - Signal logic → compile test → Visual test
   - Add TP/SL → compile test
   - Add dashboard → compile test
   - Add SMC → compile test
   - Add Fibonacci → compile test
5. **Merge to single file** ก่อน publish (Pine Script ไม่รองรับ cross-file import)

## Reference Documents
- [PRD.md](PRD.md) — Full product requirements
- TradingView Pine Script v6 Docs: https://www.tradingview.com/pine-script-docs/
- Pine Script Reference Manual: https://www.tradingview.com/pine-script-reference/v6/
- SMC Concepts: https://www.luxalgo.com/library/indicator/smart-money-concepts-smc/

## Important Notes

### Brand Consistency
- ใช้ชื่อ **"Crown Gold Signal"** ทุกที่ (ไม่ย่อ/ไม่เปลี่ยน) จนกว่าจะ finalize ชื่อใหม่
- สีหลักของ brand: **ทอง (#f7b500)** + ดำ (#1e222d)
- Logo/Icon: ใช้ Crown emoji 👑 หรือออกแบบ logo จริงภายหลัง

### Legal/Compliance
- **ต้องมี Disclaimer** ในทุก marketing material:
  - "Past performance is not indicative of future results"
  - "Trading involves risk of loss"
  - "This indicator is for educational purposes"
- **ToS ชัดเจน:**
  - ห้าม share script/invite
  - ห้าม redistribute
  - Refund policy (7 วัน, เงื่อนไข)

### Customer Service
- ใช้ Line OA เป็นช่องทางหลัก
- Response time target: ภายใน 4 ชั่วโมงในเวลาทำการ
- Script สำหรับตอบคำถามบ่อย → เก็บใน `marketing/line_oa_scripts.md`

---

**Last Updated:** 2026-04-15
**Next Action:** สร้าง CHECKLIST.md + เริ่มเขียน Pine Script MVP
