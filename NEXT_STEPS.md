# 📋 Next Steps — ลำดับละเอียดตั้งแต่วันนี้ถึง Launch

**Last Updated:** 2026-04-16
**Status:** Code v1.0 เขียนเสร็จ + push GitHub + compile pass แล้ว
**Next Milestone:** Visual Test + Backtest

---

## 🎯 Phase 1: Code Validation (ทำทันที — 1-3 วัน)

### Step 1.1: Compile Test (ฟรี, ใช้ Free plan) ⏱️ 30 นาที

```
1. ไปที่ https://tradingview.com → login/register (ฟรี)
2. เปิดกราฟ XAUUSD → กด "Pine Editor" ด้านล่าง
3. เปิด src/CrownGoldSignal.pine ใน VS Code → Copy ทั้งหมด
4. Paste ใน Pine Editor → กด Ctrl+S (Save)
5. ตั้งชื่อ: "Crown Gold Signal v1.0"
```

**ผลที่คาดหวัง:** compile ผ่านหรือมี error list

**ถ้ามี error:**
- Copy error message ทั้งหมด
- ส่งให้ Claude → แก้ แล้ว commit push

---

### Step 1.2: Visual Test ⏱️ 1-2 ชั่วโมง

ไล่ตรวจ checklist:

- [ ] Arrow BUY/SELL ปรากฏถูกตำแหน่ง
- [ ] TP/SL lines วาดถูก + มี label บอกราคา
- [ ] Dashboard มุมขวาบนแสดงครบ 17 rows
- [ ] OB/FVG boxes แสดงถูกสี
- [ ] Fibonacci + Golden Zone วาดอัตโนมัติ
- [ ] ทดสอบ symbol อื่น: EURUSD, GBPUSD (ถ้าทำงานได้แสดงว่า generic)
- [ ] ทดสอบ timeframe M15, H1, H4

**ถ้ามีปัญหา visual:** screenshot + บอก Claude

---

### Step 1.3: Anti-Repaint Test ⏱️ 30 นาที (CRITICAL!)

```
1. เปิดกราฟ XAUUSD H1
2. หา signal ที่เกิดขึ้นเมื่อ 50-100 bars ที่แล้ว → screenshot ตำแหน่ง
3. กด "Bar Replay" (ไอคอนนาฬิกาด้านบน)
4. เลื่อนกลับไปก่อน signal นั้น → กด Play
5. สังเกต: signal ต้องเกิดที่ bar **เดียวกัน** ตำแหน่งเดียวกัน
```

**ถ้า signal หาย/เกิดที่ bar อื่น = มี repaint bug** → บอก Claude ทันที

---

### Step 1.4: Backtest Strategy Version ⏱️ 2-3 ชั่วโมง

```
1. เปิด Pine Editor → Paste src/CrownGoldSignal_Strategy.pine
2. Save → Add to chart
3. คลิกแท็บ "Strategy Tester" ด้านล่าง
4. ตั้งค่า:
   - Chart: XAUUSD H1
   - Period: 2024-01-01 ถึงปัจจุบัน
5. ดูผล tab "Overview" + "Performance Summary"
```

**Target:**

| Metric | Target |
|--------|--------|
| Net Profit | ≥ +50% |
| Winrate | ≥ 85% |
| Profit Factor | ≥ 1.8 |
| Max Drawdown | ≤ 15% |

**ถ้าไม่ถึง target:** บอก Claude ว่าได้เท่าไหร่ → ช่วย tune parameters

---

### Step 1.5: Screenshot ผลเก็บไว้ ⏱️ 30 นาที

เก็บไว้ใน `assets/screenshots/` สำหรับ marketing:

- Strategy Tester overview (winrate, PF, DD)
- Equity curve graph
- Signal ที่ดี 5-10 ตัวอย่าง (ทำกำไรถึง TP2-TP4)
- Dashboard screenshot

---

## 📢 Phase 2: Marketing Prep (ขนานไปกับ Phase 1 — 3-7 วัน)

### Step 2.1: Brand Assets ⏱️ 1 วัน

- [ ] Logo Crown Gold Signal (ใช้ Canva/Figma ออกแบบ หรือใช้ emoji 👑 ไปก่อน)
- [ ] Color palette: ทอง **#f7b500** + ดำ **#1e222d**
- [ ] Facebook Page cover (1640×924 px)
- [ ] Profile picture 500×500

---

### Step 2.2: Line OA + OpenChat ⏱️ 1 วัน

- [ ] สมัคร Line Official Account (ฟรี): https://www.linebiz.com/th/
- [ ] ตั้งชื่อ: "Crown FX Automation" หรือ "Crown Gold Signal"
- [ ] ตั้ง Auto-reply: greeting + FAQ
- [ ] สร้าง Rich Menu (ปุ่ม: ดูราคา / สมัคร / ติดต่อ)
- [ ] สร้าง Line OpenChat "Crown Gold Free Signal" → ตั้งกฎกลุ่ม

---

### Step 2.3: Landing Page ⏱️ 2-3 วัน

**ตัวเลือก platform:**

| Platform | ราคา | เหมาะกับ |
|----------|------|---------|
| **Carrd.co** | $19/ปี | ง่ายสุด 1 page |
| **Framer** | ฟรี plan | สวย drag-drop |
| **WordPress + Elementor** | ~$5/mo | ยืดหยุ่น |
| **Webflow** | $14/mo | Pro |

**Sections ที่ต้องมี:**

