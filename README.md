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

### Lab 1: Discovering and Cataloging the Data

> A data lake has an array of data sources and formats. So it is important to **discover** and **catalog** the acquired data to **understand** it and **enable integrations** with other purpose built AWS services.

In this lab, An **AWS Glue crawler** is created to **auto discover** the **schema** of the data stored in amazon S3.</br>
The discovered information (from above) is **registered** in the **AWS Glue Catalog**. This enables AWS Glue to use the stored catalog information for **ETL processing**. It will also allow **AWS Athena** to **run queries** on the data stored in Amazon S3. </br> </br>

#### Actions
**1. Creating a Glue Crawler:** </br> </br>
a. Setting crawler properties, _a.k.a_ **name** </br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/1_set_crawler_properties.png) </br></br>
b. Choosing data sources and classifiers. Here, **S3** has been selected as the **data source** and it's **path** has been added for crawling purposes.</br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/2_choose_daatsource_and_classifier_1.png) </br></br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/2_choose_daatsource_and_classifier_2.png)</br></br>
c. Configuring security settings. Here, **ServerlessAnalyticsRole** has been selected as the existing **IAM** role.</br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/3_configure_security_settings.png)</br></br>
d. Setting outputs and scheduling. At first, a new database **nyctaxi_db** has been created as the **target database**. Later, it has been included in the output condifuration with **raw_** as table name prefix.</br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/4_set_output_and_scheduling_1.png)  </br></br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/4_set_output_and_scheduling_2.png)</br></br>
e. Reviewing and creating the glue crawler **nyx_taxi_crawler**.</br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/5_review_and_create_crawler_1.png) </br></br> ![image](https://github.com/Nazarah/aws-serverless-datalake-jumpstart/blob/main/Images/lab1/5_review_and_create_crawler_2.png)
</br></br>
Instructions for this lab from AWS can be found [here](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/20-cataloging-data/21-create-crawler).


### Lab 2: Exploring the data

### Lab 3: Transforming the data

### Lab 4: Enriching the data

### Lab 5: Visualizing the data



## Terminologies (in order of appearances)
- [Data Lake](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/10-getting-started#what-is-a-data-lake)
)
- [Amazon S3](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/10-getting-started#introducing-amazon-s3)
- [Amazon Glue](https://catalog.us-east-1.prod.workshops.aws/workshops/276faf92-bffc-4843-8a8e-8078add48194/en-US/20-cataloging-data#introducing-aws-glue)



