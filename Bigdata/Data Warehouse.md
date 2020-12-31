# Data Warehouse

- [Data Warehouse](#data-warehouse)

## What Data Warehouse is

- A data warehouse (DW or DWH), also known as an enterprise data warehouse (EDW), is a system used for reporting and data analysis, and is considered a core component of business intelligence.
- DWs are central repositories of integrated data from one or more disparate sources.
- They store current and historical data in one single place that are used for creating analytical reports for workers throughout the enterprise.
- The data stored in the warehouse is uploaded from the operational systems.
- The data may require data cleansing for additional operations to ensure data quality before it is used in the DW for reporting.

## Main approaches to build EDW

### Extract, Transform, Load (ETL) Approach

- ETL-based WH uses staging, data integration, and access layers.
- The staging layer:
  - or staging database stores raw data extracted from each of the disparate source data systems.
- The integration layer:
  - It integrates the disparate data sets by transforming the data from the staging layer.
  - The integrated data are then moved to yet another database, often called the data warehouse database.
  - The moved data is arranged into hierarchical groups, often called dimensions, and into facts and aggregate facts.
  - The combination of facts and dimensions is sometimes called a star schema.
- The access layer helps users retrieve data.

### Extract, Load, Transform Approach

- ELT-based data warehousing gets rid of a separate ETL tool for data transformation. Instead, it maintains a staging area inside the data warehouse itself.
- The data gets extracted from various source systems and are then directly loaded into the data warehouse, before any transformation occurs.
- All necessary transformations are then handled inside the data warehouse itself.
- Finally, the manipulated data gets loaded into target tables in the same data warehouse.

## Resources

- [Wikipedia](https://en.wikipedia.org/wiki/Data_warehouse#ETL-based_data_warehousing)
- [Amazon AWS](https://aws.amazon.com/data-warehouse/)