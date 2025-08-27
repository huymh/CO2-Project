# ⛽ National CO2 Emissions from Fossil Fuels and Cement Production

## 📰 Overview
This project is an interactive Power BI dashboard that visualizes global and national CO2 emissisions by country and year. It was built to highlight trends, compare nations, and explore historical emission patterns from 1751 to 2020.

## 💡 Highlights
- Interactive filters for country, year, fuel type
- Global & country level views
- Historical trends with dynamic visuals
- Encorporates DAX for calculated measures

## SQL Query
Within Microsoft SQL Server Management Studio, each nation's cumulative and average fossil fuel emissions amount, starting year, ending year, and total years of emissions was queried using the following T-SQL query.
```sql
-- cumulative and average FFE, starting and ending Years, total years by country
-- sorted by cumulative and average FFE descending

SELECT
	country,
	ffe_cumulative,
	ffe_cumulative / years_of_ffe AS avg_ffe_per_year,
	min_year,
	max_year,
	years_of_ffe
FROM(
	SELECT                                                    -- Outer most subquery : calculate years of ffe
		*,
		max_year - min_year AS years_of_ffe
	FROM(
		SELECT                                                -- Inner most subquery : calculate cumulative, start year, end year
			Country,
			SUM(Total) AS ffe_cumulative,
			MIN(Year) AS min_year,
			MAX(Year) AS max_year
		FROM dbo.ffe
		GROUP BY COUNTRY) AS cumulative) AS total_years
WHERE years_of_ffe <> 0
ORDER BY
	ffe_cumulative DESC,
	avg_ffe_per_year DESC;
```
### Result
<img width="607" height="382" alt="b6a0cb368c71b29061261ed6ce18a625" src="https://github.com/user-attachments/assets/29ae375c-f501-4889-878f-73a8ddf16c68" />


This query was imported into Power BI to streamline the dashboard development process.

## 📊 Data
[National CO2 emissions from fossil fuels and cement manufacture](https://rieee.appstate.edu/projects-programs/cdiac/)

## 🛠 Tools Used
- Power BI Desktop : dashboard creation
- Microsoft SSMS : custom SQL queries
- DAX : calculations and measures

## 🔎Preview
<img width="1544" height="871" alt="co2_preview" src="https://github.com/user-attachments/assets/4104454b-cd84-4a58-be9d-3111fd3bb9e6" />

