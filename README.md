::: {align="center"}
# Delhi Metro Operations & Revenue Analytics

### A 4-page Power BI dashboard exploring ridership, passenger demand, revenue, profitability, routes, and station-network patterns.

**Power BI · DAX · Power Query · Data Modeling · Data Visualization**
:::

------------------------------------------------------------------------

## Project Overview

**Delhi Metro Operations & Revenue Analytics** is an interactive Power
BI portfolio project designed to explore metro-trip activity from
operational, passenger-demand, financial, and network perspectives.

The report combines trip-level data with a separate station-master
dataset in a four-page dashboard. Users can filter by date, ticket type,
origin, destination, metro line, station layout, route, fare, and
remarks where relevant.

The workflow covers source-data inspection, data cleaning, calculated
metrics in DAX, date-based analysis, report design, and documentation.

> **Data-use note:** This is a portfolio/analytical exercise. The
> figures should not be interpreted as official Delhi Metro Rail
> Corporation (DMRC) operational or financial statistics unless the
> underlying source is independently verified as official. Revenue,
> cost, profit, and passenger figures are calculated from the supplied
> dataset and its assumptions.

## Dashboard Pages

  -----------------------------------------------------------------------
  Page                    Focus                   Main questions
  ----------------------- ----------------------- -----------------------
  1\. Executive Overview  High-level performance  How many passengers and
                                                  trips are represented?
                                                  What are the calculated
                                                  revenue, cost, profit,
                                                  and margin?

  2\. Passenger & Demand  Ridership and travel    How does demand vary
                          patterns                over time, across
                                                  weekdays, stations, and
                                                  ticket types?

  3\. Revenue &           Financial analysis      How do calculated
  Profitability                                   revenue, cost, and
                                                  profit vary by month,
                                                  distance band, and
                                                  ticket type?

  4\. Metro Network &     Station and route       Which origin stations
  Operations              exploration             and routes stand out,
                                                  and how is the station
                                                  master distributed by
                                                  line/layout?
  -----------------------------------------------------------------------

### Page 1 --- Executive Overview

**Filters:** Date range, Ticket Type, From Station, To Station.

**KPIs:** Total Passengers, Total Trips, Total Revenue, Total Profit,
Average Fare, Profit Margin.

**Visuals:** - Monthly Revenue Trend - Monthly Passenger Trend - Top 5
Origin Stations - Top 5 Routes by Revenue - Ticket Type Distribution

### Page 2 --- Passenger & Demand

**Filters:** Date range, Ticket Type, From Station, To Station, Remarks.

**KPIs:** Total Passengers, Passengers per Trip, Average Daily
Passengers, Peak Daily Passengers, Average Distance (km).

**Visuals:** - Monthly Passenger Demand - Passengers by Day of Week -
Top 5 Origin Stations - Top 5 Destination Stations - Passenger
Contribution by Ticket Type

### Page 3 --- Revenue & Profitability

**Filters:** Date range, Ticket Type, From Station, To Station, Route,
Fare range.

**KPIs:** Total Revenue, Total Cost, Total Profit, Profit Margin,
Revenue per Passenger, Revenue per Trip.

**Visuals:** - Revenue vs Cost by Month - Profit Margin by Distance
Band - Total Revenue by Distance Band - Profit Margin by Month Year -
Profit Driver Analysis (Decomposition Tree)

### Page 4 --- Metro Network & Operations

**Filters:** Date range, Line, Station Layout, From Station, To Station.

**KPIs:** Active Stations, Total Metro Lines, Total Routes, Average Trip
Distance (km), Longest Trip Distance (km), Top Origin Station.

**Visuals:** - Delhi Metro Station Network map - Top 5 Origin Stations
by Average Trip Distance - Top Route by Passenger Volume - Station
Records by Layout

The map uses station-master latitude/longitude fields. Station-layout
composition is calculated from station-master records, while trip-origin
and route visuals use the trip table.

------------------------------------------------------------------------

## Data Sources & Structure

The report uses two source datasets. Keep raw source files unchanged and
store prepared data separately.

### 1. Trip data

