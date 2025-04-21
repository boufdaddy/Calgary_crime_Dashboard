# Calgary Crime Dashboard (Power BI Project)

This Power BI project analyzes crime data in Calgary from 2018 to 2024, showcasing trends, hotspots, and category-based distributions. Built using open data from the [City of Calgary Open Data Portal](https://data.calgary.ca), the dashboard aims to provide a transparent, data-driven view of safety across communities.

---

## 📊 Dashboard Features

- **Total Crimes:** 216,790 incidents from 2018–2024
- **Highest Crime Month:** September 2019
- **Most Affected Community:** Beltline
- **ArcGIS Heatmap** of community-level crime distribution
- **Category-wise Crime Bar Chart** by year
- **Trend Line:** Total Crimes per year
- **Filters:** Year-Month, Community, Crime Category

---

## 📌 Key Measures (DAX)

```DAX
Total Crimes = COUNTROWS('Community_Crime_Statistics')

Crimes Per Year = 
CALCULATE([Total Crimes], 
    ALLEXCEPT('Community_Crime_Statistics', 'Community_Crime_Statistics'[Year])
)

Crimes Per Month = 
CALCULATE([Total Crimes], 
    ALLEXCEPT('Community_Crime_Statistics', 'DateTable'[MonthYearLabel])
)

Highest Crime Month =
CALCULATE(MAX('DateTable'[MonthYearLabel]), 
    TOPN(1, VALUES('DateTable'[MonthYearLabel]), [Total Crimes], DESC)
)

Most Affected Community = 
CALCULATE(MAX('Community_Crime_Statistics'[Community]), 
    TOPN(1, VALUES('Community_Crime_Statistics'[Community]), [Total Crimes], DESC)
)
