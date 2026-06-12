FrostGuard AI 🧊


AI-powered cold chain intelligence for the last mile.



FrostGuard protects temperature-sensitive products — vaccines, insulin, blood samples, dairy — using low-cost indicator stickers and AI-powered image analysis. No expensive IoT hardware. No connectivity required at the point of scanning.

"A ₹100 medicine should not require ₹10,000 hardware to remain safe."


Live Demo

Open index.html in any browser — no build step, no server required.

For real AI analysis, add a free Gemini API key from aistudio.google.com in the top bar.


The Problem

Traditional cold chain monitoring costs ₹5,000–₹12,000 per shipment in IoT sensors. Rural clinics, PHCs, and NGOs cannot afford this. Spoiled medicines reach patients undetected.

Traditional Cold Chain
─────────────────────────────────────────────────────────
 Manufacturer ──► IoT Sensor (₹10,000) ──► Cloud ──► Alert
                       │
                  Needs power
                  Needs WiFi
                  Gets lost/stolen
                  Needs maintenance
─────────────────────────────────────────────────────────
❌ Unaffordable for rural PHCs, NGOs, small distributors

Our Solution

FrostGuard Cold Chain
─────────────────────────────────────────────────────────
 Manufacturer ──► Indicator Sticker (₹2–5) ──► QR Label
                                                    │
                                              Receiver scans
                                                    │
                                           Photos indicator
                                                    │
                                        Gemini AI classifies
                                                    │
                                       Health Score + Action
─────────────────────────────────────────────────────────
✅ Works on any Android · No power · No WiFi · ₹2–5 total

LayerWhatCostPhysicalIrreversible temperature indicator sticker₹2–5IdentityQR code with structured shipment UID₹0.50IntelligenceGemini AI color analysis + health score~₹0.02/scan

Instead of making the box smart, we make the interpretation smart.


Features


📊 Dashboard — Live stats, risk heatmap, activity feed, 7-day chart
📦 Shipments — Full list, search/filter, detailed scan history
➕ Register — Create shipment, auto-generate structured UID + QR code
📷 Scan — Lookup any shipment by UID, view health score & recommendation
🔬 AI Analysis — Upload indicator photo or simulate color → Gemini returns risk profile
🤖 AI Copilot — Chat assistant powered by Gemini for cold chain Q&A
⚙️ Admin — Export CSV, manage data, system stats
📴 Zero dependencies — Pure HTML/CSS/JS, works offline



System Architecture

┌─────────────────────────────────────────────────────────────┐
│                        FROSTGUARD AI                        │
├───────────────┬──────────────────┬──────────────────────────┤
│  PHYSICAL     │   IDENTITY       │   INTELLIGENCE           │
│  LAYER        │   LAYER          │   LAYER                  │
│               │                  │                          │
│  ┌─────────┐  │  ┌────────────┐  │  ┌────────────────────┐ │
│  │Indicator│  │  │  QR Code   │  │  │   Gemini Vision    │ │
│  │ Sticker │  │  │            │  │  │   API              │ │
│  │  ₹2–5   │  │  │ FG-VAC-    │  │  │                    │ │
│  │         │  │  │ CHN-2026-  │  │  │ Color → Score      │ │
│  │⬜→🟦→🟪 │  │  │ X9A7K      │  │  │ 0–100 Health       │ │
│  └─────────┘  │  └────────────┘  │  │ Risk Level         │ │
│               │                  │  │ Recommendation     │ │
│  Irreversible │  Encodes product │  └────────────────────┘ │
│  color change │  city, date, ID  │                          │
└───────────────┴──────────────────┴──────────────────────────┘


Data Flow

┌──────────┐     ┌──────────────┐     ┌─────────────────┐
│Dispatcher│     │   FrostGuard │     │    Receiver     │
└────┬─────┘     │   Platform   │     └────────┬────────┘
     │           └──────┬───────┘              │
     │ Create           │                      │
     │ shipment ───────►│                      │
     │                  │ Generate UID + QR    │
     │                  │◄─────────────────    │
     │ Print & attach   │                      │
     │ QR to box        │                      │
     │                  │                      │
     │    [Shipment travels with indicator]    │
     │                  │                      │
     │                  │        Scan QR ──────►
     │                  │◄── Load shipment ────│
     │                  │                      │ Photo
     │                  │                      │ indicator
     │                  │◄── Upload image ─────│
     │                  │                      │
     │                  │ Gemini AI             │
     │                  │ ┌──────────────────┐ │
     │                  │ │ Classify color   │ │
     │                  │ │ Score: 0–100     │ │
     │                  │ │ Risk: Safe/Warn  │ │
     │                  │ └──────────────────┘ │
     │                  │ Health score ────────►
     │                  │ + Recommendation     │
     │                  │                      │
     │◄── Dashboard ────│                      │
