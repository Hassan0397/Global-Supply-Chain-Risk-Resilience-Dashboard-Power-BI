# 📊 Global Supply Chain Risk & Resilience Dashboard — Power BI

An interactive **Power BI** project designed to help executives, procurement, logistics, finance, and risk teams monitor supply chain risks, delays, and cost impacts while enabling scenario planning for resilience.

---

## 🚨 Problem Statement

Global supply chains are complex and exposed to multiple risks (supplier delays, route disruptions, geopolitical events, weather). Companies often struggle to:

- Identify high-risk suppliers and routes quickly  
- Quantify potential impact on lead time and costs  
- Make informed decisions to mitigate delays and losses  
- Track operational KPIs and exposure in real-time  

**This project consolidates supply chain, shipment, and risk data into a single dashboard to enable actionable insights and risk mitigation.**

---

## ✅ Solution

The dashboard provides:

- **Supply Chain KPIs:** On-Time Delivery %, Average Lead Time, Delay Rate %, Supplier Reliability %, Risk Score, Risk-Adjusted Lead Time & Cost, Exposure $  
- **Visualization:** Executive overview, supplier ranking, route/port maps, and what-if scenario analysis  
- **Interactive Filters:** Region, Supplier, Route, Product, Risk Level, Transport Mode, Time  
- **Scenario Analysis:** Simulate supplier failures to assess risk impact  
- **Decision Support:** Helps executives, procurement, logistics, and finance prioritize risk mitigation  

---

## 🚀 Project Workflow

### 🟦 1. Project Planning & Requirements
- Define one-line goal: **"Identify supply chain risks, assess impact, and prioritize mitigation."**  
- Target users: Executives, Procurement, Logistics/Operations, Risk/Compliance, Finance  
- Key questions: Supplier reliability, route delays, on-time delivery %, risk-adjusted costs, exposure, hotspot regions, scenario outcomes  

---

### 🟩 2. Data Collection & Preparation
Required datasets:

- `Suppliers.csv` → SupplierID, name, country, historical on-time %, contracts  
- `Products.csv` → ProductID, category, criticality (A/B/C), unit cost  
- `Shipments.csv` → ShipmentID, supplier, product, route, promised/shipped/delivered dates, quantity, cost  
- `Routes.csv` → RouteID, origin/destination, transport mode  
- `RiskEvents.csv` → date, country/port, event type, severity  
- `Calendar.csv` → dates, weeks, months, quarters, years  
- Optional: Backup suppliers/routes, FX rates, CO₂ per route  

Tasks:

- Clean and standardize datasets  
- Ensure proper data types (Date, Currency, Decimal, Whole Number)  
- Handle missing values  

---

### 🟨 3. Data Modeling
- Build a **star schema** in Power BI  
- **Dimension Tables:** `dim_supplier`, `dim_product`, `dim_route`, `dim_date`  
- **Fact Tables:** `fact_shipments`, `fact_risk_events`  
- Set relationships: Many-to-One from fact tables to dimensions  
- Mark `dim_date` as the **Date Table** for time intelligence  

---

### 🟥 4. Transformations (Power Query)
- Standardize column names and formats  
- Replace nulls with defaults where appropriate  
- Create derived columns:
  - Risk-Adjusted Lead Time = `LeadTime * (1 + RiskFactor)`  
  - Risk-Adjusted Cost = `Cost * (1 + RiskFactor)`  
- Categorize risk levels (e.g., Low, Medium, High)  

---

### 🟪 5. DAX Measures (KPIs)
- **On-Time Delivery %** → `DIVIDE(COUNTROWS(FILTER(fact_shipments, DeliveredOnTime=TRUE)), COUNTROWS(fact_shipments), 0)`  
- **Average Lead Time (days)** → `AVERAGE(fact_shipments[LeadTime])`  
- **Delay Rate %** → `DIVIDE(COUNTROWS(FILTER(fact_shipments, DeliveredOnTime=FALSE)), COUNTROWS(fact_shipments), 0)`  
- **Supplier Reliability %** → `DIVIDE(COUNTROWS(FILTER(fact_shipments, DeliveredOnTime=TRUE && SupplierID=SelectedSupplier)), COUNTROWS(FILTER(fact_shipments, SupplierID=SelectedSupplier)), 0)`  
- **Risk Score (0–100)** → weighted composite from country, weather, strike, historical delays  
- **Risk-Adjusted Lead Time** → `LeadTime * (1 + RiskFactor)`  
- **Risk-Adjusted Cost** → `Cost * (1 + RiskFactor)`  
- **Exposure ($)** → sum of `Cost` for high-risk suppliers/routes  
- **Perfect Order Rate %** → `COUNTROWS(FILTER(fact_shipments, PerfectOrder=TRUE)) / COUNTROWS(fact_shipments)`  

---

### 🟧 6. Report Pages & Visuals

**1️⃣ Executive Overview**

- KPI Cards: On-Time Delivery %, Average Lead Time, Risk Score, Exposure $  
- Trend Line: Delivery performance over time  
- Map: Risk hotspots by country/region  
- Top 5 Suppliers/Risk Ranking  

**2️⃣ Supplier Analysis**

- Table: Supplier reliability, risk score, exposure $  
- Bar/Column: Top risk contributors  
- Filters: Supplier, Product, Risk Level  

**3️⃣ Route & Map Analysis**

- Map: Routes and ports by delay frequency  
- KPIs: Route-level performance and exposure  
- Filters: Origin, Destination, Transport Mode  

**4️⃣ What-If / Scenario Analysis**

- Simulate supplier failure or route disruption  
- Adjust risk factor and observe impact on Exposure $ and Risk-Adjusted Lead Time  
- Interactive slicers to test multiple scenarios  

---

### 🟨 7. Usage

1. Open `.pbix` in **Power BI Desktop**  
2. Load sample datasets (CSV files included)  
3. Refresh data sources  
4. Apply slicers (Region, Supplier, Route, Product, Risk Level, Time)  
5. Navigate through 4 report pages for full insights  
6. Use What-If controls to simulate supplier failures  

---

### 🧠 Key Outcomes

- Identify top 5 risky suppliers in under 10 seconds  
- View risk hotspots on map and drill into shipments  
- Compare original vs. risk-adjusted lead time and cost  
- Run “Supplier Offline” scenario and see impact on exposure  
- Supports informed decision-making for executives, procurement, logistics, and finance  

---

### 🛠 Tools Used

- **Power BI Desktop**  
- **Power Query** (ETL transformations)  
- **DAX** (KPIs & analytics)  
- **CSV / Excel** for source data  

---

### 📚 Skills Demonstrated

- Data modeling with star schema  
- DAX measures for supply chain KPIs  
- Scenario & what-if analysis  
- Interactive dashboards with maps, slicers, and filters  
- Professional dashboard design for executives and managers  