1. **Hero** — "Winrate 90%+ Indicator สายทอง บน TradingView"
2. **Demo video** หรือ screenshot chart
3. **Features** (3-condition, SMC, TP/SL 4 ระดับ)
4. **Backtest results** (screenshot จาก Phase 1.5)
5. **Pricing** (599/2,590/6,900 + Early Bird 2,490)
6. **Testimonial** (ช่วงแรกใช้ของ beta tester)
7. **FAQ**
8. **CTA** → Line OA

**ให้ Claude เขียน copy:** บอก → invoke `copywriting` + `landing-page-generator` skills

---

### Step 2.4: Demo Video ⏱️ 1 วัน

- ใช้ **OBS Studio** (ฟรี) หรือ **Loom** บันทึกหน้าจอ
- 30-60 วินาที — แสดง:
  1. Signal เกิด → TP1 hit → TP2 hit
  2. Dashboard + ข้อมูลครบ
  3. Alert ทำงาน
- Export 1080p → upload YouTube (unlisted) + embed landing page

---

## 🧪 Phase 3: Beta Test (5-7 วัน)

### Step 3.1: Recruit Beta Testers ⏱️ 2-3 วัน

- โพสต์ในกลุ่ม Facebook เทรดทองไทย: "รับสมัคร Beta Tester 10 คน ฟรี 30 วัน"
- Line OpenChat ที่มีอยู่แล้ว
- เลือก 5-10 คนที่จริงจัง (ไม่ใช่แค่ขอฟรี)

---

### Step 3.2: Run Beta Test ⏱️ 7-14 วัน

- ส่ง invite TradingView ให้ beta testers
  - ตอนนี้ยังใช้ Free plan → ลูกค้า copy paste code ได้ชั่วคราว
  - หรืออัปเกรด Premium $59.95 แล้ว invite จริง
- สร้างกลุ่ม Line แยกสำหรับ beta
- ขอ feedback ทุก 3-4 วัน
- แก้ bug ที่เจอ → commit push

---

## 💼 Phase 4: Business Setup (2-3 วัน)

### Step 4.1: Legal/Terms ⏱️ 1 วัน

- [ ] **Terms of Service** (ห้าม share script, refund policy 7 วัน)
- [ ] **Privacy Policy**
- [ ] **Disclaimer** (trading risk)

**ให้ Claude เขียน:** บอกไป → เขียน draft ให้

---

### Step 4.2: Payment Flow ⏱️ 1 วัน

- [ ] เปิด **PromptPay หมายเลขธุรกิจ**
- [ ] เตรียม **QR Code** + เลขบัญชี
- [ ] **Script ตอบลูกค้า Line OA** (20 scenarios — Claude ช่วยเขียน)
- [ ] **Excel/Google Sheet** tracking ลูกค้า + วันหมดอายุ

---

### Step 4.3: TradingView Premium ⏱️ 10 นาที

- อัปเกรด **ตอนใกล้ launch เท่านั้น** (ประหยัด $60)
- คลิก Profile → Upgrade → Premium ($59.95/mo)
- ไป Pine Editor → Open script → "Publish Script" → **Invite-only**
- รอ review 1-3 วัน

---

## 🚀 Phase 5: Launch (1 วัน)

### Step 5.1: Pre-Launch Teaser (7 วันก่อน)

- [ ] Countdown post Facebook + TikTok รายวัน
- [ ] Waitlist form เก็บ email
- [ ] Early Bird counter "เหลือ 100 slot"

---

### Step 5.2: Launch Day

- [ ] เปิดขายเวลาที่กำหนด (แนะนำ **8 โมงเช้า**)
- [ ] Post ทุก channel พร้อมกัน
- [ ] Live demo ใน Line OpenChat
- [ ] Standby ตอบ Line OA **8 ชั่วโมง**

---

## 📅 Timeline แนะนำ

| Week | Focus |
|------|-------|
| **Week 1** (now) | Phase 1 (code validation + backtest) |
| **Week 2** | Phase 2 (marketing prep) + Phase 3 start (beta recruit) |
| **Week 3** | Phase 3 run (beta testing) + Phase 4 (business setup) |
| **Week 4** | Pre-launch teaser + Phase 5 (launch) |

**Total: ~30 วัน**

---

## 🎯 Next Action ตอนนี้เลย

**ลำดับ 1: เปิด TradingView แล้ว paste code test compile** (30 นาที)

ถ้า error ส่งให้ Claude ทันที — แก้ให้ภายใน session ✅

---

## 🛠️ Deliverables ที่ Claude ทำได้ขนานได้ (ขอได้เลย)

| Deliverable | Skill ที่ใช้ |
|-------------|-------------|
| 📝 Landing page copy | `copywriting` + `landing-page-generator` |
| 💬 Line OA reply scripts (20 scenarios) | `customer-support` |
| 📹 Demo video script | `copywriting` |
| 🎨 Facebook ad copy 3 variations | `ad-creative` + `copywriting` |
| ⚖️ Terms of Service + Refund Policy | (draft ทั่วไป) |
| 📄 Backtest report markdown | `data-storytelling` |
| 🎯 TikTok scripts 5 คลิป | `viral-generator-builder` |

---

## 📚 References

- [PRD.md](PRD.md) — Full product requirements
- [CLAUDE.md](CLAUDE.md) — Dev instructions + mandatory skill/agent usage
- [CHECKLIST.md](CHECKLIST.md) — 41 tasks breakdown
- [README.md](README.md) — Project overview
- GitHub: https://github.com/thanakitpw/Crown-Gold-Signal

---

**Made with 👑 by Crown FX Automation — Bangkok, Thailand**
