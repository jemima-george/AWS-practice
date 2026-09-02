## Task 3: Networking, Scaling & Application Services

### Domain Name System (DNS):
- Used to direct traffic to resources
- When searching for a domain (eg:amazon.com), DNS finds the IP address of the domain to connect to the domain's web server. 
- Amazon Route 53 is a DNS Service 
- Amazon Route 53 also provides health checks for EC2 instances, load balances etc.
- Can register a domain using Route 53 -
    1. Search for Route 53 on Console, Go to domain registration
    2. Register domain with a name (eg: training.link - .link is the cheapest option) -> Select -> Proceed to checkout -> can turn off auto-renew
    3. Fill out contanct info
    4. If request fails, follow link in message for support
    5. After, go to hosted zones to find your registered domain.  

### Scaling Up Vs Scaling Out:
Scaling Up -
- Add more hardware resources to a virtual machine or instance 
- Eg: Can change instance size from t2.micro to c5.large for more memory and cpu
- When storing states about the user like in a dynamic website, scaling up is better

Scaling Out -
- Add more instances (resources + operating system + web service) for the application
- load balance between them
- static website - easier to scale out
- Will not lose data or server because of multiple instances 

### Amazon E2 Auto Scaling:
- Can automatically launch and terminate EC2 instances based on demand
- Maintain availability if instance fails
- Works with - 
    - CloudWatch service to monitor whether application needs scaling up or scaling out
    - Elastic load balancing to distribute connections
    - E2 spot instances for cost 
    - VPC to deploy instances accross different avalability zones
- Cloud watch checks metrics and can launch new instances if uses more than 80% cpu
- Terminate instance when we don't need it
- Types are manual, dynamic, schedule
- Can adjust scaling policies based on preferences such as changing target metrics, scaling adjustments or schedule scaling for high demand times
- Launch templates definies what runs when auto scaling group scales.
- How to create Auto scaling group for EC2 instances:
    1. Use user data web server as launch template so pages will be different for different availability zones. 
    2. Launch templates in EC2 Console
    3. Create Launch templates for auto scaling with name, AMI, instance type, existing security group as WebAccess, add user data in advanced details -> Launch template
    4. Go to Auto scaling groups -> Create group with name and select launch template -> Choose availability zones -> Choose scaling options (min, max)

### Load Balancer:
- Used to distribute connections to the instances/other targets
- If an instance fails, load balancer will direct user connection to another working instance
- Manages network traffic by connecting user to available instance or web server
- Does Health checks to ensure instances are running properly 

![alt text](network-load-balancer.png)

Types of load balances: 
- Application Load Balancer - 
    - Operates at request level
    - Rotuing based on path url
    - Has http or https listeners
    - USE CASES: Web application, docker contianers, lambda targets
- Network Load Balancer - 
    - Operates at connection level
    - Routing based on IP protocols. Eg: TCP,TLS,UDP
    - Offers high performance, low latency
    - USE CASES: TCP and UDP based applications, very low latency, static IP addresses
- Gateway Load Balancer - 
    - Used infront of virtual appliances such as firewalls, intrusion dectection systems
    - Uses Geneve protocol
    - USE CASES: Deploy and manage 3rd party virtual appliances, centralised inspection, firewalls, cybersecurity

How to create Application Load balancer:
1. Go to EC2 Console and create Auto scaling group for 2 EC2 instances in 2 availabily zones (AZ)
2. Go to Load balancing -> Create Target groups -> Select target type as instances and add a name -> Choose HTTP as protocol -> Create target group
3. Go to Load balancers -> Create Load balancer for Application Load balancer with a name -> Choose the 2 AZ for mapping -> Select webaccess as security groups -> Select target group created under listeners and routing -> Create load balancer
4. Go to the Auto scaling group, edit load balancing -> select application, network, gateway target groups and select the target group -> update
5. Copy DNS name in load balancer and paste in browser to test

### Application Services:
Serverless services -
- No need to manage instances, provide hardware or manage OS
- Automatically manages capacity provisioning and patching
- Automatic scaling and cheaper
- Use with event driven architecture which is a pattern where an event would trigger an action in another service 
- Can build static website without server
- Eg: AWS Lambda Service

