# Porfolio
Greetings! My name is Neil, a data enthusiast. Welcome to my Github repository showcasing a compilation of projects reflecting my journey and expertise in the realm of business intelligence and data engineering. Within this repositoy, you will find a diversity of projects I have put together throughout my data professional career, from building robust data pipelines, designing databased to crafting insightful business dashboards. Wether you're a fellow data enthusiast, a potential employer, or simply curios about the possibilities of data, please feel free to explore and reach out with any questions or opportunities for collaboration. 🙂

## I. TICKETING PLATFORM DATA PIPELINES
### 1. Background:
This is a project I did for a company specializing in online ticket sales, catering to sports and recreational events. While the initial database architecture effectively supported the platform's backend operations, this setup wasn't designed with analytical purposes in mind. Not only did data were stored scatteringly, but also the naming convention was a disaster. This lack of a standard data model hindered the company's ability to analyze the data and derive meaningful insights from it. 

**`In a nutshell, my mission was to reshape the data and make it usuable for analytics`**. 

### 2. Objectives:
#### Objective 1: Put together an OLAP database which: 
- stakeholders can run ad-hoc queries against.
- is the data source of the business dashboard.
- is the foundation to build a CRM system.
#### Objective 2: Build a robust and automated data pipeline that refreshes the data on a daily basis.
#### Objective 3: Build a business dashboard which:
- tracks daily sales performace by monitoring sales KPIs and key financial metrics.
- presents an analysis of customers behaviour and segmentation.
  
### 3. Constrains & Challenges:
It's worth metioning the constraints and challenges I encountered before and during the project because they are the decisive factors of the approach I adopted.

First among them was the dependency on the head DevOps of the company for the access to the raw data. In particular, I was restricted from directly acessing the company's transactional database stored in MySQL. Instead, the head DevOps would dump each entire table from the database into JSON files, before uploading them to an AWS S3 bucket and overwriting the existing files. This constrain made micro-batch processing and incremental loading almost impossible. I needed to come up with a workaround that had to be memory-efficient and scalable when the size of those JSON files grew.

The second most significant constrain I encountered was that the new data would only arrive in the S3 bucket once a day at midnight, so theoretically the data I would receive was only up to 23:59:59 the day before. This was definitely something I had to work with the stakeholders to manage their expectations.

Last on the list is the communication with the stakeholders, which is a common challenge faced by many other data engineers.  

### 4. Approach:
#### EXTRACT:
##### As mentioned above, the data source I was working with is a collection of JSON files in an AWS S3 bucket, some of them were heavily nested. I had two options:
- Build a fully managed pipeline with AWS Glue and AWS Crawler, then create a databse using AWS Athena. Or if I had wanted to have more flexibility, I could have built used AWS Lambda function.
- Code a pipeline with Python and open-source tools.
##### I did try both of them, and finally decided to go the second option because:
- I was going to use Power BI to build a business dashboard from the cleaned data, and set up a daily schedule refresh to automatically refresh the dashboard underlying dataset. To achieve this, I needed to either install the Power BI gateway on the host operating system (OS) to which I would later deploy my pipeline or utilize a cloud-based data source such as Google BigQuery or Snowflake. Unfortunately, the Power BI gateway is only compatible with Windows OS, whereas my pipeline would be containerized within a Docker container running on Linux. Consequently, I had to opt for a serverless data warehouse as the target database for this project. While I favor Athena for its robust distributed Presto SQL engine, I had to exclude it from consideration in this case. This decision was due to Power BI's limitation of connecting to Athena solely via an ODBC driver installed locally, necessitating the installation of a Power BI gateway for scheduling daily refreshes.
#### LOAD:
#### TRANSFORM:
### 5. Technologies, Tools, and Frameworkes:
This project leverages a variety of open-source technologies (Dagster and dbt) and cloud services (GCP, AWS and Azure), with Python and SQL being the major programming languages. The final application is running on Docker to ensure scalability.

![activeTix](https://github.com/khoinguyenvo/Porfolio/assets/133230440/c5faa94d-b56d-4d25-a8dc-d874f25af15c)

### 6. Github repository:
[Project 1 - Online Ticketing Platform - Data Pipeline](https://github.com/khoinguyenvo/Porfolio/tree/43fd579549de6aa6ee7cce5cc29fddbea419636d/Project%201)
