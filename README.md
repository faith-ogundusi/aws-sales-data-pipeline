AWS Sales Data Pipeline

"AWS" (https://img.shields.io/badge/AWS-Cloud-FF9900?style=flat&logo=amazonaws&logoColor=white)
"Python" (https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)
"Amazon S3" (https://img.shields.io/badge/Amazon_S3-Storage-569A31?style=flat&logo=amazons3&logoColor=white)
"AWS Lambda" (https://img.shields.io/badge/AWS_Lambda-Serverless-FF9900?style=flat&logo=awslambda&logoColor=white)
"Amazon RDS" (https://img.shields.io/badge/Amazon_RDS-MySQL-527FFF?style=flat&logo=amazonrds&logoColor=white)
"Amazon SNS" (https://img.shields.io/badge/Amazon_SNS-Notifications-FF4F8B?style=flat&logo=amazonsns&logoColor=white)

Project Overview

The AWS Sales Data Pipeline is a cloud-based data engineering project that processes online retail sales data using AWS services.

The pipeline ingests raw sales data, validates and separates records into valid and rejected datasets, stores accepted records in Amazon RDS, sends pipeline notifications through Amazon SNS, and presents business insights through a Sales KPI Dashboard.

Business Problem

Businesses need reliable ways to process large volumes of sales data while identifying invalid records and making sales information available for analysis.

Manual processing can be time-consuming and may make it difficult to maintain organized data and generate timely business insights.

Proposed Solution

A serverless AWS data pipeline was implemented to automate the main stages of sales data processing:

Raw Sales CSV
     │
     ▼
 Amazon S3
     │
     ▼
 AWS Lambda
 Validation & Processing
     │
     ├──────────────► Rejected Records ──► Amazon S3
     │                                      │
     │                                      └──► SNS Alert
     │
     └──────────────► Valid Records ─────► Amazon S3
                                            │
                                            ▼
                                       Amazon RDS
                                            │
                                            ▼
                                  Sales KPI Dashboard

                     AWS Lambda ─────► Amazon SNS
                                      Completion Alert

Architecture

The detailed AWS architecture diagram illustrates the flow of data between the storage, processing, database, notification, and visualization components.

Architecture diagram: "architecture/aws-sales-data-pipeline-architecture.png"

«The architecture diagram will be added to the repository as part of the project documentation.»

AWS Services Used

Service| Role in the Pipeline
Amazon S3| Stores raw, valid, and rejected sales data
AWS Lambda| Performs serverless data validation and processing
Amazon RDS| Stores accepted sales records in MySQL
Amazon SNS| Sends pipeline completion and alert notifications
AWS IAM| Manages access and permissions for AWS resources

Dataset

The project uses the Online Retail Dataset, containing transactional sales records from a UK-based online retailer.

Key fields include:

- Invoice number
- Stock code
- Product description
- Quantity
- Invoice date
- Unit price
- Customer ID
- Country

Revenue calculation:

"Revenue = Quantity × UnitPrice"

Pipeline Results

The pipeline processed 50,000 sales records.

Result| Records| Percentage
Valid / Accepted| 30,315| 60.6%
Rejected| 19,685| 39.4%
Total| 50,000| 100%

Validation rules included checks for:

- Missing required values
- Zero or negative quantities
- Zero or negative unit prices

Accepted records were stored in Amazon RDS, while rejected records were retained separately for review.

Sales KPI Dashboard

A Sales KPI Dashboard was created using the accepted pipeline data.

Dashboard: "visualizations/dashboard.html"

The dashboard presents:

- Revenue KPIs
- Order trends
- Top products by revenue
- Top products by quantity
- Revenue by country
- Top customers
- Sales trends over time

The dashboard provides a visual summary of the processed sales data and supports business-focused analysis.

Repository Structure

aws-sales-data-pipeline/
│
├── data/
│   ├── raw/
│   ├── valid/
│   └── rejected/
│
├── visualizations/
│   └── dashboard.html
│
├── LICENSE
└── README.md

Key Benefits

- Automates sales data processing and validation
- Separates valid and rejected records
- Uses scalable cloud storage with Amazon S3
- Uses serverless processing with AWS Lambda
- Stores structured data in Amazon RDS
- Provides pipeline notifications through Amazon SNS
- Converts processed data into useful business visualizations

Key Learning Outcomes

This project provided hands-on experience with:

- AWS cloud architecture
- Amazon S3
- AWS Lambda
- Amazon RDS
- Amazon SNS
- AWS IAM
- Data validation and processing
- Data pipeline design
- Data visualization
- GitHub project documentation

Author

Faith Ogundusi

Data Engineer | AWS Cloud | Building Data Pipelines & Scalable Data Solutions

"LinkedIn" (https://www.linkedin.com/in/faith-ogundusi) · "GitHub" (https://github.com/faith-ogundusi)

---

Project Repository: "github.com/faith-ogundusi/aws-sales-data-pipeline" (https://github.com/faith-ogundusi/aws-sales-data-pipeline)
