## Task 4: Deployment, Databases, Governance & Security

## Deployment and Automation:

### Amazon CloudFront:
- Amazon CloudFront which is a content delivery network (CDN)
- It caches content like videos and audios
- Improves performance of content for users
- Can distribute content to various locations around the world
- Use distribution, orgin and caches around the world
- Uses AWS global network for low latency and high performance
- Delivers both static and dynamic content
- Uses https and security protocols/ protection

### AWS Global Acelerator:
- Users that want to access an application which is in 2 regions under a load balancer
- DNS/ route 53 finds routes to domain name and returns 2 ip addresses since there are 2 regions available
- User traffic is directed to closest edge location
- Global accelerator listens to the IP address and chooses where to forward the traffic using AWS global network
- if one region fails, the application will be distrubted from the other ip address
- Useful for non-https use cases such as gaming, iot, 

### CloudFormation:
- Tool to define architecture built on AWS
- Using a code text file and deploy the infrastructure globally
- Code can be in either JSON or YAML 
- Builds infrastructure on AWS based on the definitions in the code template
- Can deploy everything in AWS using cloudformation
- Can reuse cloud infrastructure
- Create stacks for deploying
- Can update stacks to implement changes in our template file
- If we delete stack, cloudformation will also terminate

### Create and Update Stacks using CloudFormation:
Create an EC2 instance with security group for SSH access -
1. Search for EC2 on the Console -> Launch instance with amazon linux as AMI and copy the AMI ID but don't create instance
2. Search for CloudFormation Console 
3. Create Stack with -
    - Prepare template using your own template, sample template or design a visual template
    - Can upload a template JSON or YAML file if you are using your own template
    - Use AMI ID copied in the template file as AMI image id. This is to direct to the EC2 instance to attach security group. 
    - Upload the template file with AMI image id
    - Add stack name
4. View cloudformation events as it follow the code template and Create an EC2 instance with security group for SSH access
5. Can update or change template by changing stack actions to 'create change set for current stack' and click 'replace current template' and upload new file. Will show the changes before updating.
6. Deleting stack will delete all resources created 

### AWS Cloud development kit (CDK):
- Service provides a framework to define cloud application resources using programming languages
- Provision resources using AWS CloudFormation
- download pre-configured application components, model infrastructure using programming language, deploy with aws cloudformation

### AWS Elastic Beanstalk:
- Platform as a service solution
- Developer just has to Upload source code as a zip file to elastic beanstalk and deployment will be managed automatically
- Beanstalk will then create the Elastic Beanstalk environment which can include an auto scaling group with instances inside and a load balancer to distribute traffic
- Cannot create VPC
- Supports many platforms and uses core AWS services
- Manage health of applications


### AWS Developer Tools:
- Used in continuous integration and continuous delivery
- Continuous integration - code commit service is similar to github and can be collaborate with other developers. code build service can build and test code. Updates can be made and this process is continuous. Jenkins is similar to code build service.
- Continuous delivery - after code is succesfully tested, code deploy service will deploy the code to the applications. Ansible is similar to code deploy service.
- AWS code pipeline connects these 3 services 
- CodeStar service to connect ide and codestar would work with different aws developer tools (the 3 code servives, cloud formation) to build the application automatically.

### AWS Cloud 9:
- Intergrated development environment (IDE)
- Editor to write, run and debug code
- Provides collaboration features
- Range of debugging tools
- Integrates with AWS services like aws lambda,EC2, code pipeline
- Create an environment 

### AWS AppConfig:
- Service to create, manage and deploy application configurations
- Capability of AWS Systems manager
- Seetungs that influence behaviour of the application
- Can host applications on EC2, lambda, mobile apps, iot devices
- reduce errors with configurations

### AWS X-Ray:
- Service that collects data about application requests
- Provides tools like viewing, filtering and gaming insights
- helps with end-toend tracing
- Supports other AWS services
- Real-time debugging and monitoring
- Easy tracking of user requests across the application
- Improves performance
- Reduce downtime by removing data silos which makes it easier to diagnose and solve issues
- Cost efficiency
- trace data analytists and identify root causes
- Integrations with services like MySQL, PostgreSQL, DynamoDB, SQS/SNS

## Databases and Analytics:

### Database Types and Use Cases:
Types:-
1. Relational databases -
    - Data is organised by tables, rows and columns
    - Uses SQL rules
    - SQL provided tools to insert, update, delete, query data
    - Scale vertically
    - Supports complex queries and joins
    - Eg: Amazon RDS, Oracle, MySQL, PostgreSQL

2. Non-relational databases -
    - Veried data storage models
    - Flexible schema (NoSQL) - data stored in key value pairs, columns, documents or graphs
    - rules can be defined outside database in the application
    - Scales horizontally
    - Unstructured
    - has primary key and attributes. Attributes can be missing or have different data types since it does not have a rigid schema
    - Eg: Amazon DynamoDB, MongoDB, Redis

3. Graph Databases -
    - Store, manage and navigate relationships between data
    - Used in facebook to find connection between people
    - uses nodes to represent entities
    - edges to represent relationships
    - properties to store information about nodes and edges
    - Eg: Amazon Neptune

