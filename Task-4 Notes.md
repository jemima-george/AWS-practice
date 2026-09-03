## Task 4: Deployment, Databases, Governance & Security

### Deployment:

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

