# CrisisConnect

**Autonomous Offline-First Disaster Management, Mesh Networking & UAV Aerial Triage Ecosystem**

---

## The Problem

When disaster strikes, cellular towers flood, fiber backbones sever, and power grids fail — creating a communication blackout during the "Golden Hour" of disaster response, exactly when coordination matters most.

- **483+** deaths in the 2018 Kerala floods, with official audits confirming alert and communication failures *(Source: CAG Audit Report, 2021)*
- **~7,000 of 14,167** cell tower sites (~50%) went down in West Bengal during Cyclone Amphan *(Source: The Quint / Economic Times, 2020)*
- **4,083+** people remained officially missing three months after the 2013 Uttarakhand floods, with no centralized tracking system *(Source: The Hindu, 2013)*

**CrisisConnect** closes this gap — a national-scale, offline-first disaster management ecosystem that keeps rescue coordination alive without depending on active telecom infrastructure.

---

## How It Works

CrisisConnect operates across the full disaster lifecycle in three phases:

### 🟢 Pre-Disaster — Preparedness
- Ingests official Common Alerting Protocol (CAP) feeds from SACHET/NDMA
- Pre-caches offline vector maps and computes safe-zone evacuation routes
- Runs quietly in the background — zero setup needed when disaster strikes

### 🔴 During-Disaster — Active Response
- **Automatic SOS activation** the instant cellular signal is lost — no manual tap required
- Phone-to-phone **BLE / Wi-Fi Direct mesh relay** with TTL-based deduplication
- **Autonomous UAV relays** and LoRa buoys extend coverage where the ground mesh can't reach
- **P0–P3 triage prioritization** so critical medical cases (trapped, bleeding, infants) are surfaced first
- Two-way SIP VoIP audio from drones for direct victim-to-rescuer communication

### 🔵 Post-Disaster — Recovery & Reunification
- Offline incident data syncs via a **conflict-free causal merge engine** (Lamport timestamps)
- Optimized routing (VRPTW) to the nearest available shelter or hospital
- **Fuzzy-logic name matching** (Jaro-Winkler, Levenshtein) reunites families across misspelled, inconsistent shelter records

---

## Key Features

| Feature | Description |
|---|---|
| 🌐 Zero-hardware-cost mesh | Runs entirely on phones people already own — no proprietary radios |
| ⚡ Automatic SOS trigger | Fires on signal loss, removing the single biggest point of human failure |
| 🚁 UAV-extended coverage | Drones bridge mesh gaps in large or sparsely populated disaster zones |
| 🏥 Smart triage | P0–P3 priority queue ensures critical cases are never lost in the noise |
| 🔄 Command failover | Deputy CPOC automatically takes over if the main command server goes dark |
| 🔒 Privacy by design | AES-256 encryption, auto-purged medical data, DPDP Act 2023 compliant |
| 🧩 Self-hostable | Fully open-source and deployable on-premise — no vendor lock-in |

---

## Tech Stack

**Mobile & Frontend**
- Flutter / React Native + SQLite (Drift) — offline-first mobile client
- MapLibre GL Native + Protomaps (PMTiles) — offline vector maps
- Next.js + Vite + Tailwind CSS + Recharts — Command Center web portal

**Mesh & Communication**
- BLE 5.2 / Google Nearby Connections API — phone-to-phone mesh
- Protocol Buffers (Protobuf) — sub-96-byte SOS packet serialization
- LoRaWAN (868/915 MHz) — long-range UAV/buoy telemetry
- MAVLink / PX4 Autopilot — drone flight control integration

**Backend & Data**
- FastAPI (Async ASGI) — core API server
- PostgreSQL 16 + PostGIS — geospatial database
- Redis — real-time state and triage queue caching
- MinIO S3 — self-hostable object storage

**AI / Algorithms**
- TensorFlow Lite — onboard thermal victim detection
- Google OR-Tools — VRPTW-based UAV route optimization
- Jaro-Winkler + Levenshtein + Double Metaphone — fuzzy person matching

**Government Integrations**
- NDMA SACHET (CAP alert feed)
- ISRO Bhuvan (geospatial layers)
- MeitY Bhashini (multilingual NLP)

---

## Architecture

```
Civilian Mobile App ──BLE/Wi-Fi Mesh──> Nearby Devices
        │                                     │
        └──LoRa Telemetry──> UAV Relay ───────┘
                                  │
                          MAVLink Backhaul
                                  │
                      Command Center (FastAPI)
                                  │
                    PostgreSQL + PostGIS + Redis
```

See [`/docs/architecture.md`](docs/architecture.md) for the full system design, sequence diagrams, and data flow.

---

## Getting Started

### Prerequisites
- Flutter SDK ≥ 3.x
- Python ≥ 3.11
- PostgreSQL ≥ 16 with PostGIS extension
- Redis ≥ 7.x

### Installation

```bash
# Clone the repository
git clone https://github.com/<your-org>/crisisconnect.git
cd crisisconnect

# Backend setup
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload

# Mobile app setup
cd ../mobile
flutter pub get
flutter run
```

### Environment Variables

Create a `.env` file in `/backend` with:

```
DATABASE_URL=postgresql://user:password@localhost:5432/crisisconnect
REDIS_URL=redis://localhost:6379
SACHET_API_KEY=your_key_here
```

---

## Project Links

- 📦 **Source Code:** [GitHub Repository](#)
- 🎥 **Demo Video:** [YouTube](#)
- 🌐 **Live Prototype:** [Try it here](#)

*(Replace the placeholder links above with your actual repo, video, and prototype URLs.)*

---

## Compliance & Standards

CrisisConnect is designed in alignment with:
- Disaster Management Act 2005 (Amendment 2025)
- NDMA Incident Response System (IRS) Guidelines
- Digital Personal Data Protection (DPDP) Act 2023
- Drone Rules 2021 / Digital Sky framework
- Common Alerting Protocol (CAP) standard
- RFC 4838 — Delay-Tolerant Networking Architecture

---

## Roadmap

- [x] Mesh protocol & Protobuf packet engine
- [x] Offline vector map caching
- [ ] PX4 companion stack & SIP VoIP integration
- [ ] Google OR-Tools VRPTW algorithm deployment
- [ ] Bhashini & Bhuvan API integration
- [ ] NDRF multi-district mock drill validation

---

## Team

**Lead Architect:** Garv & Team
**Event:** Smart India Hackathon 2026, Open Innovation Track

---

## License

This project is licensed under the MIT License — see [`LICENSE`](LICENSE) for details.

---

## Contributing

Contributions are welcome. Please open an issue to discuss proposed changes before submitting a pull request.

---

*Built to close the Golden Hour Blackout — because rescue coordination shouldn't depend on cell towers staying up.*
