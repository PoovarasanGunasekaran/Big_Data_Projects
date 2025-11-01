#  Casino Daily Summary Pipeline in Azure

This project automates the daily processing of casino customer summary files using **Azure Data Lake Storage Gen2, Azure Data Factory, and Databricks**. It separates customers into distinct tiers, generates daily output files for each group, and streamlines business analytics by producing clean, ready-to-use datasets for further analysis.


## Architecture Overview
 -    **Input Files:**  Daily summary CSV files (18 columns) are dropped into the ADLS Gen2 input folder.
  -   **Azure Data Factory Pipeline:**
	    -   Reads the input CSV file.
        -   Applies mapping and splits the data into five customer segments:  
	        -   Folder 1: Premium Tier customers (`Customer_tier = "Premium"`)
            -   Folder 2: Gold Tier customers (`Customer_tier = "Gold"`)
            -   Folder 3: Silver Tier customers (`Customer_tier = "Silver"`)
            -   Folder 4: New customers (`Customer_tier`  is empty)
	        -   Folder 5: All other records (non-matching  `Customer_tier`)
           -   Each segment is saved in its designated folder within ADLS Gen2.
        
-   **Databricks Notebook:**
    -   Reads all five customer segment folders individually.
    -   For each folder:
        -   Groups data by  `customer_ID`
        -   Orders each group by  `clock_in_instance`
        -   Selects only the last record for each customer (latest clock in instance)
        -   Writes the result as a Parquet file named  `<Tier>_currentdate.parquet`  into a different ADLS Gen2 storage account for each segment.

## Features

-   Automated daily ingestion and partitioning of summary files.
-   Flexible tier segmentation: Premium, Gold, Silver, New, and Other.
-   Efficient grouping of the latest customer activity.
-   Output in Parquet format for optimal analytics performance.
-   End-to-end orchestration with scalable Azure cloud services.

## Technologies Used

-   Azure Data Factory
-   Azure Data Lake Storage Gen2
-   Databricks (Python/PySpark)
-   Parquet output files

# Working Steps:-
## Pipeline Overview



## Azure Data Factory Pipeline



## Databricks Notebook



## Input File Structure
