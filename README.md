# Data-Warehouse-project
Data Warehouse for ATL Airport — analyzing flights, passengers, and weather data using a snowflake schema and ETL process for advanced decision support.
# ✈️ ATL Airport Data Warehouse (2014–2024)

## 📘 Project Overview
This project is a **Data Warehouse** designed for **Hartsfield–Jackson Atlanta International Airport (ATL)**.  
It aims to support **strategic decision-making and performance analysis** by integrating data from multiple sources such as flights, airlines, passengers, climate, and destinations.

The warehouse stores **10 years of historical data (2014–2024)** and provides a **multidimensional analysis** of flight operations, passenger traffic, and weather impact.

---

## 🎯 Objectives
- Centralize heterogeneous data related to airport operations.  
- Enable **OLAP analysis** (e.g., total flights per airline, average delays per season, etc.).  
- Improve **data quality and consistency** through ETL processes.  
- Provide insights for **airport management and performance optimization**.

---

## 🧩 Data Model (Snowflake Schema)

**Fact Table:**
- `FactFlights` — contains key performance indicators (flight counts, delays, passengers, etc.)

**Dimension Tables:**
- `DimAirline` — airline details  
- `DimAircraft` — aircraft type and capacity  
- `DimAirport` — airport information  
- `DimCity` — city details  
- `DimCountry` — country information  
- `DimDate` — time dimension (year, month, day, season)  
- `DimWeather` — weather and climate conditions  

> The model follows a **Snowflake Schema**, allowing optimized storage and better data normalization.

---

## 🔄 ETL Process
The ETL (Extract – Transform – Load) process integrates raw data from multiple sources into the warehouse.

1. **Extract**  
   - Collect raw data on flights, passengers, airlines, and weather from CSV, API, or manual sources.  

2. **Transform**  
   - Clean, format, and validate data (handle duplicates, missing values, and inconsistent codes).  
   - Apply business rules (e.g., mapping cities to countries, classifying flight delays).  

3. **Load**  
   - Load data into SQLite database following the snowflake schema.  

> ETL implemented with SQL scripts and automated data generation.

---

## 📊 OLAP & Analytics
Using **OLAP cubes**, users can analyze:
- Number of flights per airline, route, or time period  
- Average passenger load per aircraft type  
- Impact of weather conditions on delays  
- Year-over-year trends in airport performance  

Example queries:
```sql
-- Total number of delayed flights per airline
SELECT a.airline_name, COUNT(*) AS total_delays
FROM FactFlights f
JOIN DimAirline a ON f.idAirline = a.idAirline
WHERE f.delay > 0
GROUP BY a.airline_name
ORDER BY total_delays DESC;
