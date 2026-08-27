AWS Sales Data Pipeline

"AWS" (https://img.shields.io/badge/AWS-Cloud-FF9900?style=flat&logo=amazonaws&logoColor=white)
"Python" (https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)
"Lambda" (https://img.shields.io/badge/AWS_Lambda-Serverless-FF9900?style=flat&logo=awslambda&logoColor=white)
"RDS" (https://img.shields.io/badge/Amazon_RDS-MySQL-527FFF?style=flat&logo=amazonrds&logoColor=white)
"S3" (https://img.shields.io/badge/Amazon_S3-Storage-569A31?style=flat&logo=amazons3&logoColor=white)
"SNS" (https://img.shields.io/badge/Amazon_SNS-Notifications-FF4F8B?style=flat&logo=amazonsns&logoColor=white)
"Status" (https://img.shields.io/badge/Status-Completed-brightgreen?style=flat)

---

Table of Contents

- "Project Overview" (#project-overview)
- "Business Problem" (#business-problem)
- "Proposed Solution" (#proposed-solution)
- "Architecture" (#architecture)
- "AWS Services Used" (#aws-services-used)
- "Dataset" (#dataset)
- "Pipeline Execution Results" (#pipeline-execution-results)
- "Sales KPI Dashboard" (#sales-kpi-dashboard)
- "Repository Structure" (#repository-structure)
- "Deployment Guide" (#deployment-guide)
- "Key Benefits" (#key-benefits)
- "Challenges" (#challenges)
- "Future Enhancements" (#future-enhancements)
- "Key Learning Outcomes" (#key-learning-outcomes)
- "Conclusion" (#conclusion)
- "Author" (#author)

---

Project Overview

The AWS Sales Data Pipeline is a cloud-based data engineering project designed to process online retail sales data using AWS services.

The pipeline takes raw sales data through a processing and validation workflow, separates valid and rejected records, stores the resulting data, and provides a Sales KPI Dashboard for visualization and analysis.

The project demonstrates practical application of:

- AWS cloud services
- Serverless data processing
- Data validation and cleaning
- Structured data storage
- Event-driven notifications
- Data visualization

---

Business Problem

Businesses generate large volumes of sales data that must be cleaned, validated, stored, and analyzed before it can support effective decision-making.

Manual processing can be time-consuming and makes it difficult to:

- Identify and isolate invalid records
- Maintain organized, audit-ready datasets
- Store processed data in a structured format
- Generate timely sales insights
- Receive notifications about pipeline execution

This project addresses these challenges by implementing a cloud-based sales data pipeline that automates key stages of data processing and organization.

---

Proposed Solution

The solution uses AWS services to create a serverless sales data processing workflow.

The pipeline:

1. Stores raw sales data in Amazon S3
2. Processes and validates the data using AWS Lambda
3. Separates records into valid and rejected datasets
4. Stores valid and rejected outputs in Amazon S3
5. Loads accepted records into Amazon RDS
6. Uses Amazon SNS for pipeline completion and alert notifications
7. Uses the processed data to generate a Sales KPI Dashboard

---

Architecture

The pipeline follows a cloud-based architecture in which sales data moves from ingestion through serverless processing, validation, structured storage, notification, and visualization.

Pipeline Flow

                    Online Retail CSV
                           │
                           ▼
                    Amazon S3
                    Raw Data
                           │
                           ▼
                    AWS Lambda
              Validation & Processing
                     /          \
                    /            \
                   ▼              ▼
          Valid Records      Rejected Records
                │                  │
                ▼                  ▼
          Amazon S3             Amazon S3
         Valid Data          Rejected Data
                │
                ▼
           Amazon RDS
       Processed Sales Data
                │
                ▼
       Sales KPI Dashboard

                    AWS Lambda
                        │
                        ▼
                   Amazon SNS
              Completion / Alerts

Architecture Diagram

The detailed AWS architecture diagram will be included in the repository under the "architecture/" directory.

---

AWS Services Used

AWS Service| Purpose
Amazon S3| Stores raw, valid, and rejected sales data
AWS Lambda| Performs serverless data processing and validation
Amazon RDS| Stores accepted sales records in a relational MySQL database
Amazon SNS| Sends pipeline completion and alert notifications
AWS IAM| Provides identity and access management for AWS resources

---

Dataset

Source: UCI Online Retail Dataset via Kaggle

Description: Transactional sales records from a UK-based online retailer.

The dataset contains information about invoices, products, quantities, prices, customers, transaction dates, and customer countries.

Schema

Column| Type| Description
"InvoiceNo"| String| Unique invoice/order identifier
"StockCode"| String| Product/item code
"Description"| String| Product name
"Quantity"| Integer| Units sold per line item
"InvoiceDate"| DateTime| Date and time of the transaction
"UnitPrice"| Float| Price per unit in GBP
"CustomerID"| Float| Unique customer identifier
"Country"| String| Country of the customer

Revenue Formula

Revenue = Quantity × UnitPrice

Data Categories

Repository Path| Description
"data/raw/"| Original raw sales data
"data/valid/"| Records that passed the validation and cleaning stage
"data/rejected/"| Records rejected during processing

---

Pipeline Execution Results

The pipeline was executed using AWS Lambda, with the resulting datasets stored in Amazon S3 and accepted records loaded into Amazon RDS.

Processing Summary

Metric| Value
Raw records processed| 50,000
Valid / accepted records| 30,315 (60.6%)
Rejected records| 19,685 (39.4%)
Accepted data file| "valid/valid_sales.csv"
RDS destination| "salesdb.sales_transactions"
Database engine| MySQL 8.4
Lambda runtime| Python 3.12
Lambda memory| 256 MB
Approximate Lambda execution time| 46 seconds
SNS alert topic| "sales-pipeline-alerts"
Pipeline execution timestamp| 2026-08-27 13:24 UTC

Validation Rules Applied

The Lambda function rejected records containing any of the following:

- Null or missing values in required fields
- Negative or zero "Quantity" values
- Zero or negative "UnitPrice" values

This validation ensures that only records meeting the defined business rules proceed to the accepted-data stage.

---

Sales KPI Dashboard

A Sales KPI Dashboard was developed to present sales performance using charts and tables derived from the accepted pipeline output.

Dashboard location:

"visualizations/dashboard.html"

Dashboard Visualizations

#| Visualization| Business Insight
1| KPI Summary Cards| Provides an at-a-glance view of key sales metrics
2| Monthly Revenue Trend| Shows revenue trends over time
3| Top 10 Products by Revenue| Identifies the highest-value products
4| Top 10 Products by Quantity Sold| Identifies products with the highest sales volume
5| Revenue by Country| Highlights major geographic markets
6| Orders by Month| Shows changes in order volume over time
7| Top Customers by Revenue| Identifies high-value customers

All business visualizations are based on accepted records.

Rejected records are excluded from business KPI calculations.

---

Repository Structure

aws-sales-data-pipeline/
│
├── data/
│   ├── raw/
│   │   └── online_retail.csv
│   │
│   ├── valid/
│   │   └── valid_sales.csv
│   │
│   └── rejected/
│       └── rejected_sales.csv
│
├── visualizations/
│   └── dashboard.html
│
├── LICENSE
└── README.md

---

Deployment Guide

The following steps summarize how the pipeline can be deployed in an AWS environment.

Prerequisites

- AWS account
- AWS Management Console access
- Python 3.x
- Online Retail dataset
- Basic knowledge of Amazon S3, Lambda, RDS, IAM, and SNS

---

Step 1 — Create Amazon S3 Storage

1. Open the Amazon S3 console.
2. Create an S3 bucket.
3. Create the required data locations for:
   - Raw data
   - Valid data
   - Rejected data
4. Upload the raw sales dataset to the raw-data location.

---

Step 2 — Configure IAM

Create an IAM role for the Lambda function.

The role should provide only the permissions required by the pipeline, including access to the relevant S3 resources and other AWS services used by the Lambda function.

For production environments, permissions should follow the principle of least privilege rather than using broad managed policies.

---

Step 3 — Configure Amazon RDS

1. Create a MySQL Amazon RDS database.
2. Configure the required networking and security-group rules.
3. Create the target database and sales table.
4. Configure the Lambda function with the required database connection information.
5. Verify that Lambda can communicate with the RDS instance.

---

Step 4 — Deploy AWS Lambda

1. Create a Lambda function.
2. Select Python 3.12 as the runtime.
3. Attach the appropriate IAM execution role.
4. Deploy the data-processing code.
5. Configure the required memory and timeout settings.
6. Configure the environment variables or connection settings required by the pipeline.

The Lambda function performs the validation and processing logic and routes records to their appropriate destinations.

---

Step 5 — Configure Notifications

Amazon SNS is used to provide pipeline notifications.

The SNS topic is used for:

- Pipeline completion notifications
- Pipeline alert notifications

This provides visibility into the outcome of pipeline execution.

---

Step 6 — Execute and Validate the Pipeline

After deployment:

1. Provide the raw sales file to the pipeline.
2. Monitor Lambda execution.
3. Review the Lambda execution logs.
4. Confirm valid records are written to the valid-data location.
5. Confirm rejected records are written to the rejected-data location.
6. Confirm accepted records are available in Amazon RDS.
7. Confirm the SNS notification is delivered.
8. Use the accepted data to generate the KPI dashboard.

---

Key Benefits

- Automates important stages of sales data processing.
- Separates valid and rejected records.
- Improves data organization and traceability.
- Uses serverless processing with AWS Lambda.
- Provides structured storage through Amazon RDS.
- Uses Amazon S3 for scalable object storage.
- Provides SNS notifications for pipeline execution.
- Provides a sales dashboard for business analysis.
- Creates a foundation for future data engineering and analytics solutions.

---

Challenges

During the project, several challenges were encountered, including:

- Configuring multiple AWS services
- Managing IAM permissions
- Working with a large real-world sales dataset
- Designing data validation rules
- Handling rejected records
- Connecting AWS Lambda with Amazon RDS
- Configuring pipeline notifications
- Transforming processed data into meaningful visualizations
- Organizing the project for portfolio presentation

These challenges provided practical experience in building, testing, and troubleshooting a cloud-based data pipeline.

---

Future Enhancements

Enhancement| Description
Advanced monitoring| Add CloudWatch alarms and dashboards for pipeline health
Automated data-quality monitoring| Track rejection rates and data-quality metrics
Interactive dashboard| Add filtering by date, country, product, and customer
Live dashboard connectivity| Connect the dashboard directly to the database
Amazon QuickSight| Build a managed business intelligence dashboard
AWS Glue| Introduce managed data cataloging and ETL capabilities
Amazon Athena| Enable SQL-based analytics directly against S3 data
CI/CD| Automate deployment and testing through GitHub Actions

---

Key Learning Outcomes

AWS Cloud Skills

- Amazon S3
- AWS Lambda
- Amazon RDS
- Amazon SNS
- AWS IAM
- Cloud-based data pipeline architecture

Data Engineering Skills

- Data ingestion
- Data validation
- Data cleaning
- Data transformation
- Rejected-record handling
- Relational database storage
- Pipeline monitoring and notifications
- Data visualization
- KPI development

Professional Skills

- Cloud architecture design
- Troubleshooting AWS services
- Technical documentation
- GitHub repository management
- Portfolio project development

---

Conclusion

The AWS Sales Data Pipeline demonstrates how AWS cloud services can be combined to create a practical sales data processing solution.

The pipeline processes raw online retail data, validates individual records, separates accepted and rejected data, stores processed records in Amazon RDS, provides SNS notifications, and presents business insights through a Sales KPI Dashboard.

The project provides hands-on experience with serverless computing, cloud storage, relational databases, data validation, event-driven notifications, and data visualization.

---

Author

Faith Ogundusi

Data Engineer | AWS Cloud | Building Data Pipelines & Scalable Data Solutions

""LinkedIn" (https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin&logoColor=white)" (https://www.linkedin.com/in/faith-ogundusi)

""GitHub" (https://img.shields.io/badge/GitHub-Follow-181717?style=flat&logo=github&logoColor=white)" (https://github.com/faith-ogundusi)

---

Project Repository:
https://github.com/faith-ogundusi/aws-sales-data-pipeline
