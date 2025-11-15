# 📊 Global Supply Chain Risk & Resilience Dashboard — Power BI

An interactive **Power BI** project designed to help executives, procurement, logistics, finance, and risk teams monitor supply chain risks, delays, and cost impacts — all on a single consolidated dashboard.

---

## 🚨 Problem Statement

Global supply chains face multiple risks including supplier delays, route disruptions, geopolitical events, and weather. Companies often struggle to:

- Identify high-risk suppliers and routes quickly  
- Quantify potential impact on lead time and costs  
- Make informed decisions to mitigate delays and losses  

**This dashboard consolidates all supply chain, shipment, and risk data into a single page for actionable insights.**

---

## ✅ Solution

The dashboard provides:

- **Supply Chain KPIs:** On-Time Delivery %, Average Lead Time, Delay Rate %, Supplier Reliability %, Risk Score, Risk-Adjusted Lead Time & Cost, Exposure $  
- **Visualization:** All KPIs, supplier performance, route analysis, risk events, and scenario simulations on one page  
- **Interactive Filters:** Region, Supplier, Route, Product, Risk Level, Transport Mode, Time  
- **Scenario Analysis:** Simulate supplier failure or route disruption and view impact immediately  

---

## 🚀 Project Workflow

### 🟦 1. Project Planning & Requirements
- Goal: **"Identify supply chain risks, assess impact, and prioritize mitigation."**  
- Users: Executives, Procurement, Logistics/Operations, Risk/Compliance, Finance  
- Key questions: Supplier reliability, route delays, on-time delivery %, risk-adjusted costs, exposure, hotspot regions, scenario outcomes  

---

### 🟩 2. Data Preparation
Required datasets:

- `Suppliers.csv` → SupplierID, name, country, historical on-time %, contracts  
- `Products.csv` → ProductID, category, criticality (A/B/C), unit cost  
- `Shipments.csv` → ShipmentID, supplier, product, route, promised/shipped/delivered dates, quantity, cost  
- `Routes.csv` → RouteID, origin/destination, transport mode  
- `RiskEvents.csv` → date, country/port, event type, severity  
- `Calendar.csv` → dates, weeks, months, quarters, years  

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
- Categorize risk levels (Low, Medium, High)  

---

### 🟪 5. DAX Measures (KPIs)
- **On-Time Delivery %** → `DIVIDE(COUNTROWS(FILTER(fact_shipments, DeliveredOnTime=TRUE)), COUNTROWS(fact_shipments), 0)`  
- **Average Lead Time (days)** → `AVERAGE(fact_shipments[LeadTime])`  
- **Delay Rate %** → `DIVIDE(COUNTROWS(FILTER(fact_shipments, DeliveredOnTime=FALSE)), COUNTROWS(fact_shipments), 0)`  
- **Supplier Reliability %** → `DIVIDE(COUNTROWS(FILTER(fact_shipments, DeliveredOnTime=TRUE && SupplierID=SelectedSupplier)), COUNTROWS(FILTER(fact_shipments, SupplierID=SelectedSupplier)), 0)`  
- **Risk Score (0–100)** → composite weighted from country, weather, strike, historical delays  
- **Risk-Adjusted Lead Time** → `LeadTime * (1 + RiskFactor)`  
- **Risk-Adjusted Cost** → `Cost * (1 + RiskFactor)`  
- **Exposure ($)** → sum of `Cost` for high-risk suppliers/routes  
- **Perfect Order Rate %** → `COUNTROWS(FILTER(fact_shipments, PerfectOrder=TRUE)) / COUNTROWS(fact_shipments)`  

---

### 🟧 6. Dashboard Page

[**Global Supply Chain Risk Dashboard**](https://github.com/Hassan0397/Global-Supply-Chain-Risk-Resilience-Dashboard-Power-BI/blob/main/Supply_Chain_Dashboard_Summary%20image.png)

- **KPI Cards:** On-Time Delivery %, Average Lead Time, Risk Score, Exposure $  
- **Supplier Table:** Reliability %, Risk Score, Exposure $  
- **Route & Map Visualization:** Risk hotspots by region and route delays  
- **Trend Charts:** Delivery performance and delays over time  
- **Scenario/What-If Controls:** Simulate supplier failure or route disruption and instantly view impact  
- **Filters/Slicers:** Region, Supplier, Route, Product, Risk Level, Transport Mode, Time  

---

### 🟨 7. Usage

1. Open `.pbix` in **Power BI Desktop**  
2. Load included sample datasets  
3. Refresh data sources  
4. Use slicers (Region, Supplier, Route, Product, Risk Level, Time)  
5. Interact with the single-page dashboard to analyze supply chain risks  
6. Test scenario controls to simulate disruptions  

---

### 🧠 Key Outcomes

- Quickly identify top risky suppliers and routes  
- Monitor overall supply chain performance in real-time  
- Compare original vs. risk-adjusted lead time and cost  
- Assess impact of hypothetical disruptions on exposure $  
- Supports informed decisions for executives, procurement, logistics, and finance  

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
- Interactive, single-page executive dashboards  
- Scenario & what-if analysis  
- Professional dashboard design with maps, tables, charts, and filters  