4. Operational/Transactional Databases -
    - Online transaction processing databases (OLTP)
    - Can be used to add customer records, checking stock 
    - Short transactions and simple queries
    - Eg: Amazon RDS, Oracle, MySQL
    - Can use non-relational databases like mongodb, cassandra

5. Analytical Databases - 
    - Online Analytics processing databases
    - Source data will come from OLTP
    - Collect data and using complex queries like finding trends
    - Eg: Amazon RedShift, Teradata, HPVeritica
    - NR Eg: Amazon EMR, MapReduce

### Amazon Relational Database Servive (RDS):
- Managed  Relational Database Servive
- Used for Online transaction processing (OLTP)
- Runs on Amazon EC2 instance. Must choose DB instance type
- RDS uses EBS Volumes for storage like other EC2
- Backups can be taken using snapshots
- Amazon RDS offers different database engines:
    - Amazon Aurora (MySQL and PostgreSQL)
    - MYSQL
    - PostgreSQL suports both relational and non-relational query
    - Oracle
    - Microsoft SQL
    - MariaDB which is a community developed fork for MySQL and is free 
- Can scale up by changing to bigger instance type with higher cpu and memory
- Can scale out to write to a primary RDS and reads from a read replica 
- Can replicate a Standy from a RDS primary in another AZ which helps with disaster recovery

### Amazon Aurora:
- AWS database that is offered in Amazon RDS 
- Compatible with MySQL and PostgreSQL
- Faster than standard MySQL and PostgreSQL databases
- Has features such as fault-tolerant, self-healing, auto-scaling up storage system
- Replicas are used to read data and are in the same region
- High permformace

### Amazon DynamoDB:
- Non-relational database service
- managed NoSQL database and serverless service
- Low latency access to data
- Dynamo Streams records the changes made in the databases

### Amazon RedShift:
- Data Warehouse
- Source data comes from OLTP
- Online Analytics processing
- Can analyse data with BI tools such as QuickSight using SQL
- Relational database
- Uses Amazon EC2 instances. Should choose an instance type and family
- Keeps 3 copies of the data
- provides continuous and incremental backups

### Amazon Elastic Map Reduce (EMR):
- Provides managed implementation of Hadoop to process big data
- Managed cluster platform that simplifies running big data frameworks like Hadoop
- Used for processing data for analytics and business intelligence
- Tranform and move large data
- Extract, tranform and load

### Amazon ElastiCache:
- Database service for memory caching of data
- High performance
- Low latency
- Infront of other databases such as RDS and DynamoDB using elasticache Node 
- Nodes run on EC2 instance so should be set up
- Used in web session store, database caching, leaderboards

### Amazon MemoryDB for Redis:
- Redis compatible
- Durable, in-memory database service
- Fast performance
- Stored in memory
- durable across multiple AZs
- combines DB and caching
- Strong consistency 

### Amazon Athena and AWS Glue:
- Serverless service used to run SQL queries against data
- Query data in S3
- Can connect to lambda
- data can be in CSV, JSON, Parquet etc.
- AWS Glue to store info and schemas about databases and table
- Optimise Athena by patitioning your data, bucket partitioned data, use compresion, optimise file sizes, optimise ORDER BY and GROUP BY, include only nescessary columns

### Amazon Kinesis:
- Used often for streaming data
- data is ingested into data streams
- can process through analytics
- can firehose or load data into another destination like S3 bucket
- can query data in bucket with athena
- can load into redshift or other services
- can use BI tools like QuickSight
- provides real-time SQL processing

### Amazon OpenSearch Service:
- AKA Elastisearch
- Service to search, visualise and analyse text and unstructred data 
- Secure, can deploy into Amazon VPC and integrate with IAM
- Highly available and scalable
- Suports SQL queries
- Integrates with open source tools
- Scale by adding or removing instances
- Upto 3 AZ
- Deploy by creating a cluster in CLI, specify no. of instances and instance types, choose storage options. 
- Clusters can be deployed in VPC for more security
- Best to deploy data instances across 3 AZ
- Use data in cluster to search and analyse it
- Data gets ingested from other sources. eg: Amazon Kinesis data firehose
- Can use Kibana Dashboard at the opensearch service
- ELK Stack combines Elasti search, Logstash, Kibana services

### AWS Data Exchange:
- Can publish products, get subscriptions
- Can update products
- Receives reports
- Connects to data sets given by third-party providers and call API endpoint
- Allows secure exchange and use of data products/data sets
- Providers publish data into AWS Dataexchange and subscribers get access to the data products
- Enhances BI, analytics and machine learning models
- Exchange data for S3

### Amazon MSK:
- Service that enables you to build and run applications that uses Apache Kafka to process streaming data
- Used to ingest and process stream data in real-time
- Used to create, update and delete clusters
- Can use data plane operations to produce and consume data 
- Components include Kafka clusters, broker nodes, zookeeper nodes, producers, consumers, topics

### Other Databases and Analytical Services:
- AWS Data pipeline used to process and move data between AWS compute and storage services 
- Amazon QuickSight - BI service to create BI dashboard for machine learning powered insights displayed
- Amazon Neptune - Graph database 
- Document DB - Document database service and supports mongoDB, queries and indexes JSON data
- Amazon QLDB- Ledger database for immutable change history and transaction logging
- Amazon Managed Blockchain - Service that joins public an private networks using Hyperledger Fabric and Ethereum

