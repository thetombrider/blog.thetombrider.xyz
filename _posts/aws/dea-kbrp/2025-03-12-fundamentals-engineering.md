---
title: "Data Engineering on AWS: Foundations"
layout: post
date: 2025-03-12
categories: [aws]
tags: [data, data engineering, notes]
---

## Foundations - Roles and Concepts

There are many people in an organization who are involved with data. These are the main roles that can be found in an organization with their respective responsibilities and areas of interest.

| Personas              | Responsibility                                                                 | Areas of Interest |
|-----------------------|-----------------------------------------------------------------------------|-------------------|
| Chief Data Officer (CDO) | Builds a culture of using data to solve problems and accelerate innovation | Data quality, data governance, data and artificial intelligence (AI) strategy, evangelizing the value of data to the business |
| Data Architect        | Driven to architect technical solutions to meet business needs, focuses on solving complex data challenges to help the CDO deliver on their vision | Data pipeline, data processing, data integration, data governance, and data catalogs |
| Data Engineer        | Delivers usable, accurate datasets to the organization in a secure and high-performing manner | The variety of tools used for building data pipelines, ease of use, configuration, and maintenance |
| Data Security Officer | Ensures that data security, privacy, and governance are strictly defined and adhered to | Keeping information secure, complying with data privacy regulations, protecting personally identifiable information (PII), and applying fine-grained access controls and data masking |
| Data Scientist       | Constructs the means for quickly extracting business-focused insight from data for the business to make better decisions | Tools that simplify data manipulation and provide deeper insight than visualization tools and tools that help build the machine learning (ML) pipeline |
| Data Analyst        | Reacts to market conditions in real time, must have the ability to find data and perform analytics quickly and easily | Querying data and performing analysis to create new business insights and producing reports and visualizations that explain the business insights |

## Data discovery

Data discovery refers to the process of finding and understanding relevant data sources within an organization and the relationships between them. It is a crucial first step for extracting value from data assets. 

Data discovery is an important prerequisite to architecting and deploying a data analytics system, but it's also an ongoing process. 

Steps:

1. Define Business Value:
    - Conduct data discovery kick-off workshops with stakeholders to understand business goals, prioritize use cases, and identify potential data sources. 
2. Identify your data consumers:
    -     Who are the end users (for example, business analysts, data engineers, data analysts, or data scientists)? 
    - Which insights are you currently getting from your data?
    
    - Which tool or interface do your data consumers use?
3. Identify data sources:
    - Research the different internal and external sources where data is generated and stored. This includes databases, applications, and files. 
4. Define storage, catalog and access needs: Determine the best storage for specific data types. Assess data quality to determine processing needs. Catalog and register details about data sources.
5. Define processing needs: Extract relevant data from sources like databases, data lakes, and CRM systems using tools such as AWS Glue crawlers or custom scripts. Curate and transform the raw data as needed using services like AWS Glue and Amazon EMR.

## AWS Data Services and the Modern Data Architecture

Within organizations, teams often build data solutions in isolation and have their own data ingestion, storage, management, and governance layers.

To avoid these challenges, you must build a modern data architecture for analytics and insights that breaks down all data silos—including third-party data. This architecture creates end-to-end governance and puts the data in the hands of everyone in the organization.

A Modern Data Architecture covers the following phases:

1. Ingest
    - To ingest data, AWS offers a variety of services including DMS, Data Firehose, MSK (Managed Streaming for Kafka), IoT Core, Data Sync, Transfer Family, Snow Family
2. Store
    - Before you can ingest data, you need a place to put it, therefore a modern data architecture starts with the data lake. A data lake is a centralized repository that you can use store structured, semi-structured, and unstructured data at scale. Amazon S3 provides an optimal foundation for a data lake because of its virtually unlimited scalability and high durability.
3. Catalog
    - An essential component of a data lake built on Amazon S3 is the data catalog. Organizations can use cataloging to keep track of data assets and understand what data exists, where it is located, its quality, and how it is used. A data catalog is designed to provide a single source of truth about the contents of the data lake. 
    - AWS Glue Data Catalog creates a catalog of metadata about your stored assets. Use this catalog to help search and find relevant data sources based on various attributes like name, owner, business terms, and others.
4. Process
    - After the data is cataloged, it can now be processed or transformed into formats that are more useful for analysis and insights. Transformation can include data type conversion, filtering, aggregation, standardization, and normalizing.
    - AWS offers various processing services:
        - AWS Glue, a fully managed ETL service to build ETL pipelines
        - Amazon EMR, a managed big data solution that allows to use open-source frameworks. 
        - Amazon Managed Service for Apache Flink
5. Deliver
    - Transformed data is delivered to consumers and stakeholders, such as data scientists, data analysts, and business analysts. 
    - Many AWS services can be used at this stage:
        - Redshift: a data warehouse with analytics capabilities
        - Athena: query engine to analyze data in S3
        - EMR: to run Spark, Hive, Presto and Flink analytics frameworks on data stored in S3 or other AWS services.
        - OpenSearch Service: Deploy, operate, and scale OpenSearch clusters in the AWS Cloud. 
        - QuickSight: Visualize and analyze large datasets using SQL, charts, graphs, and dashboards
        - SageMaker: Build, train, and deploy machine learning models for use in predictive analytics, computer vision for image recognition, natural language processing, recommendation systems, and more.
