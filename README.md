# :star2: AWS Serverless Data Lake Jumpstart :star2:

In this [Lab experiment](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US),  a cloud-native and future proof serverless data lake architecture has been built using the Lambda Architecture data processing pattern.

## Objective :
1. To analyze dataset on the flow of yellow taxi trips from pickup borough to dropoff borough in New York city.
2. To emphasis analysis on taxi trips originating from Manhatton only

![image](https://github.com/user-attachments/assets/5b880093-4866-4927-945c-1da8a891aa18)


## Used services
1. **Amazon S3**: Source to fetch raw dataset about taxi trips in New York; Destination to keep the transformed data with **ETL** (Extract, Transform, Load) process for analysis purpose
2. **AWS Glue**: To discover and catalog the fetched source data from Amazon S3, to apply ETL process on the raw data to format it for visualization, and to catalog the transformed data as well.
4. **Amazon Athena**: To query the cataloged dataset prior to applying ETL process and afterwards.
5. **Amazon Quicksite**: Analyze the tranform data to visualize the flow of yellow taxi trips in New York from pickup borough to dropoff borough. Also filtering the dataset to focus on trips originating from **Manhatton** only

## Prior preparations for the Lab from Amazon
1. Amazon S3 buckets were created.
2. sample data files were copied to Amazon S3 buckets.
3. an IAM (Identity and Access Management) service role was created.

![image](https://github.com/user-attachments/assets/f086e6c7-6c39-4be1-be1c-0ab3b5b81eee)

## Requirements to run the labs
1. [Instructor led](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/10-getting-started/11-workshop-studio/aws-event) (_I followed this worflow using a workshop studio with free amazon user account valid for 72 hourse._)
2. [Self paces](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/10-getting-started/12-own-account)

## Labs executed
Lab 1: [Discovering and cataloging the data](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/README.md#lab-1-discovering-and-cataloging-the-data) </br>
Lab 2: [Exploring the data](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/README.md#lab-2-exploring-the-data) </br>
Lab 3: [Transforming the data](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/README.md#lab-3-transforming-the-data) </br>
Lab 4: [Enriching the data](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/README.md#lab-4-enriching-the-data) </br>
Lab 5: [Visualizing the data](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/README.md#lab-2-visualizing-the-data) </br>

## Lab 1: Discovering and Cataloging the Data

> A data lake has an array of data sources and formats. So it is important to **discover** and **catalog** the acquired data to **understand** it and **enable integrations** with other purpose built AWS services.

In this lab, An **AWS Glue crawler** is created to **auto discover** the **schema** of the data stored in amazon S3.</br>
The discovered information (from above) is **registered** in the **AWS Glue Catalog**. This enables AWS Glue to use the stored catalog information for **ETL processing**. It will also allow **AWS Athena** to **run queries** on the data stored in Amazon S3. </br> </br>


### Action 1. Creating a Glue Crawler:
a. Setting crawler properties, _a.k.a_ **name** </br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/1_set_crawler_properties.png) </br></br>
b. Choosing data sources and classifiers. Here, **S3** has been selected as the **data source** and it's **path** has been added for crawling purposes.</br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/2_choose_daatsource_and_classifier_1.png) </br></br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/2_choose_daatsource_and_classifier_2.png)</br></br>
c. Configuring security settings. Here, **ServerlessAnalyticsRole** has been selected as the existing **IAM** role.</br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/3_configure_security_settings.png)</br></br>
d. Setting outputs and scheduling. At first, a new database **nyctaxi_db** has been created as the **target database**. Later, when available for selection, **nyctaxi_db** is included in the output confifuration with **raw_** as table name prefix.</br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/4_set_output_and_scheduling_1.png)  </br></br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/4_set_output_and_scheduling_2.png)</br></br>
e. After reviewing the configurations, the glue crawler **nyx_taxi_crawler** is created.</br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/5_review_and_create_crawler_1.png) </br></br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/5_review_and_create_crawler_2.png)
</br></br>

Instructions from AWS to create crawlers can be found [here](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/20-cataloging-data/21-create-crawler). </br></br></br>

### Action 2. Running the Crawler
Here the data would be cataloged by running the created crawler. When the crawler **nyx_taxi_crawler** has run successfully, a value of **2** would appear under the column **Table changes from the last run** under the crawler list. </br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/6_run_crawler.png)
</br></br>

Instructions from AWS to run a crawler can be found [here](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/20-cataloging-data/22-run-crawler). </br></br></br>

### Action 3. Review the metadata in Glue Data Catalog
To review metadata of the created database, the **schemas** of any table included in the Database can be checked.</br>

