---
title: "Fundamentals of Analytics on AWS: Part 1"
layout: post
date: 2025-03-13
categories: [aws]
tags: [data, data engineering, notes]
---
## Analytics Concepts

Data analysis is the process of analyzing a dataset to make decision. It is a subset of Data Analytics, which is the broader effort of an organization to extract value from data through gathering and analysis of data.

### Analytics

There are 4 types of analytics:

- **Descriptive**: focus on summarizing historical data. Insight into trends and patterns. --> Data visualizaitons.
- **Diagnostic**: Diagnostic analytics is characterized by techniques, such as drill-down, data discovery, data mining, and correlations. In each of these techniques, multiple data operations and transformations are used for analyzing raw data. This form of analytics provides insights and requires human judgment to turn those insights into actionable information.
- **Predictive**: This type uses historical data and statistical algorithms to make forecasts about future outcomes. Predictive analytics is characterized by techniques, such as machine learning, forecasting, pattern matching, and predictive modeling.
- **Prescriptive**:  This technique is based on predictive analytics, but goes one step further and actually recommends actions or responses to the predicted outcome. Prescriptive analytics can analyze the potential implications of different choices and then suggest the best course of action based on those different scenarios. It is characterized by machine learning, graph analysis, simulation, complex event processing, neural networks, and recommendation engines.

### Machine Learning

Definitions:

- **Artificial intelligence (AI)** : A broad branch of
  computer science that is involved with building smart machines that can perform tasks requiring human intelligence.
- **Machine learning (ML) model** : A computer program that is designed to find patterns from an unanalyzed dataset. ML is a subset of AI. Computers use ML to learn from and make
  predictions based on data. ML models can forecast what might happen in the future (predictive analytics) and provide a course of action (prescriptive analytics).
- **ML algorithm** : A computer program that helps
  computers understand hidden patterns in data, make predictions about the data, and recommend actions to take. ML algorithms can analyze huge volumes of data much faster than humans.

Generative AI on AWS

Generative AI is a type of ML model that creates new content and ideas from user prompts. Generative AI learns from existing data
and then uses that knowledge to create new, original content. It is done through a type of ML called deep learning, which uses algorithms to mimic the structure of the human brain. These algorithms, called
artificial neural networks, are inspired by the biological neurons of the human brain and are able to learn complex patterns from data.

Generative AI is powered by large, pre-trained models called foundation models. Generative AI models are trained on massive amounts of data, which can be anything from text to images to music. The model learns the patterns and structures of the data. It then uses that data to make predictions about what the content should look like, similar to the data it was trained on.

### 5 V of Big Data

Definitions

- **Big data:** Data that is stored rapidly from various sources, massive in size, and is complicated for organizations to secure, analyze, and gain valuable insight from.

#### Volume

Every organization's infrastructure has to support large amounts of scalable and durable data storage and must also be able to gather this data from many different sources. 

#### Variety

Data can assume various source types:
- Structured
  - Relational DBs
- Semistructured
  - NoSQL DBs
- Unstructured
  - Files

##### Row-based and columnar data storage

Data within a database should be indexed to allow a query to quickly find the data it needs to produce a result. Indexes control the way data is physically stored on disk. They physically group records into a predictable order based on the key values within the table. This plays a huge part in the speed and efficiency of queries.

Both OLTP and OLAP systems can use either indexing method. However, there are advantages to choosing the method that is best suited to the types of queries that will be run the majority of the time.

Row based is better for transactional systems with random reads and returning full rows, while columnar storage is best for analytical processing and sequential reads and returning aggregations of column values.

#### Velocity

There are four velocities for processing data:
- Scheduled
  - Scheduled batch processing represents data that is processed in a very large volume on a regularly scheduled basis. For instance, once a week or once a day. It is generally the same amount of data with each load, making these workloads predictable.
- Periodic
  - Periodic batch processing is a batch of data that is processed at irregular times. These workloads are often run after a certain amount of data has been collected. This can make them unpredictable and hard to plan around.
- Near real-time
  - Near real-time processing represents streaming data that is processed in small individual batches. The batches are continuously collected and then processed within minutes of the data generation.
- Real-time
  - Real-time processing represents streaming data that is processed in very small individual batches. The batches are continuously collected and then processed within milliseconds of the data generation.

#### Veracity

##### Data integrity 

Data changes over time. As it is transferred from one process to another, and through one system to another, there are opportunities for the integrity of the data to be negatively impacted. You must ensure that you maintain a high level of certainty that the data you are analyzing is trustworthy. Data veracity is contingent on the integrity of the data. Data integrity is all about making sure your data is trustworthy. You need to make sure it has integrity, and that the entire data chain is secure and free from compromise. 

##### Transforming data with the ETL process

Extract, transform, and load (ETL) is the process of collecting data from raw data sources and transforming that data into a common type. This new data is loaded into a final location to be available for analysis and inspection.

The purpose of the ETL process is as follows:
- To ensure the data has the required accuracy, precision, and depth
- To bring together data from different sources to gain a complete picture
- To build purpose-built data sets to answer key business questions

##### ELT Process Steps

In modern cloud-based environments, the extract, load, and transform (ELT) approach loads data as it is. It then transforms it at a later stage, depending on the use case and analytics requirements. 

The steps are similar to those in the ETL process, performed in a different order, but with similar results.

The ELT process requires more definition at the beginning. Analytics must be involved from the start to define target data types, structures, and relationships.

These are the three steps of ELT:

- Extract raw data from various sources.
- Load it in its natural state into a data warehouse or data lake.
- Transform it as needed while in the target system.

With ELT, all data cleansing, transformation, and enrichment occur within the data warehouse. You can interact with and transform the raw data as many times as needed

#### Value

##### Querying and reporting

Analytical reporting is used to transform data into actionable information that empowers organizations to make informed decisions, optimize processes, and achieve strategic objectives.

Analytics exists to help you get the most value and useful insights from raw data. With reporting tools, you can create visual representations of data, such as charts, graphs, and dashboards. Visualization makes complex data more accessible and understandable, helping users quickly identify trends, patterns, and anomalies. 
