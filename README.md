# LoanPortfolioFinancialAnalysis
It contains a Power BI dashboard designed to provide a comprehensive financial status and risk assessment of a loan portfolio.
## 🎯 Project Goal

The primary goal of this dashboard is to enable financial institutions, risk analysts, and portfolio managers to:
* Monitor overall loan performance and financial health.
* Identify trends in funded amounts and loan status over time.
* Assess credit risk across different borrower segments (e.g., credit grades, home ownership).
* Understand the distribution of loan purposes and their associated funding.
* Gain geographical insights into loan origination and performance.

📊 Dashboard Overview : The dashboard is structured into two main pages to deliver a holistic view:Page 1: Executive Summary & Performance OverviewKey Performance Indicators (KPIs): Displays total funded amount, loan count, average interest rate, and the crucial $14.17\%$ Default Rate.Time Series Analysis: Tracks funded amounts and loan status changes over time using the dedicated Dim_Date table.Status Distribution: Pie/Donut charts show the breakdown of loans by Loan_Status (e.g., Fully Paid, Charged Off, Current).Slicer Panel: Allows users to filter the entire view by Credit Grade (Tile), Loan Term (Tile), and Home Ownership Status (Dropdown).

Page 2: Risk and Segmentation Deep Dive
Risk vs. Pricing: A visual hierarchy that enables drill-down from Credit_Grade to Credit_Sub_Grade to verify if the average Interest Rate aligns with the assigned risk tier (e.g., C5 pays more than C1).

Geographic Risk: A Choropleth Map visualizing Loan Count or Total Funded Amount shaded by State_Code to identify regional concentrations of risk/volume.

Borrower Profiling: A Scatter Plot of Average DTI vs. Average Annual Income (sized by Total Loan Amount) to pinpoint high-risk or high-volume borrower clusters.

Technical and Modeling Details
Data Source: Synthetic bank loan data (split across two files: Finance_1.csv and Finance_2.csv).

Data Integration (Power Query): The two source files were merged using an Inner Join on the unique Loan_ID to create a single, efficient Fact_Loans table.

Data Cleaning: Comprehensive cleaning steps were performed on critical fields, including:

Interest_Rate: Removed the % symbol and converted to Decimal Number.

Loan_Term: Extracted the numerical value and converted to a Whole Number.

Handled nulls in Months_Since_Last_Delinquency and Employment_Length.

Data Model (Star Schema): A high-performance Star Schema was implemented:

Fact Table: Fact_Loans

Dimension Tables: Dim_Date (created using CALENDARAUTO()) and Dim_Purpose.

DAX Measures: Key explicit measures were created for accuracy and performance, including the complex Default Rate calculation: CALCULATE(COUNTROWS(Fact_Loans), Fact_Loans[Loan_Status] IN {"Charged Off"}) / COUNTROWS(Fact_Loans)

💡 Conclusions : The analysis derived from this dashboard leads to several actionable conclusions and clear paths for future development:Key Findings:Significant Default Risk: The portfolio exhibits a baseline $14.17\%$ Default Rate, underscoring the necessity of continuous risk monitoring.Pricing Validation: The drill-down feature confirmed that interest rate pricing is generally aligned with the granular Credit_Sub_Grade tiers, indicating a functioning underwriting model.Geographic Focus: The Choropleth map identifies specific states that contribute disproportionately to total funding volume, highlighting where risk concentration efforts should be focused.

Future Enhancements:
Recovery Analysis: Implement a metric to analyze the efficiency of collection efforts (Recoveries vs. Charged Off Amount).

Industry Segmentation: Clean the messy Employee_Title column to create a Dim_Industry table for analyzing default rates across different employment sectors.

What-If Analysis: Integrate DAX parameters to allow analysts to simulate the impact of changing interest rates or underwriting standards on the overall Default Rate.
