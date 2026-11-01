# ✈️ Airline Route Profitability & FP&A Analysis (2024)

**An airline network financial performance analysis built primarily with Excel PivotTables, with Python supporting advanced visualizations and predictive modeling.**

> **Context:** A simulated airline case study covering a route network originating from Dubai (DXB).  
> **Scope:** 7,974 flights · 30 destinations · calendar year 2024.  
> **Primary tool:** Microsoft Excel (PivotTables, PivotCharts, Conditional Formatting, and KPI formulas).  
> **Supporting tools:** Python (pandas, NumPy, Matplotlib, Seaborn, scikit-learn, and XGBoost).  
> **About this README:** This document describes and interprets the **tables, charts, and results provided in the original project**, without recalculating or replacing them. The dataset is simulated, and its source does not specify a currency.



## 1. Project Background and Business Problem

In the airline industry, a high load factor does not necessarily translate into high profitability due to the impact of costs, airfares, and various other operational factors. If management only monitors total revenue and overall network profits, they can easily overlook loss-making routes or cost drivers that erode the efficiency of specific route groups.

From a **financial analysis perspective**, the core objective is not merely identifying profitable versus loss-making flights, but also uncovering the root causes behind performance disparities across short, medium, and long-haul route groups. **To address this challenge, the project developed a flight-level financial and operational reporting system using PivotTables and PivotCharts in Excel**.

**Central Question: How can an airline improve route profitability by optimizing capacity utilization, revenue efficiency, cost structure, and seasonality?**
---

## 2. Dataset and Analytical Approach

### 2.1. Dataset Overview

| Attribute | Description |
|---|---|
| Analysis period | 2024 |
| Number of records | **7,974** |
| Observation unit | One flight record |
| Destinations | **30**, all originating from DXB |
| Route categories | Short Haul / Medium Haul / Long Haul |
| Aircraft types | Airbus A320, A350-900, A380; Boeing 737-800, 777-300ER, 787-9 |
| Seasons | Low / Normal / Shoulder / Peak |
| Flight-level financial data | Ticket Revenue, Ancillary Revenue, cost components, Total Revenue, Total Cost, Profit, Profit Margin |
| Operational data | Passengers, Aircraft Capacity, Load Factor, Flight Hours, Destination, Route Category |
| Additional analytical fields | Distance, RASK, CASK, Break-even Load Factor, and other metrics |

### 2.2. Data Dictionary by Category

| Data group | Selected variables | Analytical purpose |
|---|---|---|
| Flight identifiers | `Flight_Number`, `Flight_Date`, `Origin`, `Destination`, `Route` | Identify flights and analyze results by route and date |
| Operations | `Aircraft_Type`, `Aircraft_Capacity`, `Passengers`, `Load_Factor`, `Flight_Hours` | Assess transportation capacity and operational efficiency |
| Segmentation | `Route_Category`, `Demand_Level`, `Season` | Compare haul length, demand segments, and seasons |
| Revenue | `Ticket_Revenue`, `Ancillary_Revenue`, `Total_Revenue` | Measure revenue generation |
| Cost | `Fuel_Cost`, `Sales_Distribution_Cost`, `Overhead_Cost`, `Depreciation_Cost`, and other expenses | Examine cost levels and cost composition |
| Profitability | `Total_Cost`, `Profit`, `Profit_Margin` / `PM` | Measure financial outcomes |
| Unit economics | `Distance`, `RASK`, `CASK`, `RASK_CASK_Spread` | Compare performance per available seat-kilometer |

### 2.3. Data Preparation

The notebook includes steps to load the Excel dataset, inspect its row and column counts, check duplicates and missing values, process incomplete fields, and add destination-based distances. The Excel workbook contains the prepared data and metrics used to construct the PivotTable reporting framework.

**The project's core analytical method** is to use existing fields and additional metrics to create multiple business views through PivotTables. Changing Rows, Columns, Values, and Filters makes it possible to compare profitability across Route, Month, Season, Route Category, and Aircraft Type.

---

## 3. Business Questions 

| Analysis area | Key question |
|---|---|---|
| Network Performance | How much revenue, cost, and profit does the network generate? |
| Route Profitability | Which destinations have the highest and lowest Average PM? | 
| Capacity | How is Load Factor related to Profit Margin? |
| Cost | Which expenses dominate, and how does the cost mix differ across route categories? | 
| Unit Economics | What do RASK and CASK reveal about route efficiency? |
| Fleet | How does performance differ by aircraft across Short, Medium, and Long Haul? |
| Seasonality | Which months and seasons show lower LF, RASK, and profit? |
| Break-even | Which route segments require higher LF to break even? | 
| Exceptions | Which flights have LF above 85% yet still incur losses? |
| Predictive Modeling | How well can operational features predict PM? | 

