# Azure-Data-Factory

# Azure-Data-Factory

## 📘 Dynamic Copy of Multiple Azure SQL Database Tables to Azure Data Lake Storage Gen2

Welcome to **Dynamic Azure Data Factory Integration**! This project demonstrates how to use Azure Data Factory to **dynamically extract and copy multiple tables from an Azure SQL Database** into Azure Data Lake Storage Gen2 (ADLS Gen2). The solution is metadata-driven and does **not require hardcoding of table names** — making it highly scalable and maintainable across large databases.

---

## 📌 Project Goals

- Automatically identify and extract table metadata (names and schema) from the Azure SQL database.
- Leverage ADF’s Lookup and ForEach activities to drive dynamic data movement.
- Copy each table’s data into a structured ADLS Gen2 location using parameterized datasets and linked services.

...

## 🧾 Metadata Table Example

The following SQL query is used to extract the table metadata from Azure SQL DB:

```sql
SELECT 
    QUOTENAME(t.name) AS tableName, 
    QUOTENAME(SCHEMA_NAME(t.schema_id)) AS schemaName 
FROM 
    sys.tables AS t

---

Sample Output:
tableName	schemaName
[Customer]	[SalesLT]
[Product]	[SalesLT]
[ErrorLog]	[dbo]
[Address]	[SalesLT]

This metadata feeds into the Lookup activity in the pipeline, which then drives the ForEach loop to copy data table-by-table.

---

⚙️ Pipeline Structure
Lookup Activity – Fetches the table and schema names dynamically.

ForEach Activity – Iterates over the metadata list.

Copy Data Activity – Performs the actual data copy from SQL DB to ADLS Gen2.v
