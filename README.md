# Budapest Schools — Geospatial Data Quality Analysis

*Extracting, cleaning, and visualizing OpenStreetMap data in Power BI*

**Tools:** Overpass Turbo (data extraction) · Oracle SQL / APEX (storage & analysis) · Power BI (visualization)

## Goal

Extract, clean, and analyze publicly available geospatial data (OpenStreetMap) on schools in Budapest, with a focus on **data quality assessment** and visualization.

## Process

1. **Data extraction** — Queried all `amenity=school` locations within Budapest's administrative boundary via Overpass QL, retrieving both point and area-based entries. Result: **526 records** (119 nodes, 407 ways).
2. **Table design & load** — Designed a 10-column `SCHOOLS_RAW` table in Oracle SQL, deliberately excluding low-value fields identified during data profiling. Loaded via APEX Data Load Wizard: **526/526 rows, 0 errors**.
3. **Completeness analysis** — SQL-based, field-by-field completeness check (name: 95.8%, address fields: ~89–91%). Found that incompleteness tends to cluster on the same records rather than being independently distributed.
4. **Data quality flagging** — Instead of deleting incomplete records, added a `data_quality_flag` column and classified every record as `complete`, `needs_review`, or `low_quality` — preserving all data for flexible downstream use.
5. **District-level aggregation** — Parsed district numbers from postcodes to analyze school distribution across Budapest's 23 districts.
6. **Power BI dashboard** — Built an interactive dashboard combining a color-coded map, a district bar chart, and a data-quality pie chart, all cross-filtered.

## Key Findings

- **89.5%** of records (471) were fully complete; **7.98%** needed review; **2.47%** were low quality.
- District **XI (43 schools)** and **XIV (39 schools)** have the most schools; District XXIII has the fewest (4).
- Data incompleteness followed identifiable patterns (minimally tagged entries vs. missing address-only records) rather than being random — suggesting it's tied to how different contributors add data to OSM.

## Lessons Learned

- Flagging instead of deleting incomplete data keeps a dataset auditable and usable, letting downstream analysis include or exclude records as needed.
- Visualizing data quality itself (not just the analysis results) is important — it makes a dataset's limitations transparent to anyone using it.

## Full Documentation

The complete step-by-step process (with all screenshots and SQL queries) 
is available here: [Project_documentation_EN.docx](Project_documentation_EN.docx)
