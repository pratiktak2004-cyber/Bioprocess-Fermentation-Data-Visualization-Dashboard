# Bioprocess Fermentation & Data Visualization Dashboard
### *Advanced Data Visualization & Statistical Process Control in Excel*

An enterprise-grade **Data Visualization** dashboard and relational data model built in Microsoft Excel for real-time bioprocess monitoring, advanced **Data Visualization** curves, and automated Statistical Process Control (SPC). 

This project simulates a biomanufacturing execution environment—leveraging comprehensive **Data Visualization** techniques to track key bioprocess parameters (Dissolved Oxygen, pH, Temperature, and Biomass accumulation) across 48-hour fermentation runs with automated Statistical Process Control (SPC) visual alerts.

---

## Project Overview & Data Visualization Strategy

In industrial biotechnology and bioprocess engineering, effective **Data Visualization** of critical process parameters (CPPs) in real time is vital for yield optimization, batch consistency, and regulatory compliance (cGMP). 

This project demonstrates an end-to-end data pipeline and **Data Visualization** architecture within Excel:
1. **Relational Data Architecture:** Normalized schema separating batch metadata, operational control thresholds, and time-series telemetry to feed the **Data Visualization** engine.
2. **Dynamic Filtering Engine:** Spill-range dynamic lookup formulas (`FILTER`, `XLOOKUP`, `MAXIFS`) that drive real-time **Data Visualization** updates based on user inputs.
3. **Multi-Variable Data Visualization:** Dual-axis plotting and interactive curves mapping sigmoidal cell growth against critical physiological parameters.
4. **Statistical Process Control (SPC):** Automated conditional logic and visual alert indicators alerting operators to parameter excursions outside safe operating windows.

---

##  Repository & Data Architecture

The workbook is structured into a normalized 4-tab model following database design best practices, feeding directly into the top-layer **Data Visualization** interface:

```text
[ Dim_Batch_Master ] ────────┐
                             │ (1:N Relational Link)
                             ▼
[ Dim_Control_Limits ] ──> [ Fact_Batch_Telemetry ] 
                                  │
                                  ▼ (Dynamic FILTER Engine)
                           [ Dashboard / Data Visualization Layer ]
                             ├── Dynamic Helper Range (J6:N14)
                             ├── Executive KPI Cards & MAXIFS
                             ├── Dual-Axis Combo Chart Visuals
                             └── SPC Conditional Alert Indicator (H1)