6. Security and Governance
    - Security in data analytics systems refers to measures taken to protect data from unauthorized access, breaches, or attacks.
    - Governance encompasses the policies, procedures, and processes that ensure the proper management, quality, and use of data. 

    Some AWS services related to Security and Governance are:
    - Lake Formation: With Lake Formation, you can centrally manage and scale fine-grained data access permissions and share data with confidence within and outside your organization.
    - IAM: IAM manages fine-grained access and permissions for human users, software users, other services, and microservices.
    - Key Management Service: Use AWS KMS to create and control data encryption keys for data at rest and in transit.
    - Macie: automatically discover, classify, and protect sensitive data in AWS, such as personally identifiable information (PII).
    - DataZone: catalog, discover, share, and govern data stored across AWS, on premises, and third-party sources.
    - Audit Manager: Audit Manager continuously audits usage to assess risk and compliance with regulations and industry standards.

## Orchestration and automation

Without efficient coordination and automation, data pipelines can become fragmented, error-prone, and time-consuming to manage. Additionally, scaling these processes to handle growing volumes of data can be daunting. 

Orchestration and automation can help solve these problems. 

- Orchestration is the process of coordinating multiple services to define and manage the flow of data through a series of steps. It involves defining workflows and dependencies between steps. 

- Automation refers to using tools and services to automate repetitive tasks related to data ingestion, processing, and analytics. 

AWS offers many automation and orchestration services: 
- Step Functions: Step Functions is a visual workflow service to orchestrate and automate workflows, pipelines, and processes. Step Functions ensures tasks run in the correct order.
- Lambda: Lambda runs code (called Lambda functions) without provisioning or managing servers. Combined with Step Functions, Lambda functions can invoke AWS services and microservices and perform tasks to that are part of orchestrated workflows.
- MWAA: Amazon Managed Workflows for Apache Airflow (Amazon MWAA) can be used to orchestrate data analytics workflows on AWS. 
- EventBridge: Amazon EventBridge is a serverless service used to build event-driven applications. It employs loosely coupled applications that work together by emitting and responding to events. 
- SNS: Amazon Simple Notification Service (Amazon SNS) is a fully managed messaging service. With Amazon SNS, applications and services can send messages to multiple endpoints simultaneously through SNS topics. 
- SQS: Amazon Simple Queue Service (Amazon SQS) is a managed message queuing service to send, store, and retrieve multiple messages of various sizes asynchronously. 

### Enhancing orchestration and automation

Two technologies can make orchestration and automation even more effective in data analytics workflows: Zero-ETL and serverless architectures.

### Zero-ETL

Zero-ETL refers to an approach for data integration that minimizes or eliminates the need for ETL processes. 
With zero-ETL integrations, data can be directly queried from its original sources without requiring data movement or transformation.

Several AWS services support zero-ETL and can be used in orchestrated workflows:
- Athena: With Athena, data stored in Amazon S3 can be queried by using SQL commands. It does not need to be extracted and loaded elsewhere. Step Functions can orchestrate Lambda functions to process and analyze the query results from Athena in real time. 
- Redshift Streaming ingestion: Amazon Redshift ingests streaming data in near real time at high throughput. Because it doesn't need to stage in Amazon S3, the need for some ETL tasks is eliminated
- Aurora with Redshift: Replicate data from some Aurora sources to Amazon Redshift in near real time for analytics. Zero-ETL seamlessly makes that data available in Amazon Redshift and removes the need to build and maintain complex ETL pipelines. 
- Redshift autocopy from S3: Continuously ingest new data files from Amazon S3 into Amazon Redshift with no manual intervention.
- OpenSearch Service: OpenSearch Service has zero-ETL integration with Amazon S3 for querying data directly in Amazon S3 without extracting to OpenSearch.

### Serverless Architectures

A serverless architecture is a way to build and run applications and services without having to manage infrastructure. Your application still runs on servers, but all the server management is done by AWS. Serverless architectures are extremely cost effective because you only pay for the actual time that your code is running.

Many AWS services support this paradigm, including: 
- Lambda
- API Gateway
- DynamoDB
- S3
- SNS
- SQS
- Redshift Serverless
- EMR Serverless
- AWS Glue
- MSK Serverless
- OpenSearch Service Serverless

## Security

Security should cover 5 areas:
- Access Management: Strong access controls are important to ensure only authorized users and applications can access analytics resources and data.
- Regulatory Compliance: Many regulations like GDPR and HIPAA mandate that organizations securely manage data and adhere to privacy and security best practices.
- Sensitive data protection: Data analytics often involves large volumes of sensitive data such as Personally Identifiable Information (PII), financial records, and health records. These must be protected from unauthorized access, theft, or leakage. 
- Data and network security: AWS services like security groups, network access control lists, and firewalls help restrict network access and secure compute and storage resources. Features like encryption-at-rest provide added protection.
- Data auditability: It is essential to be able to track the origin, transformation, and flow of data from source to target. You need to know where the data came from, how it was processed, and who and what systems have access to it. 

## Monitoring

Monitoring is crucial for maintaining the reliability, availability, and performance of AWS data analytics workflows. 

The following are a few key aspects that should be monitored:

- Resources
- Analytics jobs
- Data pipelines
- Data access


https://docs.aws.amazon.com/pdfs/architecture-diagrams/latest/modern-data-analytics-on-aws/modern-data-analytics-on-aws.pdf#modern-data-analytics-on-aws

https://docs.aws.amazon.com/pdfs/prescriptive-guidance/latest/modern-data-centric-use-cases/modern-data-centric-use-cases.pdf#data-engineering-principles

