# zoho_crm_culturalinfusion
This project implements a secure, automated, and low-cost serverless data pipeline that extracts CRM data from Zoho CRM, transforms it in AWS, and delivers weekly refreshed analytics dashboards in Amazon QuickSight. This solution bridges the gap using a lightweight AWS ETL architecture that removes manual exports, reduces reporting errors, and ensures consistent, up-to-date sales insights. 
# Business Objectives 
- Improve reporting accuracy and timeliness
- Eliminate manual CSV exports and spreadsheet-based reporting
- Provide management with a unified view of sales performance
- Enable weekly decision-making using reliable analytics
- Maintain strong security and access control over CRM data

# High-Level Architecture 
Data Flow
Zoho CRM (REST API) -> AWS Lambda (ETL, Python) -> Amazon S3 (Analytics Data Lake) -> AWS Glue Data Catalog -> Amazon Athena (SQL) -> Amazon QuickSight (Dashboards)
- Event-driven & scheduled using Amazon EventBridge
- Serverless (no EC2, no servers to manage)
- Incremental loads using Zoho “last_modified_time”
  
# Tools & Technologies 
- Python
- SQL
- Zoho CRM API
- AWS Services

# End-to-End Pipeline Flow

1. EventBridge triggers the ETL Lambda function once every weekend
2. AWS Lambda:
- Reads Zoho OAuth credentials from AWS Secrets Manager
- Exchanges refresh token for access token
- Fetches only records modified since the last successful run
- Handles pagination and API rate limits
- Cleans, normalises, and flattens JSON responses
3. Cleaned data is written to Amazon S3 Analytics bucket
4. AWS Glue Crawler detects schema changes and updates the Data Catalog
5. Amazon Athena queries S3 data and builds analytics-ready tables
6. Amazon QuickSight refreshes dashboards automatically
7. Amazon CloudWatch logs execution, errors, and performance metrics

## AWS Architecture Diagram 
![image](https://github.com/delwynluu/zoho_crm_culturalinfusion/blob/18b886ac29b872751bf7064774c9e86b41faaef9/AWS%20Architecture%20Diagram)
