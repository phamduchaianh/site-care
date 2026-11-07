# ⚡ SiteCare — Autonomous Depot Optimization

> **Kempower Hackathon 2026 Project**  
> Autonomous depot intelligence, predictive maintenance, and dynamic grid optimization for mission-critical EV fleet charging.

[![Kempower Hackathon](https://img.shields.io/badge/Hackathon-Kempower%202026-ff6700.svg)](https://kempower.com)
[![Status](https://img.shields.io/badge/Status-Demo%20Ready-10b981.svg)]()
[![Stack](https://img.shields.io/badge/Stack-HTML5%20%7C%20CSS3%20%7C%20Vanilla%20JS-blue.svg)]()
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero%20External-orange.svg)]()
[![License](https://img.shields.io/badge/License-MIT-gray.svg)](LICENSE)

---

## 📌 Executive Summary

Modern electric bus depots and commercial logistics hubs operate under strict operational constraints: razor-thin departure schedules, severe SLA breach penalties (€150+ per missed departure), and soaring peak electricity rates with strict local grid limits.

**SiteCare** is an intelligent, autonomous depot optimization system designed specifically for high-power DC fast-charging infrastructure (such as Kempower Satellite & Power Unit systems). It combines:
1. **Predictive Hardware Anomaly Detection:** Intercepts thermal anomalies and power derates hours before catastrophic shutdown occurs, autonomously scheduling certified technicians and isolating at-risk dispensers.
2. **Dynamic Grid & Spot-Price Optimization:** Shifts non-urgent charging demand away from high peak-tariff hours into low-cost energy windows while enforcing hard site grid ceilings (400 kW) and guaranteeing vehicle target State-of-Charge (SoC).

---

## 🎯 Live Interactive Demo

The demo is a lightweight, zero-dependency, single-page application built to simulate real-world depot operations across two distinct operational sites:

| Depot Site | Primary Role | Operational Focus |
|---|---|---|
| **S1 Bus Depot North** | Public Transit Fleet | Predictive Maintenance, Fleet Departure SLA Protection |
| **S2 Logistics Depot East** | Delivery & Heavy Transport | Spot Price Arbitrage, Grid Constraint Management |

### 🚀 Running the Demo Locally
No build step or runtime installation required:
```bash
# Clone the repository
git clone https://github.com/phamduchaianh/site-care.git
cd site-care

# Open directly in your browser
xdg-open index.html   # Linux
open index.html       # macOS
start index.html      # Windows

# Or serve via any local static server
python3 -m http.server 8080
# Visit http://localhost:8080
```

---

## 🔍 Key Demo Scenarios

### 1. S1 Bus Depot North — Predictive Anomaly Detection & SLA Defense

```
[01:50 Telemetry]        [SLA Engine]             [Autonomous Orchestrator]
Cabinet C1-3 (360 kW) ──▶ Bus B09 (Dep: 06:00) ──▶ 1. Auto-dispatch Tech TE1 (<04:00)
Temp: 58.9°C (+14.9°C)    3 Queued Morning Buses   2. Quarantine Dispensers D1-9..12
F015 Derate 50%           €600 SLA Penalty Risk    3. Reroute Critical Charging
```

* **The Anomaly:** Cabinet **C1-3 (360 kW)** exhibited an elevated temperature profile (+14.9°C above peer cabinets F010 & F012) and triggered an intermittent derate code (`F015`).
* **The Impact:** Bus **B09** was actively charging (requiring 90% SoC before its 06:00 run), with 3 additional morning rush buses scheduled on dispensers `D1-9` through `D1-12`. Without intervention, a shutdown would cause 4 missed departures and **€600 in contract penalties**.
* **SiteCare Action:**
  - Automatically dispatches certified technician **TE1** with guaranteed arrival before 04:00.
  - Quarantines dispensers `D1-9..D1-12` against high-current draws to prevent thermal runaway while preserving battery readiness.
* **Baseline vs. SiteCare:**
  - *Nov 13 Baseline (Unmanaged):* 02:25 shutdown ➔ 4 missed bus departures ➔ €600 SLA penalty ➔ repair finished late at 06:31.
  - *With SiteCare:* Early warning ➔ proactive technician dispatch ➔ 100% on-time departures preserved.

---

### 2. S2 Logistics Depot East — Smart Energy & Grid Peak Shaving

```
Spot Tariff: €82.33 / 100 kWh (18:00 Peak)  ──▶ Shift to ──▶ €11.06 / 100 kWh (20:00 Low)
Site Grid Ceiling: 400 kW Hard Cap          ──▶ Enforced ─▶ 0 Grid Violations
Cost Reduction: €689 ─────────────────────────────────────▶ €482 (-30.0%)
```

* **Dynamic Spot Arbitrage:** Identifies high hourly tariff spreads (e.g., **€82.33/100 kWh** at 18:00 vs. **€11.06/100 kWh** at 20:00 — a **€71.27/100 kWh potential delta**).
* **Smart Load Management:**
  - Prioritizes tight-deadline vehicles while deferring flexible charging sessions to off-peak tariff periods.
  - Continuously throttles aggregate site draw below the **400 kW grid limit**, avoiding costly demand surges and transformer strain.
* **Interactive Simulation Results:**
  - **Trucks Below Target SoC:** Reduced from **4 ➔ 1**
  - **Grid Violations:** Kept strictly at **0 ➔ 0**
  - **Depot Energy Spend:** Drops from **€689 ➔ €482** (~30% direct savings)

---

## 🛠️ Architecture & Technology

- **Frontend:** Pure HTML5, CSS3 Custom Properties, Responsive Flex/Grid layout, and Vanilla JavaScript.
- **Visualizations:** Inline SVG vector charts for spot price curve comparisons and responsive CSS state transitions.
- **Kempower Design Language:** Integrated brand colors (Kempower Orange `#ff6700`, deep slate `#0f172a`, and clean typography) designed to match industrial charging software aesthetics.
- **Portability:** 100% self-contained in a single `index.html` file with zero build tools, package managers, or external CDN dependencies.

---

## 🔮 Future Roadmap

- [ ] **Real-time OCPP 2.0.1 / ISO 15118 Ingestion:** Direct integration with Kempower ChargEye telemetry streams.
- [ ] **AI-driven Component Lifetime Degradation:** Remaining Useful Life (RUL) forecasting for power modules and cooling fans.
- [ ] **Bi-directional V2G / Depot Battery Storage (BESS):** Automated revenue generation via frequency regulation and peak clipping.
- [ ] **Multi-Depot Fleet Fleet Control:** Enterprise-grade dashboard aggregating across dozens of regional charging hubs.

---

## 👥 Hackathon Team

Developed with ❤️ for the **Kempower Hackathon 2026**.

* Repository: [github.com/phamduchaianh/site-care](https://github.com/phamduchaianh/site-care)
* Demo Application: [`index.html`](index.html)