AWS Lambda -
- Run some code when triggered by an event
- Cost is based on memory assigned and the duration of func execution
- IAM role grants func permission to access other AWS services
- CloudWatch handles monitoring and logging
- Must add permissions to AWS Lambda if you want func code to connect to other AWS services

### Create/test a basic Lambda function:
Create a basic Lambda function that logs a message to Amazon CloudWatch logs -
1. Open working-with-lambda.md file and Copy the python code to run when event is triggered (import logging....) 
2. Search for Lambda in the Console -> Create a function -> Author from scratch -> Add function name -> Choose runtime as python -> Create function
3. Scroll down to Code source, Paste python code copied to log message into CloudWatch -> Click Deploy
4. Change tab from code source to configuration with default config for time and memory -> Click permission tab which has CloudWatch logs by default. Can edit execution role to add permissions to other AWS services.
5. Change to Test tab -> Copy first test event in working-with-lambda.md file -> Go back to test tab and add an event name -> Paste test event into event JSON -> Click save -> Click Test to Run
6. Change to Monitor tab -> Click view CloudWatch logs -> Select log stream
7. To Test event using the CLI, Go to CloudShell in Console -> Create a file in CloudShell named "payload.json" by running: nano payload.json -> Copy json test code from working-with-lambda.md file and paste in CloudShell -> save file -> Run Point 5 command from working-with-lambda.md file  in CloudShell but update <function-name> part with the lambda function name -> Can view test in CloudWatch logs 

How to create an event notification for S3 uploads:
1. Copy python code (line 54 to line 78) from working-with-lambda.md file 
2. Go back to the Lambda function's Code source tab and paste new code to log new objects uploaded into s3 bucket -> Deploy 
3. Go to Configuration tab -> Permissions -> Click Role name -> Add permissions under permisssions policies -> Search for S3 and select S3ReadOnlyAccess -> Add permission
4. Go back to lambda func -> Add trigger -> Chose S3 as source -> Choose a bucket/ create new bucket 
5. View S3 uploads in CloudWatch logs

### Lambda practice evidence:
Labdma Function Code Source:

![alt text](lambda-code.png)

Test event to log message into CloudWatch logs:

![alt text](lambda-test.png)

Message logged in CloudWatch logs:

![alt text](lambda-logs.png)

### Application Integration Services:
- Simple Queue Service (SQS) - puts messages/orders into a queue, useful during high demand times 
- Simple Notification Service (SQS) - information sent to users when a new message is added into the topic queue, supports notifications to web application, email, sms
- Step Functions - useful for coordinating aws services with workflows
- Amazon MQ - similar to sqs, messages support apache, active mq, rabbitmq
- Event bridge - serverless event bus to connect application and aws services, event source changes and notifies event bus which has a rule to do or send a message to a target

### Understand API Gateway:
- Useful service to connect an application to different microservices
- Takes requests from application through rest api oven https
- Focuses on http methods to direct to different microservices 

### Amazon VPC, Networking, and Hybrid:
Amazon Virtual Private Cloud (VPC) -
- VPC is an isolated portion of the AWS cloud within a region
- Things created within vpc can only be visible inside your account unless launch publicly
- Within VPC, we can create subnets which are mapped to AZ
- Can launch instances in subnets and use internet gateway to connect to internet
- Has a router to define the routes and how to route traffic
- Can create multiple VPC within each region
- AWS services that sit outside the vpc are called public services. Eg: DynamoDB, S3
- AWS services that sit inside the vpc are called private services. Eg: RDS, Elastic file system
- No Cost for VPC

### Explore VPC:
Create practice custom VPC -
1. Search for VPC Console
2. Create own VPC:
    - select vpc and more
    - can change name
    - select no. of AZ
    - Can choose no.of public or private subnets
    - Choose VPC endpoints as none 
3. Go to subnets -> select public subnets -> edit subnet settings -> check enable auto-assign public IPv4 address
4. Can also manually create a custom VPC with custom subnets and manually change route table with subnet associations, Can create internet gateway and attach to the vpc, edit routes in both public and private route tables and add route as any ip address that targets the internet gateway
5. Launch instance into subnet by editing network settings and change vpc and choose a subnet 