Suggested filename: `01_Trip_Data_Raw.csv`\
Prepared Power BI table: `01_Trip_Data_Cleaned`

The cleaned trip table contains **150,000 rows** and these fields:

  -----------------------------------------------------------------------
  Column                              Description
  ----------------------------------- -----------------------------------
  `TripID`                            Identifier for a trip record

  `Date`                              Trip date; the report covers
                                      2022--2024

  `From_Station`                      Origin station

  `To_Station`                        Destination station

  `Distance_km`                       Trip distance in kilometres

  `Fare`                              Fare value provided in the dataset

  `Cost_per_passenger`                Cost value per passenger provided
                                      in the dataset

  `Passengers`                        Passenger count associated with the
                                      record

  `Ticket_Type`                       Ticket category

  `Remarks`                           Context/remark category
  -----------------------------------------------------------------------

### 2. Station master

Suggested filename: `02_Station_Master_Raw.csv`

Fields include `Station ID`, `Station Name`, `Distance from Start (km)`,
`Line`, `Opening Date`, `Station Layout`, `Latitude`, and `Longitude`.

The source station master contains **285 records**. The same station
name can occur more than once when it represents different line-specific
records. Therefore, station name should not automatically be treated as
a unique key. The report's distinct station-name KPI is 283; the layout
donut counts station records in its visual's filter context.

### Suggested repository structure

``` text
Delhi-Metro-Analytics/
├── 01_Raw_Data/
│   ├── 01_Trip_Data_Raw.csv
│   └── 02_Station_Master_Raw.csv
├── 02_Cleaned_Data/
│   └── 01_Trip_Data_Cleaned_150K.csv
├── 03_PowerBI/
│   └── Delhi_Metro_Operations_Revenue_Analytics.pbix
├── 04_Documentation/
│   ├── README.md
│   ├── PROJECT_ARCHITECTURE.md
│   ├── PROJECT_PROCESS.md
│   ├── DATA_DICTIONARY.md
│   ├── DAX_MEASURES.md
│   ├── PROJECT_ROADMAP.md
│   └── CHANGELOG.md
└── 05_Screenshots/
    ├── page-1-executive-overview.png
    ├── page-2-passenger-demand.png
    ├── page-3-revenue-profitability.png
    └── page-4-metro-network-operations.png
```

*These are suggested repository names. Adjust paths to match the files
actually committed.*

------------------------------------------------------------------------

## Data Preparation & Quality Notes

The source data is kept separate from the cleaned/analytical version.
Preparation rules used or documented for the trip dataset include:

1.  Trim leading/trailing whitespace from text fields, especially
    station names.
2.  Standardize date values and convert numeric fields to suitable data
    types.
3.  Treat blank text values as missing before applying replacements.
4.  Replace missing `Ticket_Type` values with `Unknown`.
5.  Replace missing `Remarks` values with `Not Specified`.
6.  Impute missing `Passengers` using a median-based approach: first by
    `Ticket_Type` and `Remarks` where possible, then by `Ticket_Type`,
    and finally by the overall median.
7.  Check duplicate trip records/IDs rather than deleting rows
    automatically without validation.
8.  Preserve the 150,000-row analytical table; disclose passenger
    imputation because it introduces estimated values.

For the station master, retain the original 285 records as source data.
Repeated station names can represent different station/line records, and
13 records have a distance-from-start value of zero. Do not change these
zero values automatically without source verification.

### Interpretation limits

-   The dashboard describes the supplied dataset, not necessarily
    real-world DMRC performance.
-   `Total Revenue`, `Total Cost`, `Total Profit`, and `Profit Margin`
    are derived metrics based on the supplied fare, passenger, and cost
    fields.
-   Passenger imputation can affect totals and averages.
-   Station names are not unique across all station-master records, so a
    direct many-to-one relationship on `Station Name` is not valid
    without a proper key.
-   The active date relationship connects `Dim_Date[Date]` to
    `01_Trip_Data_Cleaned[Date]`. Station-master visuals use the station
    master directly; do not assume date/trip filters propagate to
    station master unless a valid relationship is implemented.
