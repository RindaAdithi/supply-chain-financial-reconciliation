# Enterprise Supply Chain Analytics & Financial Reconciliation Model

##  Executive Summary
An end-to-end data analytics and financial auditing solution built to model 5,840 daily operational supply chain transactions across 4 product categories and 4 geographic regions. This project demonstrates core data engineering and analytics capabilities using **Python (NumPy/Pandas)** for data synthesis and safety-stock simulation, **Power BI (DAX)** for interactive executive visualization, and **Excel (LET/XLOOKUP)** for dual-layer financial reconciliation.

---

## Multi-Tool Architecture & Tech Stack

```text
               +-------------------------------------------------------+
               | 1. PYTHON (NumPy & Pandas)                           |
               | - Synthesizes 5,840 daily transaction records          |
               | - Computes dynamic Safety Stock & Reorder Points (ROP) |
               | - Performs vectorized inventory health flagging       |
               +---------------------------+---------------------------+
                                           |
                                           v
               +-------------------------------------------------------+
               | 2. DATASET SERIALIZATION                              |
               | - Enterprise_Supply_Chain_ML_Output.csv                |
               +---------------------------+---------------------------+
                                           |
                   +-----------------------+-----------------------+
                   |                                               |
                   v                                               v
+------------------------------------+   +------------------------------------+
| 3. POWER BI ANALYTICS DASHBOARD    |   | 4. EXCEL FINANCIAL RECONCILIATION  |
| - DAX Measures & Dynamic Aggregations| | - Modern Dynamic Array Formulas     |
| - Matrix ROP Conditional Formatting|   | - LET & XLOOKUP Audit Matrices     |
| - Executive Slicers & KPI Cards    |   | - Automated Discrepancy Spot-Check |
+------------------------------------+   +------------------------------------+
```

- Data Engineering & Simulation (Python): `analysis.py` utilizes **NumPy** for $O(1)$ dictionary pricing lookups, stochastic seasonal variance simulation (88%–128%), dynamic Reorder Point (ROP) math, and vectorized anomaly detection using `np.select`.
- Business Intelligence (Power BI): `Insights Dashboard.pbix` models data using robust DAX measures (`Total Inventory Value`, `Critical Risk Count`, `Stockout Flag`) to enable interactive drill-downs.
- Financial Reconciliation & Audit (Excel): `Financial_Reconciliation_Model.xlsx` serves as an independent control layer, verifying Power BI DAX outputs using `LET`, `XLOOKUP`, and dynamic arrays.

---

##  Repository Directory Structure

```text
supply-chain-financial-reconciliation/
├── analysis.py             # Python script for NumPy data generation & logic
├── Enterprise_Supply_Chain_ML_Output.csv  # 5,840-row operational supply chain dataset
├── Insights Dashboard.pbix            # Power BI interactive executive dashboard
├── Financial_Reconciliation_Model.xlsx    # Excel dual-layer audit & valuation model
└── README.md                              # Project documentation & technical guide
```

---

##  Data Pipeline & Business Logic (`analysis.py`)

The data generation engine simulates 365 days of operational transactions in 2025 across 4 products (`PRD_001_Laptops`, `PRD_002_Monitors`, `PRD_003_Keyboards`, `PRD_004_Processors`) and 4 regions (`North`, `South`, `East`, `West`).

### Key Formulas Implemented:
1. **Demand Simulation**:
   $$\text{Predicted 30-Day Demand} = \lfloor \text{Historical Demand} \times \text{Uniform}(0.88, 1.28) \rfloor$$

2. **Dynamic Reorder Point (ROP)**:
   $$\text{ROP} = \left\lfloor \text{Lead Time (Days)} \times \left( \frac{\text{Historical Demand}}{30} \right) \times 1.5 \right\rfloor$$

3. **Vectorized Inventory Health Status (`np.select`)**:
   - `CRITICAL_STOCKOUT_RISK`: $\text{Current Stock} < \text{ROP}$
   - `OVERSTOCK_WARNING`: $\text{Current Stock} > (\text{ROP} \times 4.5)$
   - `OPTIMAL`: Stock level within healthy operational boundaries.

---

##  Key Analytical Insights & Features

1. **Power BI Dashboard**:
   - **Executive KPI Row**: Total Inventory Valuation ($), Total Units in Stock, Average Supplier Lead Time.
   - **Matrix View**: Category-level breakdown with conditional background formatting based on ROP thresholds.
2. **Excel Audit Matrix**:
   - Compares DAX engine totals against Excel `SUMPRODUCT` and `LET` dynamic calculations.
   - Includes single-SKU lookup reconciliation to identify potential data drift or filter context mismatch.

---

##  How to Run & Reproduce

1. **Generate Data**:
   ```bash
   python analysis.py
   ```
   *Generates `Enterprise_Supply_Chain_ML_Output.csv` containing 5,840 records.*

2. **Open Power BI**:
   - Launch `Insights_Dashboard.pbix` and click **Refresh** to reload the dataset.

3. **Open Excel Reconciliation Model**:
   - Open `Financial_Reconciliation_Model.xlsx` to review the audit layer and formula verification matrices.
