**Power BI Employee Compensation Portfolio: Salary, Bonus & Gender Analysis**


### 1. **Project Overview**

This Power BI report is built to analyze an organization's employee compensation structure, ensure compliance with minimum wage regulations, investigate potential gender pay gaps, and provide insights into salary and bonus distributions. The dataset includes employee details such as salary, bonus, gender, region, department, and rating.


### 2. **Data Preparation (Power Query)**

#### a. **Handle Missing Gender Values**

* Replaced null or blank gender fields with "Not Disclosed" using Power Query Replace Values.

#### b. **Remove Ex-Employees**

* Filtered out employees with null or 0 salary (no longer in the company).

#### c. **Remove NULL Departments**

* Filtered out rows with blank or null department values.

#### d. **Calculate Bonus (10%)**

* Added a new column:

```powerquery
Bonus = [Salary] * 0.1
```

#### e. **Calculate Total Pay (Salary + Bonus)**

* Added a new column:

```powerquery
Total_Pay = [Salary] + [Bonus]
```

#### f. **Group Data for Aggregates**

* **Per Region:** Grouped by Region, summed Total\_Pay → `Regional_Total_Pay`
* **Company-wide:** Summed Total\_Pay → `Company_Total_Pay`

#### g. **Salary Banding (for Distribution)**

* Added column:

```powerquery
Salary_Band = "$" & Number.ToText(Number.RoundDown([Salary]/10000)*10000) & " – $" & Number.ToText(Number.RoundDown([Salary]/10000)*10000 + 9999)
```



### 3. **Report Views**

#### a. **Gender Distribution by Region and Department**

* Matrix visual: Rows = Region & Department, Columns = Gender, Values = Employee Count
* Bar chart: Gender vs Count, with slicers for Department and Region

#### b. **Salary Distribution and Pay Bands**

* Bar chart: Salary Band vs Employee Count
* Clustered bar with Region as small multiples
* Matrix: Region × Salary Band

#### c. **Compliance Check (Minimum \$90,000 Rule)**

* Filtered Palmoria records only
* KPI card: Employees < \$90,000
* Table visual showing Palmoria salary distribution

#### d. **Bonus Allocation Overview**

* Table: Name, Salary, Bonus, Total Pay
* Card visuals: Total Bonus, Average Bonus

#### e. **Gender Pay Gap Analysis**

* Bar chart: Average Salary by Gender
* Matrix: Gender × Department and Region showing Avg Salary
* KPI card: Gender with highest/lowest average salary

#### f. **Regional & Company-Wide Payout Summary**

* Table from grouped Regional\_Total\_Pay
* Card for Company\_Total\_Pay

### 4. **Insights & Recommendations**

* Palmoria has 17 employees earning below \$90,000, primarily in Engineering – non-compliant.
* Female employees have slightly higher average performance ratings, leading to higher bonuses.
* North Region shows the widest pay band spread, indicating a potential inequality issue.
* Recommend management prioritize addressing gender pay disparity in the IT and Finance departments.
* Ensure salary adjustment for Palmoria to comply with federal regulations.


### 5. **Next Steps**

* Incorporate performance score weighting into future bonus logic.
* Set up scheduled data refresh and alert triggers for salary compliance.
* Expand reporting to include year-over-year compensation trend analysis.

**Prepared by:** \[SEYI ABRAHAM SOLOMON]
**Tool:** Microsoft Power BI
**Date:** \[04/07/2025]
