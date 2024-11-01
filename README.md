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
Lab 1: [Discovering and cataloging the data](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/20-cataloging-data)
Lab 2: [Exploring the data](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/30-exploring-data)
Lab 3: [Transforming the data](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/40-transforming-data)
Lab 4: [Enriching the data](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/50-enriching-data)
Lab 5: [Visualizing the data](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/60-visualizing-data)

### Lab 1: Discovering and Cataloging the Data

> A data lake has an array of data sources and formats. So it is important to **discover** and **catalog** the acquired data to **understand** it and **enable integrations** with other purpose built AWS services.

In this lab, the following actions have been executed:
1. Create an **AWS Glue crawler** to **auto discover** the **schema** of the data stored in amazon S3
2. The discovered information (from above) is **registered** in the **AWS Glue Catalog**. This enables AWS Glue to use the stored catalog information for **ETL processing**.
4. It will also allow **AWS Athena** to **run queries** on the data stored in Amazon S3.



## Terminologies (in order of appearances)
- [Data Lake](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/10-getting-started#what-is-a-data-lake)
)
- [Amazon S3](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/10-getting-started#introducing-amazon-s3)
- [Amazon Glue](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/20-cataloging-data#introducing-aws-glue)