-   This project is for analytics demonstration and should not be used
    for transport planning, budgeting, or operational decisions without
    validating the source and metric definitions.

------------------------------------------------------------------------

## Data Model

### Tables

-   **`01_Trip_Data_Cleaned`** --- central trip-level fact table for
    passenger, route, fare, cost, and date analysis.
-   **`Dim_Date`** --- calendar table for time-based slicing and
    month/day analysis.
-   **`02_Station_Master_Raw`** --- station reference data for line,
    layout, opening date, coordinates, and station attributes.
-   **`Dim_Station`** --- a helper/dimension query explored for station
    analysis. Since station names can repeat across lines, do not relate
    it to the trip fact table on station name unless the key is unique
    at the chosen grain.

### Relationship design

The confirmed date relationship is:

``` text
Dim_Date[Date]  (1) ──────── (*)  01_Trip_Data_Cleaned[Date]
```

Use **single-direction filtering from `Dim_Date` to the trip table**.

The station master is not automatically connected to the trip table by
station name because the station master contains duplicate names. A
robust future model can create a unique station key and separate
role-playing dimensions for origin and destination:

``` text
Dim_Date ─────► Fact_Trips ◄───── Dim_FromStation
                         ◄─────── Dim_ToStation

Dim_Station_Master (station attributes / coordinates)
```

Implement station relationships only after creating and validating a
reliable key. Avoid an accidental many-to-many relationship or
bidirectional filtering merely to make the model diagram look connected.

------------------------------------------------------------------------

## Key DAX Measures

The following are the core calculations used by the report. Check
measure names against the current PBIX if names were changed during
formatting.

``` dax
Total Trips =
COUNTROWS('01_Trip_Data_Cleaned')

Total Passengers =
SUM('01_Trip_Data_Cleaned'[Passengers])

Total Revenue =
SUMX(
    '01_Trip_Data_Cleaned',
    '01_Trip_Data_Cleaned'[Fare] *
    '01_Trip_Data_Cleaned'[Passengers]
)

Total Cost =
SUMX(
    '01_Trip_Data_Cleaned',
    '01_Trip_Data_Cleaned'[Cost_per_passenger] *
    '01_Trip_Data_Cleaned'[Passengers]
)

Total Profit =
[Total Revenue] - [Total Cost]

Average Fare =
AVERAGE('01_Trip_Data_Cleaned'[Fare])

Passengers per Trip =
DIVIDE([Total Passengers], [Total Trips])

Revenue per Passenger =
DIVIDE([Total Revenue], [Total Passengers])

Revenue per Trip =
DIVIDE([Total Revenue], [Total Trips])

Profit Margin =
DIVIDE([Total Profit], [Total Revenue])

Average Daily Passengers =
AVERAGEX(
    VALUES('Dim_Date'[Date]),
    [Total Passengers]
)

Peak Daily Passengers =
MAXX(
    VALUES('Dim_Date'[Date]),
    [Total Passengers]
)

Average Distance =
AVERAGE('01_Trip_Data_Cleaned'[Distance_km])
```

### Derived columns

**Route**

``` dax
Route =
IF(
    '01_Trip_Data_Cleaned'[From_Station]
        = '01_Trip_Data_Cleaned'[To_Station],
    BLANK(),
    '01_Trip_Data_Cleaned'[From_Station]
        & " → " &
    '01_Trip_Data_Cleaned'[To_Station]
)
```

**Distance Band**

``` dax
Distance Band =
SWITCH(
    TRUE(),
    '01_Trip_Data_Cleaned'[Distance_km] <= 5, "0–5 km",
    '01_Trip_Data_Cleaned'[Distance_km] <= 10, "5–10 km",
    '01_Trip_Data_Cleaned'[Distance_km] <= 15, "10–15 km",
    '01_Trip_Data_Cleaned'[Distance_km] <= 20, "15–20 km",
    "20+ km"
)
```

A numeric sort column keeps distance bands in ascending order. The date
dimension also includes day-name/day-number fields for weekday sorting.

### Financial metric definitions