---

## 4. Analysis and Results

### 4.1. Financial Snapshot — Network Performance in 2024

| KPI | Reported result |
|---|---:|
| **Total Revenue** | **2,371,756,240** |
| **Total Cost** | **1,796,275,579** |
| **Total Profit** | **575,480,661** |
| **Overall Profit Margin (Profit / Revenue)** | **24.26%** |
| **Average of PM (flight-level)** | **6.19%** |
| Number of flights | **7,974** |
| Number of destinations | **30** |

![Figure 01 — Financial Snapshot](assets\

**Finding:** The network is profitable in aggregate. However, these totals do not reveal the degree of variation across destinations and haul categories. Route-level analysis is therefore necessary to identify where margins are strongest and which segments reduce overall efficiency. This also illustrates why FP&A reporting should combine **revenue, absolute profit, and profit margin** rather than relying on a single measure.

### 4.2. Route Profitability — Best- and Worst-Performing Destinations

Based on the PivotChart ranking of **Average of PM**:

| Top routes | Average PM | Bottom routes | Average PM |
|---|---:|---|---:|
| FRA | 46.08% | CAI | -83.96% |
| SIN | 42.07% | AMM | -76.29% |
| CDG | 41.27% | JED | -68.19% |
| BKK | 39.91% | RUH | -41.20% |
| HKG | 38.67% | LAX | -15.59% |

![Top and Bottom Route Margins](assets/18_route_margin_rankings.png)

*Figure 18 — Top 15 and Bottom 15 routes by Average PM. Place directly after the route ranking table.*

**Finding:** FRA, SIN, CDG, BKK, and HKG stand out with relatively high average margins, whereas CAI, AMM, JED, and RUH show substantial negative margins. These results support differentiated route management strategies. For loss-making routes, FP&A should further review Revenue/Pax, Cost/Pax, ticket pricing, and allocated costs before considering schedule frequency or aircraft configuration changes.

**Management relevance:** Rankings identify where analytical resources should be concentrated instead of assuming that every route within a given haul-length category delivers similar economics.

### .3. Load Factor — High Seat Occupancy Does Not Necessarily Mean High Profit

![Average Load Factors by Destination](assets/02_load_factor_by_destination.png)

*Figure 02 — Average Load Factors by Destination. Colors represent Route Category; the horizontal line is the median shown in the chart.*

Load Factor varies across destinations, reflecting differences in demand and seat utilization. Nevertheless, load factor is only one part of the financial equation: even a flight carrying many passengers may generate insufficient Revenue per Passenger to cover Cost per Passenger.

![Load Factors vs PM](assets/03_load_factor_vs_margin.png)

*Figure 03 — Scatter plot of Load Factor versus PM, grouped by haul category with trendlines.*

The scatter plot indicates a positive association between Load Factor and PM in certain route categories. The **Long Haul trendline has R² ≈ 0.5472**, while the **Short Haul trendline has R² ≈ 0.5248**. This suggests that load factor is associated with margin variation within these groups, but it does not explain all profitability differences.

**Finding:** Capacity utilization matters, but **it is not sufficient on its own** to determine route economics. Load Factor should therefore be assessed alongside RASK, CASK, and cost structure rather than treated as a standalone measure of success.

### 4.4. Cost Structure — Which Components Drive Expenses?

![Cost Structure](assets/04_total_cost_structure.png)

*Figure 04 — Total cost components ranked using an Excel PivotChart.*

The following cost categories feature prominently in the analysis:

| Cost category | Approximate share | FP&A significance |
|---|---:|---|
| Fuel Cost | 20.6% | Flight operations and fuel exposure |
| Sales & Distribution Cost | 19.8% | Efficiency of sales and distribution channels |
| Overhead Cost | 15.9% | Shared expenses allocated to flights |
| Depreciation Cost | 11.2% | Aircraft and other asset usage costs |

**Finding:** Fuel is one of the largest cost items, but Sales & Distribution, Overhead, and Depreciation also account for substantial shares. Cost improvement hypotheses should therefore examine **commercial costs, fixed expenses, and allocated expenses** rather than focusing only on fuel.

![Cost Structure by Routes](assets/05_cost_mix_by_haul.png)

*Figure 05 — 100% stacked column chart comparing cost composition across Long, Medium, and Short Haul.*

This chart goes beyond identifying the largest expenses across the network: it shows **how the cost mix differs by Route Category**. It provides a foundation for investigating which expenses change with flight hours, passenger counts, or route characteristics.

### 4.5. RASK vs CASK — Performance per Available Seat-Kilometer

Unit economics are particularly useful when comparing flights with substantially different distances and seating capacities.

```text
ASK = Aircraft Capacity × Distance
RASK = Total Revenue / ASK
CASK = Total Cost / ASK
RASK - CASK = Profit / ASK
```

![RASK vs CASK](assets/06_rask_cask.png)

*Figure 06 — Excel scatter plot of RASK versus CASK, preserving the original plotted points and trendline.*

The chart compares revenue generation and costs on the same unit-of-capacity basis. For each route, the difference between RASK and CASK indicates whether revenue per available seat-kilometer covers the corresponding cost.

![ASK Spread by Destination](assets/07_ask_spread.png)

*Figure 07 — ASK Spread by Destination. Place directly after the RASK vs CASK figure.*

**Finding:** A positive spread indicates unit revenue exceeding unit cost, while a negative spread flags a route for further investigation. The purpose for FP&A is not merely to rank these spreads, but to connect them to underlying drivers such as Load Factor, revenue mix, flight hours, and cost allocation.

### 4.6. Fleet Efficiency — Aircraft Type and Route Length

![Aircraft by Route Category PM Pivot](assets/11_aircraft_by_haul.png)

*Figure 11 — PivotTable heatmap of Average PM by Aircraft Type × Route Category.*

| Aircraft Type | Long Haul | Medium Haul | Short Haul |
|---|---:|---:|---:|
| Airbus A320 | — | 31.50% | -13.05% |
| Airbus A350-900 | 10.75% | 14.91% | -82.06% |
| Airbus A380 | 29.52% | -15.34% | — |
| Boeing 737-800 | — | 29.40% | -13.56% |
| Boeing 777-300ER | 18.77% | 12.95% | — |
| Boeing 787-9 | 34.62% | 10.73% | -77.74% |

**Finding:** Average PM differs markedly across aircraft–haul combinations. Wide-body aircraft operating on Short Haul flights exhibit substantially negative margins in the displayed results, whereas some of those aircraft types show positive margins on Long Haul routes. This raises an important planning question about the alignment of **aircraft capacity, flight distance, and route economics**.

![Long Haul Route KPI Matrix](assets/12_longhaul_route_kpis.png)

*Figure 12 — Long Haul KPI matrix by destination: RASK, Flight Hours, Load Factor, and PM.*

Even among Long Haul destinations, flight duration, seat occupancy, RASK, and PM differ. Haul length is therefore a useful first segmentation layer, but it should not replace a detailed destination-level analysis.

### 4.7. Seasonality — Monthly and Seasonal Demand and Profitability

![Load Factors by Month](assets/08_monthly_load_factor.png)

*Figure 08 — Average Load Factor by month.*

![Load Factor and Profit Trends by Route Category](assets/09_monthly_trends_by_haul.png)

*Figure 09 — Load Factor and Average Profit trends by haul category.*

The charts show higher Load Factors at the beginning and end of the year and lower values in the middle of the year, particularly **June–August**. A similar deterioration appears in average profit trends across the route categories.

![RASK by Season and LF/PM by Season](assets/10_season_summary.png)

*Figure 10 — RASK by Season and Load Factor/PM by Season.*

Comparing Low, Normal, Shoulder, and Peak seasons, Peak shows higher average RASK, Load Factor, and PM than Low. This suggests seasonality relates both to passenger volume and revenue quality, while many flight expenses must still be covered regardless of the season.

**FP&A implication:** A uniform annual capacity plan or revenue assumption may fail to reflect fluctuating demand. Seasonal planning should consider occupancy, fares, and cost efficiency together.

### 4.8. Break-even Load Factor and Full Flights That Still Lose Money

![Break-even Load Factor by Route Category](assets/13_belf_boxplot.png)

*Figure 13 — Python boxplot showing BELF distributions by Route Category.*

The boxplot shows that Break-even LF distributions differ between Long, Medium, and Short Haul. Short Haul has a higher median than Long Haul in the displayed chart; the dashed reference line represents an average LF of approximately **0.80**. This indicates that route categories have different break-even requirements under the BELF calculation used in the project.

![High LF but Loss Making Flights](assets/14_high_lf_loss.png)

*Figure 14 — Flights with `Load_Factor > 0.85` but `PM < 0`, grouped by Season and Route Category.*

Flights with Load Factors above 85% that are still unprofitable are concentrated in the Short Haul category, particularly in some seasons shown in the chart. This reinforces the LF vs PM finding: **selling more seats does not automatically generate profit if revenue per seat is insufficient to cover costs**.

### 4.9. Passenger Service Cost per Pax

![Passenger Service Cost per Pax Heatmap](assets/15_passenger_service_heatmap.png)

*Figure 15 — Heatmap of passenger service cost per Pax by Aircraft Type and Route Category.*

The notebook constructs this metric from Catering Cost, Handling Cost, and Passenger Service Cost and compares average values across Aircraft Type × Route Category combinations. The heatmap supports a closer examination of whether different aircraft and route configurations incur different average service expenses and which groups warrant deeper cost-driver analysis.

---

## 5. Python and Predictive Modeling

### 5.1. How Python Was Used

Python supports analyses that are more difficult to present with standard PivotCharts, including a BELF distribution boxplot, a chart of high-load-factor flights that still lose money, a passenger service cost heatmap, and model training to predict PM.

### 5.2. Predictive Modeling: Random Forest vs XGBoost

The notebook selects predictors, applies one-hot encoding to categorical variables, and performs an **80% / 20%** train/test split with `random_state=42`. Random Forest and XGBoost are tuned through `RandomizedSearchCV` and evaluated using RMSE, MAE, and R².

| Test metric | Random Forest | XGBoost |
|---|---:|---:|
| RMSE | 0.2101 | **0.2069** |
| MAE | 0.1591 | **0.1583** |
| R² | 0.7020 | **0.7111** |

![Random Forest and XGBoost Test Metrics](assets/17_model_metrics.png)

*Figure 17 — Model performance on the test set, as reported in the notebook.*

The two models perform similarly; XGBoost has slightly lower RMSE and MAE and a higher R² in this experiment. These figures describe a test-set modeling exercise, not an operational forecasting system already deployed by an airline.

### 5.3. Feature Importance

![Feature Importance Comparison](assets/16_feature_importance.png)

*Figure 16 — Top 15 features for Random Forest and XGBoost.*

`Route_Category_Short Haul` is among the most prominent features in both plots. Variables including `Flight_Hours`, `Load_Factor`, `Distance`, and `Aircraft_Capacity` also appear. The results suggest that route length, demand, and aircraft capacity characteristics contain useful information for predicting PM in the fitted models.

**Interpretation note:** Feature importance reflects a variable's contribution within a predictive model; it does not directly establish a causal effect on Profit Margin. Machine learning complements financial analysis rather than replacing knowledge of airline economics and operating constraints.

---

## 6. Key Findings & Strategic Recommendations

| Key Findings | Evidence & Insights | FP&A Recommendations |
|---|---|---|
| **1. Profitability is highly concentrated across routes.** | The network generated **575.48 million in profit**, but performance varied substantially. FRA, SIN, CDG, and HKG recorded strong margins, whereas CAI, AMM, JED, and RUH performed poorly. | **Grow & Review:** Protect the most profitable routes while reviewing revenue, costs, and flight frequency on underperforming routes. |
| **2. High Load Factor does not guarantee profitability.** | The LF vs PM scatter plot and flights with **LF > 85% that still incurred losses** show that seat occupancy alone does not determine profitability. | **Optimize Revenue Quality:** Monitor Yield, RASK–CASK Spread, and Ancillary Revenue/Pax rather than focusing only on passenger growth. |
| **3. Short-haul routes face substantial profitability pressure.** | Short Haul shows lower average margins, higher BELF, and numerous loss-making flights despite relatively healthy Load Factors. | **Improve Route Economics:** Review fares, cost per flight, schedule frequency, and aircraft suitability, with an emphasis on reducing CASK. |
| **4. Cost efficiency depends on more than fuel expenses.** | Fuel, Sales & Distribution, Overhead, and Depreciation account for large portions of total costs, while the cost mix differs across haul categories. | **Targeted Cost Optimization:** Assess distribution expenses, allocated overhead, and aircraft utilization; track CASK and Cost/Pax by route. |
| **5. Seasonality significantly affects financial performance.** | Load Factor and profitability decline during **June–August**, while Peak Season exhibits higher RASK and stronger margins. | **Dynamic Capacity Planning:** Adjust frequencies and offered capacity by season; link pricing strategy to monthly route-level profitability forecasts. |

### Management Implication

These findings indicate that **profit improvement is not simply a matter of carrying more passengers or reducing expenses**. Airlines must coordinate revenue management, cost efficiency, and capacity allocation. FP&A teams can use **route-level P&L, the RASK–CASK Spread, and Break-even Load Factor** to evaluate business scenarios and support management decisions.



---

## Conclusion

This project demonstrates that airline route profitability should be assessed using both financial and operational information. **Profit Margin is not determined by Load Factor alone**; differences in cost structure, aircraft type, route length, and seasonality can produce markedly different outcomes. RASK and CASK broaden the analysis beyond absolute profit to performance per available seat-kilometer.

The project's central value lies in its **Excel PivotTable-based FP&A workflow**: moving from a Financial Snapshot through Route Rankings, Cost Mix, Capacity Utilization, Unit Economics, and Seasonality, then turning the findings into management recommendations. Python supports advanced visualization and predictive modeling experiments, while sound decisions still require an understanding of route economics and business objectives.
