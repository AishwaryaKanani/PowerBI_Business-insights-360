# Business Insights 360 – Power BI Project  
Live Dashboard: [_Link_](https://bit.ly/4pggTpM)

Presentation Video: [_Link_](https://www.linkedin.com/posts/aishwaryakanani_powerbi-dataanalytics-businessintelligence-activity-7400879410083434496-ARJ_?utm_source=share&utm_medium=member_desktop&rcm=ACoAADqnB8gB_x1vyEg35NlTzQ1ToxAC6jNkLvg)

**By Codebasics**

The Business Insights project is a part of the **Codebasics Data Analytics Bootcamp**.

This is an **end-to-end Data Analysis and Power BI project** which is based on an imaginary company called **AtliQ Hardware**.

---

## About AtliQ Hardware

AtliQ Hardware manufactures and sells hardware like **PC, Mouse, Printers etc** to multiple companies across the world.  
AtliQ’s customers are companies like **Croma, Amazon, Neptune, Staples, Walmart etc.**

These customers are of two types:
- **Physical Stores**
- **E-commerce platforms**

---

## Problem Statement

AtliQ Hardware is struggling to do good business in **Latin America**.

So far all the decisions that AtliQ took have been based on some **surveys and intuitions**.  
The company was doing some analysis using **MS Excel files** because of limited data.

Now that the company has grown and has plenty of data to analyse, the management has decided to hire a **Data Analyst**.  
The management wants Data Analysts to utilise this data to make **accurate and informed decisions**.

---

## Management’s Dashboard Requirements

The management wants to see these reports in the **Power BI Dashboard**:

### Finance View
- Shows **Profit and Loss statements** across different products, markets, customers etc.

### Sales View
- Displays **top-performing and bottom-performing customers** with different key metrics.

### Marketing View
- Similar data as Sales View but **product based instead of customers**.

### Supply Chain
- Reliability and accuracy to better understand the **supply chain performance**.

### Executive View
- Integrated view of key insights for executives.

This Power BI project is not just a project but a **course created with real-life business scenarios**, like:
- Recorded business meetings with stakeholders  
- Feedback after every design is created and shared  
- Changing and adding features based on stakeholder feedback  
- Creating reports that save time and provide consolidated key metrics  

---

## Project Execution

### Step – 1
- Loaded the data into **MySQL Database** and connected it to **Power BI**.

### Step – 2
- Reviewed and deleted the **default relationships** created by Power BI.
- Created required **dimension tables** in Power Query.

### Step – 3
- Performed **data validation** using tables in Power BI and matched values with source data.

### Step – 4
- **Data Transformation**
- Created a **Last Sales Month Reference table** which is dynamic and updates after every sale.

### Step – 5
- Created **calculated columns** in Power Query like `fiscal_year` and merged tables.

### Step – 6
- **Data Modelling**
- Used **Star Schema** where all dimension tables were connected with fact tables.

### Step – 7
- Created **40+ calculated measures using DAX**.
- Verified results using **MySQL or Excel**.

### Step – 8
- Optimized the report to **reduce file size**, making it easier to share and access.

---

## Building The Dashboard

Created **5 different report views**, each serving different stakeholders.

### Home Page
- Navigation to all views
- Summary of each page for quick access
![_Home_page_](https://github.com/AishwaryaKanani/PowerBI_AtliQ-Mart-Supply-Chain-Analysis/blob/main/Resources/Data_model.png)
---

## Finance View

- Shows **P & L statements**
- Top-performing and bottom-performing products and customers
- Product segment performance across regions
- **Year-on-Year comparison** of P & L in a single view

A button displays:
- **Net Sales vs Last Year**
- **Net Sales vs Target**

This helps in **better decision-making**.

---

## Sales View

- Helps the sales team drill down performance by:
  - Product
  - Customer
  - Region
- Includes the same filters as Finance View for in-depth analysis.

---

## Marketing View

Contains:
- Gross Margin %
- Net Profit %
- Operational Expenses
- Cost of Goods Sold

Helps marketing teams:
- Decide marketing budgets
- Identify potential customers and markets
- Understand growth opportunities

---

## Supply Chain View

- Helps manage inventory and delivery performance
- Uses historical data to forecast demand

Example Insight:
- Forecast accuracy in Q1 2020 was **80.26%**
- Compared to **85.92% in Q1 2019**
- **Accessories** segment suffered the most (**51.50%**)

---

## Executive View

A **consolidated report** with KPIs like:
- NS
- RC%
- GM%
- NP%
- Forecast Accuracy %
- Market Share
- Top products and customers

This view:
- Saves time for senior stakeholders
- Provides high-level insights without deep dives

---

## Tools Used In Project

- MS Excel  
- MySQL  
- Power BI  
- Power BI Service  
- DAX Studio  

---

## Learnings From Project

- Power BI
- Data Modelling
- Dashboard Creation & Designing
- Project Charter
- Stakeholder Mapping
- P&L Statement Analysis
- Business metrics like:
  - Profit %
  - Gross Margin %
  - Forecast %
  - Period-over-period comparison

The learning was not limited to Power BI.  
The project involved real **business decision-making scenarios**, comparing performance across:
- Products
- Categories
- Markets
- Customers

---

## Power BI Features Learned & Used

- DAX Formulas
- Data Modeling
- Table Creation
- Tooltips
- Bookmark-based switches
- Dynamic titles
- Conditional formatting
- Dynamic Last Refresh Date
- Multiple department-specific views in one report

---

## DAX Formulas Learned & Used

```DAX
ABS Error =
SUMX(DISTINCT(dim_date[date]),
SUMX(DISTINCT(dim_product[product_code]), ABS([Net Error]))
)

ABS Error % = DIVIDE([ABS Error], [Forecast Qty], 0)

ABS Error LY = CALCULATE([ABS Error],SAMEPERIODLASTYEAR(dim_date[date]))

Ads & Promotions $ = SUM(‘fact_actuals_estimates'[ads_promotions])

Atliq MS % = CALCULATE([Market Share %], marketshare[manufacturer]=”atliq”)

BM Message =
IF([NS BM $] = BLANK() || [GM % BM] = BLANK() || [NP % BM] = BLANK(),
“BM Target is not available for the selected filters”, “”)

Customer / Product Filter Check =
ISCROSSFILTERED(dim_product[product]) || ISFILTERED(dim_customer[customer])

Forecast Accuracy % =
IF([ABS Error %]<>BLANK(), 1 – [ABS Error %], BLANK())

Forecast Accuracy % LY =
CALCULATE([Forecast Accuracy %], SAMEPERIODLASTYEAR(dim_date[date]))

Forecast Qty =
VAR lsalesdate = MAX(LastSalesMonth[LastSalesMonth])
RETURN
CALCULATE(SUM(fact_forecast_monthly[forecast_quantity]),
fact_forecast_monthly[date]<=lsalesdate)

Freight Cost $ = SUM(fact_actuals_estimates[Freight_cost])

GS $ = SUM(fact_actuals_estimates[gross_sales_amount])

Last Sales Month Home =
“Sales Data Loaded Until : ” & FORMAT(MAX(LastSalesMonth[LastSalesMonth]), “MMM YY”)

Manufacturing Cost $ = SUM(fact_actuals_estimates[manufacturing_cost])

Market Share % =
DIVIDE(SUM(marketshare[sales_$]),
SUM(marketshare[total_market_sales_$]), 0)

Net Error = [Forecast Qty]-[Sales Qty]

Net Error % = DIVIDE([Net Error],[Forecast Qty],0)

Net Error LY = CALCULATE([Net Error],SAMEPERIODLASTYEAR(dim_date[date]))

Net Profit % = DIVIDE([Net Profit $],[NS $],0)

Net Profit % LY =
CALCULATE([Net Profit %], SAMEPERIODLASTYEAR(dim_date[date]))

Net Profit $ = [GM $]+[Operational Expense $]

NIS $ = SUM(fact_actuals_estimates[net_invoice_sales_amount])

NP % BM =
SWITCH(TRUE(),
SELECTEDVALUE(‘Set BM'[ID])=1, [Net Profit % LY],
SELECTEDVALUE(‘Set BM'[ID])=2, [NP Target %])

NP Target % =
DIVIDE([NP Target $], SUM(NsGmTarget[np_target]), 0)

NP Target $ = SUM(NsGmTarget[np_target])

NS $ = SUM(fact_actuals_estimates[net_sales_amount])

NS $ LY = CALCULATE([NS $], SAMEPERIODLASTYEAR(dim_date[date]))

NS BM $ =
SWITCH(TRUE(),
SELECTEDVALUE(‘Set BM'[ID])=1,[NS $ LY],
SELECTEDVALUE(‘Set BM'[ID])=2,[NS Target $])

NS Target $ =
VAR tgt = SUM(NsGmTarget[ns_target])
RETURN IF([Customer / Product Filter Check], BLANK(), tgt)

Operational Expense $ =
([Ads & Promotions $]+[Other Operational Expense $])*-1

Other Cost $ = SUM(fact_actuals_estimates[other_cost])

Other Operational Expense $ =
SUM(‘fact_actuals_estimates'[other_operational_expense])

Performance Visual Title =
[Selected P & L Row] & ” Performance Over Time”

Post Invoice Deduction $ =
SUM(fact_actuals_estimates[post_invoice_deductions_amount])

Post Invoice Other Deduction $ =
SUM(fact_actuals_estimates[post_invoice_other_deductions_amount])

Pre Invoice Deduction $ = [GS $] – [NIS $]

Quantity = SUM(fact_actuals_estimates[Qty])

RC % =
DIVIDE([NS $],
CALCULATE([NS $],ALL(dim_market), ALL(dim_customer), ALL(dim_product)))

Risk =
IF([Net Error]>0,”EI”, IF([Net Error]<0, “OOS”, BLANK()))

Sales Qty =
CALCULATE([Quantity],
fact_actuals_estimates[date]<=MAX(LastSalesMonth[LastSalesMonth]))

Sales Trend Title =
“NS & GM % For ” & SELECTEDVALUE(dim_customer[customer])

Selected P & L Row =
IF(HASONEVALUE(‘P & L Rows'[Description]),
SELECTEDVALUE(‘P & L Rows'[Description]), “Net Sales”)

Top / Bottom N Title =
“Top / Bottom Products & Customers By ” & [Selected P & L Row]

Total COGS $ =
‘Key Measure'[Freight Cost $] +
‘Key Measure'[Manufacturing Cost $] +
‘Key Measure'[Other Cost $]

Total Post Invoice Deduction =
‘Key Measure'[Post Invoice Deduction $] +
‘Key Measure'[Post Invoice Other Deduction $]