for example, the **raw_yellow_trip** table from the **nyctaxi_db** database has the following **18** columns:</br>
`veodorid`, `tpep_pickup_datetime`, `tpep_dropoff_datetime`, `passenger_count`, `trip_distance`, `ratecodeid`, `store_and_fwd_flag`, `pulocationid`, `dolocationid`, `payment_type`, `tpep_pickup_datetime`, `fare_amount`, `extra`, `mta_tax`, `tip_amount`, `tolls_amount`, `improvement_surcharge`, `total_amount`, `congestion_surcharge`. <br>

Instructions from AWS to run a crawler can be found [here](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/20-cataloging-data/23-review-metadata). </br></br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/7_view_table_metadata_1.png)
</br></br>![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/7_view_table_metadata_2.png)
</br></br>

> Glue Data Catalog contains references to data that is used as sources and targets of the extract, transform, and load (ETL) jobs in AWS Glue.


## Lab 2: Exploring the data

In this lab, **Amazon Athena** has been used to explore the data and and check for data quality issues. To fix the quality issues, relevant **table properties** in the **AWS Glue Catalougs** have been updated.</br>

> Amazon Athena automatically stores query results and metadata information for each query that runs in a query result location specified in Amazon S3. If necessary, the files in this location can be accessed to work with them. Query result files can also be directly downleaded from the Athena console.

These [instructions](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/30-exploring-data/31-using-athena-first-time) should be followed when launching **Amazon Athena** for the first time. <b/r>

### Action 1: Previewing the table data

Data included in the tables **raw_yellow_tripdata** and **taxi_zone_lookup** can be previewed by clicking on the menu icon **⋮** beside the relevant table, and then selecting **Preview table**. </br> </br>

![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab2/1_preview_data.gif) </br> </br>

Instructions from AWS to use **Amazon Athena** for previewing table data from a database can be found [here](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/20-cataloging-data/23-review-metadata). </br></br>

### Action 2: Identifying and Fixing Data Quality Issues

In this lab, quotes associated with string values under different tables were removed to improve the quality of the data to be analyzed.

![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab2/2_csv_data_with_quotes.png) </br> </br>

> In the previous step, **quotes ("")** around the data values (e.g. from columns **borough**, **zone**, etc.) in the CSV file associated with the **taxi_zone_lookup** table were found. These quotes shouldn't be part of the data to be analyzed later. So to read the CSV file properly, table properties in AWS glue were updated to use the serialization library **OpenCSVSerDe**. In addition, the existing Serde parameter(s) was removed and was replaced with the following **key-value** pairs:

- `escapeChar`, `\`
- `quoteChar`, `"`
- `escapeChar`, `,`
</br> </br>

![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab2/3_changing_serialization-library.gif) </br> </br>
![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab2/4_adding_delimeters.gif) </br> </br>

> When the preview query for **taxi_zone_lookup** was run, the column values appeared with removed quotes.

Instructions from AWS to update the **Serialization lib** for previewing table data from a database can be found [here](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/30-exploring-data/33-handling-csv-double-quote). </br></br>

### Action 3: Running SQL Queries to Explore the data

The following SQL queries were run to explore the data:

**1. Checking number of yellow taxi trip records**
```SELECT COUNT(*) "Count" FROM raw_yellow_tripdata;``` </br></br>
**2. Exploring data categories**
```
-- observe NULL values
SELECT vendorid, COUNT(*) "Count"
FROM  raw_yellow_tripdata
GROUP BY vendorid
ORDER BY 1;
```
```
-- observe other categories
SELECT pulocationid, COUNT(*) "Count"
FROM   raw_yellow_tripdata
GROUP BY pulocationid
ORDER BY 1;
```
```
-- observe NULL values
SELECT payment_type, COUNT(*) "Count"
FROM   raw_yellow_tripdata
GROUP BY payment_type
ORDER BY 1;
```
</br></br>
**3. Explore records with NULL Vendor ID**
**4. Explore records by time period**
**5. Count records that falls outside of year 2020**
**6. Count records with NULL values (based on Vendor ID) that falls within 2020**
**7. Count records that falls in the last quarter of 2020, exclude records with missing Vendor ID**
**8. Join taxi trips data with taxi zone look up table**


## Lab 3: Transforming the data

## Lab 4: Enriching the data

## Lab 5: Visualizing the data



## Terminologies (in order of appearances)
- [Data Lake](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/10-getting-started#what-is-a-data-lake)
- [Amazon S3](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/10-getting-started#introducing-amazon-s3)
- [Amazon Glue](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/20-cataloging-data#introducing-aws-glue)
- [Amazon Athena](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/30-exploring-data#introducing-amazon-athena)
- 