-   **Revenue** = `Fare × Passengers`, summed across trip records.
-   **Cost** = `Cost_per_passenger × Passengers`, summed across trip
    records.
-   **Profit** = `Revenue − Cost`.
-   **Profit Margin** = `Profit ÷ Revenue`.
-   **Passengers per Trip** = `Total Passengers ÷ Total Trips`.
-   **Revenue per Passenger** = `Total Revenue ÷ Total Passengers`.
-   **Revenue per Trip** = `Total Revenue ÷ Total Trips`.

These formulas follow the supplied field definitions. Validate that fare
and cost are genuinely per-passenger/per-trip values before interpreting
the results as real financial performance.

------------------------------------------------------------------------

## Design & User Experience

The report uses a consistent **Metro Control Center × Premium
Analytics** visual language:

-   Dark navy canvas: `#070B14`
-   Dark card surfaces: `#0D1624`
-   Primary blue: `#2196F3`
-   Passenger/cyan accents: `#22D3EE`
-   Revenue/amber accents: `#F59E0B`
-   Profit/positive accents: `#22C55E`
-   Brand red accent: `#E31B23`
-   Secondary purple: `#A855F7`
-   Typography: Segoe UI
-   Page-specific metro photography with dark gradients to maintain text
    contrast
-   Shared navigation and consistent slicer/KPI styling across all four
    pages

The four backgrounds intentionally differ by page: aerial metro/city
view, crowded platform, long-exposure metro lights, and a
metro-station/train scene. This keeps the visual system cohesive without
making every page look identical.

------------------------------------------------------------------------

## How to Use the Report

1.  Open the `.pbix` file in Power BI Desktop.
2.  Use the page navigator at the top to move between the four pages.
3.  Select slicer values to filter visuals on the current page.
4.  Hover over charts for tooltips and select chart elements to
    cross-highlight related visuals where supported.
5.  Use the date range to inspect periods between 2022 and 2024.
6.  For financial analysis, read revenue, cost, profit, and margin
    together and consider the data/imputation limitations.

## Tools & Skills Demonstrated

-   **Power BI Desktop** --- report design, interactive visuals,
    slicers, page navigation
-   **Power Query** --- data preparation, text cleanup, type conversion,
    missing-value treatment
-   **DAX** --- measures, calculated columns, date-based analysis,
    profitability calculations
-   **Data modeling** --- date dimension, fact/dimension concepts,
    relationship cardinality and filter direction
-   **Data visualization** --- KPI cards, time-series charts, ranked bar
    charts, route analysis, decomposition tree, map and layout
    composition
-   **Documentation** --- data dictionary, architecture, cleaning
    process, measure definitions, roadmap and changelog

## Current Status

-   [x] Four dashboard pages built
-   [x] Main KPI measures and calculated columns created
-   [x] Date dimension connected to the trip table
-   [x] Page-specific backgrounds and consistent dark visual theme
    applied
-   [x] Page navigation and interactive slicers added
-   [x] Data-cleaning decisions documented
-   [ ] Validate dataset provenance before making real-world DMRC claims
-   [ ] Recheck that every chart title matches its field/measure and
    aggregation
-   [ ] Add final page screenshots to `05_Screenshots/`
-   [ ] Validate station keys and implement a proper origin/destination
    dimension model if deeper station filtering is required
-   [ ] Publish the final `.pbix` and supporting data/docs to GitHub

## Future Enhancements

1.  Validate and document the provenance of both datasets.
2.  Build a unique station key and robust origin/destination dimension
    model.
3.  Add automated data-quality checks and an explicit imputation flag
    for estimated passenger values.
4.  Expand the workflow with Python for exploratory data analysis, SQL
    for query-based analysis, and Excel for complementary reporting.
5.  Add refresh instructions, a reproducible cleaning script, and
    verified source citations.

## Repository Notes

This README describes the current Power BI project. Update file paths,
data-source attribution, screenshots, and model relationships to match
the exact contents of the published repository. Do not commit
confidential or restricted data.

------------------------------------------------------------------------

::: {align="center"}
**Delhi Metro Operations & Revenue Analytics**\
*An interactive BI portfolio project*
:::
