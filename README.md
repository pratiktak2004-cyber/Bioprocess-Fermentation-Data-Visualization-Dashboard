# Bioprocess-Fermentation-Data-Visualization-Dashboard
An enterprise-grade Data Visualization dashboard and relational data model in Microsoft Excel for real-time bioprocess monitoring, advanced Data Visualization curves, and automated Statistical Process Control (SPC).
graph TD
%% --- DATA ARCHITECTURE & DIMENSIONS ---
subgraph Data_Architecture ["Relational Data Architecture (Backend)"]
    direction LR
    DM["Dim_Batch_Master<br/>*(Batch ID, Vessel, Target)*"]
    DC["Dim_Control_Limits<br/>*(DO, pH & Temp Thresholds)*"]
    FT["Fact_Batch_Telemetry<br/>*(Time-Series Logs: DO, pH, Biomass, Temp)*"]
    
    DM -->|"1 : N"| FT
    DC -.->|"Validation Rule"| FT
end

%% --- USER CONTROL INPUT ---
subgraph User_Input ["User Interaction Layer"]
    UI["Dashboard Cell B1<br/>*Select Batch ID Dropdown*"]
end

%% --- DYNAMIC FILTER ENGINE ---
subgraph Processing_Engine ["Dynamic Filtering Engine"]
    UI -->|"Triggers Batch ID Filter"| FE["Excel FILTER & XLOOKUP Formula<br/>*(Extracts active batch time-series)*"]
    FT -->|"Feeds Raw Logs"| FE
end

%% --- DATA VISUALIZATION LAYER ---
subgraph Data_Visualization_Dashboard ["Executive Data Visualization Layer (Dashboard Tab)"]
    direction TB
    
    %% Helper Range
    HR["Dynamic Helper Range J6:N14<br/>*(Spilled Time-Series Array)*"]
    FE -->|"Spills Filtered Rows"| HR
    
    %% KPI Cards
    subgraph KPI_Cards ["KPI Data Visualization Cards"]
        KP1["Peak Biomass (g/L)<br/>*MAXIFS Formula*"]
        KP2["Batch Progress (%)<br/>*Elapsed Hrs / 48*"]
        HR --> KP1
        HR --> KP2
    end
    
    %% Dual-Axis Chart
    subgraph Chart_Engine ["Dual-Axis Combo Chart (Data Visualization)"]
        CA["Primary Y-Axis<br/>*DO (%) & pH Curves*"]
        CB["Secondary Y-Axis<br/>*Biomass (g/L) & Temp (°C)*"]
        CX["X-Axis (Elapsed Hours)<br/>*Cell Range J6:J14*"]
        HR --> CA
        HR --> CB
        HR --> CX
    end
    
    %% SPC Alert Status
    subgraph SPC_Engine ["Statistical Process Control (SPC)"]
        SP["SPC Alert Pill Cell H1<br/>*MIN/MAX Excursion Check*"]
        CF["Conditional Formatting<br/>*Green ('In Control') / Red ('Out of Spec')*"]
        HR --> SP
        SP --> CF
    end
end

%% Final Output / Visual Rendering
Data_Visualization_Dashboard -->|"Live Interactive Rendering"| Final["Executive Presentation Layer<br/>*Complete Portfolio-Ready Dashboard*"]
