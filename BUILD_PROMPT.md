# BEE REMOVAL BUSINESS APP — BUILD PROMPT v2
*For Jaco. Gauteng, South Africa. Updated 28 September 2026.*

---

## WHAT THIS IS

A simple mobile-first web app to run a bee removal and relocation business. Not a fancy product — a tool that tracks jobs, quotes, income, and hive sponsorships. One screen per job. Built for a phone in a field.

---

## TECH STACK

- **Frontend:** React (Vite) — single-page app, works offline-first where possible
- **Backend:** Supabase (free tier) — Postgres database + auth + storage
- **Hosting:** Vercel or Netlify (free tier)
- **Maps:** Google Maps embed or OpenStreetMap for job locations
- **Language:** English UI, all money in **ZAR (R)**

---

## PRICING MODEL (Gauteng market rates, Sept 2026)

No separate call-out fee. Travel is charged per km on top of a base job fee.

### Base job fee by difficulty tier

| Tier | Description | Base fee |
|------|-------------|----------|
| Standard access | Low-hanging trees, bushes, exterior structures, pool pump boxes, water meter boxes, tyres | R1,000 |
| Moderate difficulty | Higher trees requiring a ladder, under roof eaves, small wall cavities, air bricks, single-storey roofs | R1,500 |
| High difficulty | Cherry picker or scaffolding needed, double-storey roofs, ceiling spaces, deep wall cavities | R2,200 |

### Travel

- **R4.95 per km** from base (Kempton Park) to job site — applies to every job, every tier
- Quote total = base fee + (km × R4.95)
- Final amount can be adjusted on site if the job turns out harder or easier than quoted

### Optional extras

- Trap-out surcharge: R___ (multi-day jobs — set by Jaco)
- Hive box fee: R___ (charged only if client doesn't supply their own Langstroth box)
- Emergency / same-day uplift: +20–30% (optional, set by Jaco)

### Market context (why these numbers)

- Gauteng operators: standard access from R950–R1,500, walls/roofs from R1,500–R2,500, high structures R2,200–R4,000+
- One flat-rate operator charges R1,000 per hive anywhere in Gauteng with no travel charge
- Jaco's model is cleaner: local jobs aren't subsidizing far ones, and the per-km rate is transparent

---

## SCREENS / FEATURES

### 1. DASHBOARD (home screen)
- Today's jobs (list with time, location, status)
- This month's stats: jobs completed, income earned, km driven
- Pending quotes (not yet accepted)
- Quick action buttons: + New Job, + New Quote

### 2. JOBS LIST
- Filter by status: Quoted / Scheduled / In Progress / Completed / Cancelled
- Each row: client name, location, date, status badge, amount
- Tap to open job detail

### 3. JOB DETAIL
- Client name + phone (tap to call)
- Location (address + map pin)
- Job type: wall colony / drain pipe / trap-out / swarm
- Difficulty tier dropdown (standard / moderate / high) → auto-fills base fee
- Status dropdown
- Notes field (free text — what you found, what you did)
- Photos (upload from phone camera — before/after)
- Quote amount + final amount charged
- Travel: km driven + R4.95/km auto-calculated
- Mark complete → adds to monthly income

### 4. QUOTES
- Create quote: client, location, job type, difficulty tier, estimated km
- Auto-calculate: base fee (from tier) + (km × R4.95) = quote total
- Send via WhatsApp link or copy text
- Track: sent / accepted / declined / expired
- Accepted quote → converts to a scheduled job

### 5. RATES (settings, editable)
- Base fees per tier: R1,000 / R1,500 / R2,200 (editable)
- Travel rate: R4.95 per km (locked default, editable)
- Trap-out surcharge: R___ (optional)
- Hive box fee: R___ (optional)
- Emergency uplift %: ___ (optional)

### 6. SPONSOR A HIVE
- Public-facing page (shareable link)
- Shows: what sponsorship means, cost per hive, what the sponsor gets (name on hive, photos of the colony, updates)
- Sponsor form: name, contact, amount, message
- Track sponsors: active / completed
- Link from LinkedIn bio and WhatsApp status

### 7. MONTHLY REPORT
- Jobs this month vs target (5–7 removals)
- Total income
- Total km driven
- Average per job
- Export as PDF or share via WhatsApp

---

## DATA MODEL (Supabase tables)

**jobs**
- id, client_name, client_phone, location_address, location_lat, location_lng
- job_type (wall / drain_pipe / trap_out / swarm)
- difficulty_tier (standard / moderate / high)
- status (quoted / scheduled / in_progress / completed / cancelled)
- base_fee, km_driven, travel_amount, quote_amount, final_amount
- notes, photos (array of URLs), created_at, completed_at

**quotes**
- id, client_name, client_phone, location, job_type, difficulty_tier
- km_estimate, base_fee, travel_amount, total, status (sent / accepted / declined)
- created_at, responded_at

**rates**
- id, base_fee_standard (1000), base_fee_moderate (1500), base_fee_high (2200)
- travel_rate_per_km (4.95), trap_out_surcharge, hive_box_fee, emergency_uplift_pct

**sponsors**
- id, name, contact, amount, message, status (active / completed), created_at

---

## CURRENT JOBS TO ENTER (seed data)

1. **Pastor Colin — Bayslea** — bees in the wall. Tier: moderate (wall cavity). Status: scheduled.
2. **Allen Grove** — quote needed. Status: quoted. (Tier TBD after site visit.)
3. **Drain pipe in a field** — rescue and relocate. Status: to schedule. (Tier TBD — likely standard access if pipe is at ground level.)

---

## BUILD ORDER

1. Supabase project + tables + auth (Jaco logs in with email)
2. Dashboard + Jobs list + Job detail (the core loop)
3. Quotes with auto-calc (base fee from tier + km × R4.95)
4. Rates settings (editable tiers)
5. Sponsor a Hive page
6. Monthly report + export
7. PWA manifest so it installs on his phone like an app

---

## DESIGN NOTES

- Big buttons, fat text — used with gloves on, in the sun
- Dark mode friendly
- Everything one tap from the dashboard
- No login friction: remember me, biometric if available
- WhatsApp is the primary communication channel — every share action should offer "Send via WhatsApp"

---

*Build it. Then we fill it with the three jobs above.*