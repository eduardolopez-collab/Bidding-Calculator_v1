# FSR Bidding Calculator v3
**FlixBus / Greyhound — Facilities & Security Department**

A standalone internal tool for Facilities agents to benchmark vendor bids against market labor and material rates, generate structured cost breakdowns, and produce print-ready FSR (Facility Service Request) documents — no server, no login, no dependencies.

---

## What It Does

Agents fill out a service request, select services from a library of 225+ scopes across categories like Electrical, Plumbing, HVAC, Roofing, Pavement, and more. The tool then:

- Pulls **labor rate cards** per trade (Handyman, Electrician, Welder, Plumber, etc.) and adjusts for the selected city's cost-of-living multiplier
- Calculates a **static Benchmark** (market rate × city multiplier × quantity) to compare against
- Builds a live **Proposal** with adjustable worker counts, hours, and materials
- Shows an **Adjusted Benchmark** that reflects real proposal inputs
- Computes a **three-way cost split** (Labor / Materials / Travel) with color-coded thresholds
- Surfaces **Bid Intelligence** — a primary cost driver diagnosis and conditional action flags (amber/red when thresholds are exceeded)
- Accepts **vendor bids**, ranks them, and flags over-benchmark submissions
- Logs all FSRs to a searchable **FSR Log** with CSV export
- Generates a **print-ready invoice** (Print / Save as PDF) formatted to FlixBus brand standards

---

## Project Structure

```
Bidding Calulator_v1/
├── frontend/
│   └── FSR_Calculator_v3.html   # The entire app — single self-contained file
├── backend/
│   ├── functions/
│   │   └── excelSync.js         # Azure Function: nightly SharePoint → SQL sync
│   ├── routes/                  # Express API routes (cities, services, FSR, reports)
│   ├── schema.sql               # Azure SQL table definitions
│   ├── server.js                # Express entry point
│   └── package.json
├── docs/
│   ├── FSR_12Month_Product_Roadmap.docx
│   └── FSR_Azure_Implementation_Brief_PostBeta.docx
├── brand identity/
│   └── 00_Flix_Brand-Identity_2024_08.pdf
└── dazzed-font-family/          # Dazzed TRIAL typeface (licensed)
```

---

## Running the App

The frontend is a **zero-dependency single HTML file**. Open it directly in any modern browser:

```
frontend/FSR_Calculator_v3.html
```

No build step. No npm install. No server required.

> The Dazzed font files in `dazzed-font-family/` must stay in the same relative location for the UI typography to render correctly.

---

## Key Features

| Feature | Details |
|---|---|
| **225+ Services** | Grouped by category — Electrical, Plumbing, HVAC, Lighting, Roofing, Pavement, Flooring, Access Points, Fire Systems, Landscaping, and more |
| **55 Cities** | Pre-loaded with labor and material cost multipliers per city/tier |
| **Labor Rate Card** | 15 trades with Low / Med / High hourly rates |
| **190 Materials** | Unit-priced materials library; auto-populates per service, fully editable |
| **City Multipliers** | Separate labor and material multipliers applied across all calculations |
| **Proposal Builder** | Per-trade worker count + hours spinners; vendor material cost override |
| **Benchmark vs Adjusted** | Static benchmark (market default) vs live adjusted benchmark (proposal inputs) |
| **Cost Breakdown** | Labor / Materials / Travel split with amber/red alerts at defined thresholds |
| **Bid Intelligence** | Driver diagnosis + 14 conditional action flags with severity coloring |
| **Vendor Bids** | Multi-bid entry, lowest bid highlighted green when under benchmark |
| **Approval Engine** | Auto-approval, senior agent, senior manager, and escalation tiers |
| **FSR Log** | Persistent session log with search, filter, and CSV export |
| **Print / PDF** | Brand-formatted invoice with service breakdown, pricing summary, and authorization block |
| **Dark / Light Mode** | Full theme toggle |

---

## Backend (Future / In Progress)

The `backend/` folder contains the skeleton for a planned Azure-hosted API:

- **`excelSync.js`** — Azure Timer Function that reads the FSR Pricing Tool Excel workbook from SharePoint via Microsoft Graph and upserts cities + services into Azure SQL nightly
- **`routes/`** — REST endpoints for cities, services, FSR log entries, and reports
- **`schema.sql`** — Tables: `cities`, `services`, `fsr_log`

This is not yet connected to the frontend. The current app runs entirely off embedded static data arrays.

---

## Tech Stack

| Layer | Stack |
|---|---|
| Frontend | Vanilla HTML / CSS / JS — no framework |
| Fonts | Dazzed TRIAL (headlines) · Roboto (body) |
| Backend (planned) | Node.js · Express · Azure Functions · Azure SQL · Microsoft Graph |
| Export | Browser `window.print()` → PDF |

---

## Intended Users

Internal Facilities & Security agents at FlixBus / Greyhound North America. Not a public-facing tool.

---

## License

Internal use only — FlixBus / Greyhound Facilities & Security.  
Dazzed font is used under a trial license. See `dazzed-font-family/Befonts-License.txt`.
