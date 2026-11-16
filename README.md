# Delhi Metro Operations & Revenue Analytics

An interactive **4-page Power BI dashboard** exploring passenger demand, revenue, profitability, routes, and metro network patterns.

<p align="center">
  <img src="Images/Delhi_Metro_full_logo.png" alt="Delhi Metro logo" width="260">
</p>

## Dashboard Preview

The report is organized into four analytical pages:

### 1. Executive Overview
![Executive Overview](Images/Page%201.png)

### 2. Passenger & Demand
![Passenger & Demand](Images/Page%202.png)

### 3. Revenue & Profitability
![Revenue & Profitability](Images/Page%203.png)

### 4. Metro Network & Operations
![Metro Network & Operations](Images/Page%204.png)

## Project Overview

This project was developed in Microsoft Power BI to explore a metro-operations dataset and present key metrics through interactive visuals and slicers.

The dashboard covers:

- Passenger volume and trip activity
- Passenger demand trends and ticket-type contribution
- Revenue, estimated cost, profit, and profit margin
- Route and station-level patterns
- Distance-band analysis
- Station network and station-layout information

## Dashboard Pages

| Page | Focus | Examples of analysis |
|---|---|---|
| Executive Overview | High-level performance | Passengers, trips, revenue, profit, monthly trends, leading origins and routes |
| Passenger & Demand | Ridership patterns | Monthly passenger demand, weekday patterns, ticket-type contribution, origin and destination stations |
| Revenue & Profitability | Financial analysis | Revenue vs cost, profit margin by distance band, monthly margin, revenue by distance band, profit drivers |
| Metro Network & Operations | Network and route insights | Station map, route passenger volume, station layout, trip-distance analysis |

## Key Metrics

The report includes measures such as:

- Total Trips
- Total Passengers
- Total Revenue
- Total Cost
- Total Profit
- Profit Margin
- Average Fare
- Passengers per Trip
- Revenue per Passenger
- Revenue per Trip
- Average Daily Passengers
- Peak Daily Passengers
- Average Distance

Revenue and cost are calculated from the supplied fare, passenger, and cost-per-passenger fields. They should be interpreted as **dataset-derived estimates**, not audited financial figures.

## Data Files

You can access the source and cleaned data files directly from this repository.

### Raw datasets

| File | Format | Download |
|---|---|---|
| Trip data — raw | CSV | [Download CSV](https://github.com/DevanshGupta03/Delhi-Metro-Operations-Revenue-Analytics/raw/refs/heads/main/Raw%20Dataset%20CSV/01_Trip_Data_Raw.csv) |
| Station master — raw | CSV | [Download CSV](https://github.com/DevanshGupta03/Delhi-Metro-Operations-Revenue-Analytics/raw/refs/heads/main/Raw%20Dataset%20CSV/02_Station_Master_Raw.csv) |
| Trip data — raw | Excel | [Download XLSX](https://github.com/DevanshGupta03/Delhi-Metro-Operations-Revenue-Analytics/raw/refs/heads/main/Raw%20Dataset%20XLSX/01_Trip_Data_Raw.xlsx) |
| Station master — raw | Excel | [Download XLSX](https://github.com/DevanshGupta03/Delhi-Metro-Operations-Revenue-Analytics/raw/refs/heads/main/Raw%20Dataset%20XLSX/02_Station_Master_Raw.xlsx) |

### Cleaned datasets

| File | Format | Download |
|---|---|---|
| Trip data — cleaned | Excel | [Download XLSX](https://github.com/DevanshGupta03/Delhi-Metro-Operations-Revenue-Analytics/raw/refs/heads/main/Cleaned%20Dataset/01_Trip_Data_Cleaned.xlsx) |
| Station master — cleaned | Excel | [Download XLSX](https://github.com/DevanshGupta03/Delhi-Metro-Operations-Revenue-Analytics/raw/refs/heads/main/Cleaned%20Dataset/02_Station_Master_Cleaned.xlsx) |

### Power BI report

[Download the Power BI file (.pbix)](https://github.com/DevanshGupta03/Delhi-Metro-Operations-Revenue-Analytics/raw/refs/heads/main/Delhi_Metro_Operations_Revenue_Analytics.pbix)

> The links above point to the repository's raw file URLs so visitors can download the datasets and PBIX directly.

## Data Preparation & Notes

The trip dataset contains approximately **150,000 records** and covers the period represented in the report (2022–2024). The project includes a separate station master dataset.

Preparation work included:

- Trimming text fields and standardizing missing values
- Converting date and numeric columns to appropriate data types
- Handling missing ticket-type and remarks values
- Imputing missing passenger counts using grouped and fallback medians
- Reviewing duplicate trip records and IDs without automatically deleting records

### Important interpretation and modelling limitations

- The datasets are Kaggle-sourced / practice data and have not been independently verified as official Delhi Metro Rail Corporation operational records. This project must not be interpreted as an official DMRC report.
- Revenue, cost, profit, and profit margin are derived from the fields supplied in the dataset and are not official financial results.
- Passenger values include imputed records where the original passenger value was missing.
- The station master contains repeated station names for different station/line records. The trip table does not contain a corresponding unique Station ID, so station master records are not fully related to trip records through a reliable station key. Station-level visuals should be interpreted within this modelling limitation.

## Tools & Technologies

- Microsoft Power BI
- Power Query
- DAX
- Microsoft Excel
- Git and GitHub

## Repository Structure

```text
Metro Project/
├── Cleaned Dataset/
│   ├── 01_Trip_Data_Cleaned.xlsx
│   └── 02_Station_Master_Cleaned.xlsx
├── Images/
│   ├── Delhi_Metro_full_logo.png
│   ├── Page 1.jpg
│   ├── Page 2.jpg
│   ├── Page 3.jpg
│   └── Page 4.jpg
├── Raw Dataset CSV/
│   ├── 01_Trip_Data_Raw.csv
│   └── 02_Station_Master_Raw.csv
├── Raw Dataset XLSX/
│   ├── 01_Trip_Data_Raw.xlsx
│   └── 02_Station_Master_Raw.xlsx
├── Delhi_Metro_Operations_Revenue_Analytics.pbix
├── .gitignore
└── README.md
```

## How to Explore

1. Open the dashboard screenshots above to preview the four report pages.
2. Download the `.pbix` file to explore the interactive report in Power BI Desktop.
3. Download the raw or cleaned datasets from the links above to inspect the data.

## Author

**Devansh Gupta**

Data Analytics | Power BI | DAX | Excel | Data Visualization

---

If you find this project useful, feel free to explore the dashboard and datasets.
