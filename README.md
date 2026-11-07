# SiteCare: Autonomous Depot Optimization

Autonomous depot intelligence, predictive maintenance, and dynamic grid optimization for mission-critical electric vehicle charging infrastructure.

Developed for the Kempower Challenge 2026.

---

## Overview

High-power commercial fleet charging depots—such as municipal transit hubs and logistics centers—face stringent uptime requirements. A single charger failure during overnight charging can cause cascading departure delays, contractual Service Level Agreement (SLA) penalties, and service disruptions. Concurrently, unmanaged charging during peak electricity tariff windows strains local grid connections and inflates operating expenses.

SiteCare addresses these challenges through two automated subsystems:

1. **Predictive Hardware Anomaly Detection:** Identifies thermal anomalies and intermittent fault signatures in high-power charging cabinets prior to critical failure, orchestrating proactive field service and load rerouting.
2. **Dynamic Grid and Tariff Optimization:** Schedules vehicle charging sessions against day-ahead spot electricity prices while enforcing strict site-level power ceilings to avoid peak demand penalties.

---

## Core Scenarios

The accompanying demonstration models two distinct operational environments:

### Scenario 1: S1 Bus Depot North (Predictive Maintenance & SLA Protection)

* **Asset:** Cabinet C1-3 (360 kW Power Unit).
* **Observed Condition:** Operating at 58.9°C peak (+14.9°C above peer cabinets F010 and F012), following two intermittent fault logs on November 9 and 10. At 01:50, an F015 warning triggers a 50% derate.
* **Operational Risk:** Vehicle B09 requires a 90% State of Charge (SoC) prior to 06:00 departure. Three additional buses are queued across associated dispensers D1-9 through D1-12. Unmitigated shutdown risks €600 in contract SLA penalties (€150 per missed departure).
* **Automated Mitigation:**
  * Auto-dispatches certified technician TE1 with required arrival before 04:00.
  * Quarantines dispensers D1-9 through D1-12 against new high-current sessions to arrest thermal escalation.
* **Operational Comparison:**

| Parameter | Baseline (Unmanaged) | SiteCare Automated Intervention |
|---|---|---|
| Failure Event | Thermal shutdown at 02:25 | Proactive derate and controlled dispatch |
| Field Service | Reactive dispatch; repaired at 06:31 | Proactive dispatch; on-site before 04:00 |
| Fleet Impact | 4 buses missed morning departure | 0 missed departures; SoC targets met |
| Contract Penalty | €600 | €0 |

---

### Scenario 2: S2 Logistics Depot East (Smart Energy & Grid Peak Shaving)

* **Site Constraints:** 400 kW maximum site grid capacity.
* **Market Dynamics:** Significant tariff delta between 18:00 peak (€82.33 / 100 kWh) and 20:00 off-peak (€11.06 / 100 kWh) — a difference of €71.27 / 100 kWh.
* **Optimization Logic:**
  * Classifies vehicles by departure urgency and current SoC.
  * Prioritizes high-urgency vehicles while shifting flexible demand into lower-cost tariff intervals.
  * Dynamic power throttling ensures aggregate site consumption remains strictly under the 400 kW threshold.
* **Simulation Results:**

| Metric | Unmanaged Charging | SiteCare Smart Charging | Impact |
|---|---|---|---|
| Trucks Below Target SoC | 4 | 1 | 75% reduction |
| Grid Limit Violations (>400 kW) | 0 | 0 | 100% compliance |
| Total Energy Cost | €689 | €482 | 30.0% savings |

---

## Demonstration Application

The demonstration interface is implemented as a lightweight, zero-dependency single-page application.

### Technical Implementation

* **Frontend:** Standards-compliant HTML5, CSS3, and ES6 JavaScript.
* **Graphics:** Inline vector SVG for price curve visualization.
* **Runtime Dependencies:** None. No Node.js build process, package manager, or external CDN dependencies are required.
* **Design Standards:** Tailored to industrial monitoring systems, incorporating high data density and Kempower visual branding conventions.

### Running the Application

Clone the repository and open `index.html` in any modern web browser:

```bash
git clone https://github.com/phamduchaianh/site-care.git
cd site-care

# Open in browser directly
xdg-open index.html       # Linux
open index.html           # macOS
start index.html          # Windows

# Or run via local static web server
python3 -m http.server 8080
```

---

## Integration Architecture

SiteCare is structured for integration into existing EV depot management ecosystems:

* **Telemetry Ingestion:** Consumes cabinet and dispenser sensor streams (temperatures, power outputs, error codes) via OCPP 2.0.1 and Kempower ChargEye telemetry APIs.
* **Fleet Schedule Synchronization:** Connects with fleet management systems (FMS) via standard REST/GraphQL interfaces to ingest route departure schedules and required battery capacities.
* **Grid and Market Feeds:** Ingests regional day-ahead electricity spot market feeds (such as Nord Pool or ENTSO-E) and local distribution system operator (DSO) constraint limits.
* **Control Dispatch:** Issues dynamic current-limit and reservation commands back to charging hardware via OCPP Smart Charging profiles.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