│ aggregates all        │                      │
│ shipments             │                      │
└──────────────────────────────────────────────┘


Indicator Color Guide

Temperature Indicator States
────────────────────────────────────────────────────
  ⬜ WHITE          No color migration
                   Temp maintained throughout
                   Health Score: 90–100
                   → SAFE — proceed with delivery

  🔵 LIGHT BLUE    Minor color migration
                   Brief mild temperature exposure
                   Health Score: 65–89
                   → MONITOR — verify before use

  🟦 MEDIUM BLUE   Significant color change
                   Threshold exceeded
                   Health Score: 40–64
                   → WARNING — quarantine & verify

  🟪 DARK BLUE     Complete activation
                   Major temperature breach
                   Health Score: 0–39
                   → COMPROMISED — do not use
────────────────────────────────────────────────────


Shipment UID Format

FG  -  VAC  -  CHN  -  20260612  -  X9A7K
│      │       │        │             │
│      │       │        │             └── Random 5-char suffix
│      │       │        └──────────────── Date (YYYYMMDD)
│      │       └───────────────────────── Origin city code
│      └───────────────────────────────── Product type
└──────────────────────────────────────── FrostGuard prefix

Product codes:  VAC=Vaccine  INS=Insulin  BLD=Blood
                DRY=Dairy    SFD=Seafood  MED=Medicine

City codes:     CHN=Chennai  BLR=Bengaluru  MUM=Mumbai
                HYD=Hyderabad  AMD=Ahmedabad  COK=Kochi

Metadata is encoded in the UID itself — no database lookup needed to read product, city, or date.


Tech Stack

┌─────────────────────────────────────────────┐
│              FRONTEND                       │
│  HTML5 · CSS3 · Vanilla JavaScript ES2022   │
│  Zero build tools · Zero npm packages       │
└───────────────────┬─────────────────────────┘
                    │
┌───────────────────▼─────────────────────────┐
│              AI LAYER                       │
│  Google Gemini 1.5 Flash                    │
│  ├── Vision API  (indicator analysis)       │
│  └── Chat API    (copilot assistant)        │
└───────────────────┬─────────────────────────┘
                    │
┌───────────────────▼─────────────────────────┐
│              DATA LAYER                     │
│  MVP:      LocalStorage (offline-first)     │
│  Roadmap:  Supabase (Postgres + Auth)       │
│  Future:   SQLite (PWA offline sync)        │
└─────────────────────────────────────────────┘

Roadmap upgrades:


Supabase for cloud sync + auth
PWA manifest + service worker for true offline
TensorFlow.js for on-device color inference (no API call)
WhatsApp alerts via Twilio on Compromised status



Cost Comparison

Per-shipment monitoring cost
────────────────────────────────────────────
  IoT Sensor approach
  ┌────────────────────────────────────┐
  │ Hardware      ₹5,000 – ₹12,000    │
  │ Connectivity  ₹200 – ₹500/month   │
  │ Maintenance   ₹500 – ₹1,000/yr    │
  │ Training      Significant          │
  └────────────────────────────────────┘
  Total per trip: ₹5,700 – ₹13,500+

  FrostGuard approach
  ┌────────────────────────────────────┐
  │ Indicator sticker   ₹2 – ₹5       │
  │ QR label            ₹0.50          │
  │ AI analysis         ₹0.02/scan     │
  │ Hardware            ₹0 (use phone) │
  └────────────────────────────────────┘
  Total per trip: ₹2.52 – ₹5.52

  Savings: 99.95% cost reduction 🎯
────────────────────────────────────────────


Getting Started

bash# Clone the repo
git clone https://github.com/JaasirMJ/FrostGuardtheAI
cd FrostGuardtheAI

# Open directly — no install needed
open index.html        # Mac
start index.html       # Windows

Enable Real AI


Get a free API key at aistudio.google.com
Paste it in the Gemini API Key field in the top bar
Upload a real indicator photo on the AI Analysis page



Target Customers

SegmentWhoHealthcareGovernment hospitals, PHCs, NGOs, vaccine distributorsPharmaMedical distributors, diagnostic labsFoodDairy companies, milk cooperatives, seafood exporters

Business Model

PlanPriceForStarter₹999/monthSmall clinics, NGOsEnterprise₹10,000+/monthHospitals, distributorsIndicator packsPer shipmentPhysical consumables





License

Hack Of Us © 2026 FrostGuard AI
