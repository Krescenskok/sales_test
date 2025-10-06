# 🧾 Sales Dashboard Project

Build a Power BI Dashboard while demonstrating how to build data pipelines.

## 🎶 Stakeholder Problem Statement
- Stakeholder wants to see sales by customer.
- Stakeholder wants to see sales by geo-location.

## 🚀 TODOS

- Data wrangling / EDA.
- Load and preprocess data in data pipelines.
- Build bronze, silver, gold medallion layers. Nothing too crazy needed.
- Build a Power BI Dashboard utilizing gold layer.

## 📦 Project Tech Stack
- uv
- Python
    - PySpark, Polars, Pandas
- Database
    - DuckDB or something similar to demonstrate object storage for use in Power BI.
- Orchestration
    - Not needed for this project, but we do use Databricks and Prefect.


## 🛠️ Setup Instructions

1. **Clone the repo**
   ```bash
   git clone https://github.com/Krescenskok/sales_test.git
   cd sales_test
   ```


## Explanation of process
1. Examples of EDA:
- Inspected the data for null and duplicate rows, if they existed, I dropped them from the dataframe.
- If more data cleanup was necessary for this project (for example, if Data Scientist needed to use the data), I would have created boxplots to identify outliers or histograms to understand the distribution of the columns.

2. Example of loading and preprocessing data in data pipelines/Build bronze, silver, gold medallion layers:
- For this step, I have created 3 different notebooks:
     1. Extract Source to Bronze Unity Catalog: This takes the JSON files from the GitHub repository and copies them into a volume in unity catalog as the bronze layer (raw data)
     2. Extract Bronze to Silver Unity Catalog: This is where the cleanup occurs, and adding metadata columns. In this notebook, I cleaned up the data by removing null and duplicate records. In addition, I cleaned up the column names and added metadata columns containing the file name and the upload date.
     3. Extract Silver to Gold Unity Catalog: This is where the aggregations and joins occur. I provided examples of both operations using SQL in order to answer the stakeholder problem statement. 2 tables were created in the gold layer, one table to answer each problem statement.
     4. These 3 steps are part of the data pipeline as the first notebook needs to occur first (extract), then the 2nd notebook occurs for cleanup (transformation), and lastly, loading the tables to the gold layer (load).
         <img width="712" height="292" alt="Screenshot 2025-10-06 at 11 16 38 AM" src="https://github.com/user-attachments/assets/3dfda401-2cf3-4a6c-91af-954e1a468ca5" />
 
3. Build a Power BI Dashboard utilizing gold layer:
- For this step, I connected Power BI to my Gold schema in Databricks Unity Catalog, and imported the 2 tables I created.
- These 2 tables were then used to solve the stakeholder problem statements, where 2 visualizations were created:
    1. The first visualization is a bar graph, displaying the number of sales per customer. In addition, I included a filter with the customer ID and name so that the stakeholders can zoom in on certain customers if needed. Another feature in this visualization is the tooltip, which displays the customer name, customer ID, and the number of sales for that customer.
 
       <img width="1193" height="684" alt="Screenshot 2025-10-06 at 11 44 23 AM" src="https://github.com/user-attachments/assets/2ecc30e7-0d32-40ff-8729-c13df36c50ad" />
       
    2. The second visualization is a heat map, displaying the number of sales per country. In addition, I included a filter with the region so that the stakeholders can zoom into each region and help them make informed business decisions on where they should focus more on sales. Another feature in this visualization is the tooltop, which displays the Country abbreviation, Country name, total sales, and the region.
       
       <img width="1180" height="671" alt="Screenshot 2025-10-06 at 11 45 33 AM" src="https://github.com/user-attachments/assets/8c365872-5cf7-4f82-be50-d740e7671dcf" />