### Security Groups and Network ACLs:
- Security Groups and Network ACLs are 2 types of firewalls in a VPC to protect our AWS services 
- Stateful firewall allows the return of traffic from web server to client automatically 
- Stateless firewall checks for an allow rule for the traffic to pass

Network access control list (ACL) -
- Applied at subnet level
- Only Screens traffic that comes in and leaves the subnet
- Stateless firewall that has to apply the rules to inbound and outbound traffic
- Both allow and deny rules

Security Groups -
- Assigned at instance level
- Can be applied to instances in any subnet
- It is a Stateful firewall which will allow return taffic if inbound traffic is allowed
- Only allow rules

### Explore Security Groups and NACL:
Practice using Security Groups -
1. Search for EC2 Console -> Go to security groups
2. Create a security group with name and add an inbound rule for SSH type and change source to anywhere - ipv4
3. Delete previous outbound rule and add a new rule with Custom ICMP-IPv4 type and change destination to anywhere-ipv4
4. To allow curl access to http site, Add another outbound rule with HTTP type and change destination to anywhere-ipv4

Practice using NACLS -
1. Search for VPC Console -> Go to Network ACL
2. Select NACL in default vpc -> Go to inbound rules -> Edit and add rule which will be processed in order 
3. Add rule with 101 as rule number, all traffic as type, any source as source and deny
4. Match happens earlier so traffic passed but if rule number is changed to 99, access is denied

### Types of IP Address:
Public IP address -
- Realeased when instance stopped
- used in public subnets
- cannot be moved between instances
- associated with private ip address on instance
- charged

Private IP address -
- Reatined when instance is stopped
- Used in public and private subnets

Elastic IP address -
- Static public ip address
- charged
- associated with private ip address on instance
- can be moved between instances
- can keep public ip address same even if instance is stopped by associating it with an instance and map it to the private ip address
- have to delete/ release ip address when not in use or else will be charged

### NAT Gateways:
- Managed by AWS 
- Charged
- Must be Deployed in public subnets if you want to connect to the internet
- Needs an elastic IP address
- Nat instance is managed by you - manual scaling, assign security groups, can use elastic ip address or public ip address
- Public NAT Gateway Connectivity is where instances in private subnets can connect to the internet using a NAT gateway
- Private NAT Gateway Connectivity is where instances in private subnets can connect to other vpcs or on-premise networks through a NAT gateway

### VPC Peering:
- Private connection between 2 amazon VPCs
- Allows VPCs to communicate
- Does not depend on central gateway
- supports same account or cross account peering 
- full IP address control
- supports all AWS services
- no transitivive routing
- route table should be updated manually

### Amazon VPN and AWS Direct Connect:
VPN -
- AKA site-to-site VPN since it connects company site to public cloud site
- VPC has a virtual private gateway and company site/data center has a customer gateway.
- Can connect the 2 gateways using VPN which is an encrypted connection going over the internet
- Can face bandwidth issues, low latency or delay because it goes over the internet

AWS Direct Connect -
- Private connection between AWS and comany site/data center
- Connect using a direct connect location 
- Establish connection between then
- Increased speed, consistency, high latency and good performance
- Expenensive

### AWS Transit Gateway:
- Enables simple connectivity by simplifying network management that connect VPCs and on-premise networks
- More scalable than VPC peering
- Allows transitive pairing to enable VPCs to connect with each other
- Can be used for both VPN and direct connect
- Can access cross-accounts
- transit gateways connects all VPC
- Can connect to VPNs, direct connect, TGWs in other regions

### AWS Outposts
- Service to extend some functions of AWS into a company's own premise data center
- Private hybrid cloud in your own premise data center
- Public cloud in AWS
- deploy a VPC and extends subnets within coporate data center and AWS cloud
- Launch instances in the subnets and allow communcation using private IP addresses
- Services include - EC2, EBS, S3, VPC, ECS, RDS, EMR

### Basic AWS network diagram:
![alt text](vpn-connection.png)



