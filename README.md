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

## Data Visualization Architecture & Pipeline

```mermaid
graph TD
    A[Raw Batch Telemetry & Master Data] -->|Import & Load| B[(Fact_Batch_Telemetry Table)]
    
    subgraph Data_Architecture ["Relational Data Architecture Backend"]
        C[Dim_Batch_Master] -->|1:N Relationship| B
        D[Dim_Control_Limits] -.->|Validation Rules| B
    end
    
    B -->|Dynamic FILTER & XLOOKUP Formula| E[Dashboard Control Cell B1]
    
    subgraph Data_Visualization ["Executive Data Visualization Layer"]
        E --> F[Dynamic Helper Range J6:N14]
        F --> G[Peak Biomass & Progress KPI Cards]
        F --> H[Dual-Axis Combo Chart Visuals]
        F --> I[SPC Conditional Alert Indicator H1]
    end
    
    Data_Visualization --> J[Interactive Data Visualization Presentation]
