# AWS Three Tier Web Architecture Workshop

## Description: 
This workshop is a hands-on walk through of a three-tier web architecture in AWS. We will be manually creating the necessary network, security, app, and database components and configurations in order to run this architecture in an available and scalable manner.

## Architecture Overview
![Architecture Diagram](https://github.com/aws-samples/aws-three-tier-web-architecture-workshop/blob/main/application-code/web-tier/src/assets/3TierArch.png)

In this architecture, a public-facing Application Load Balancer forwards client traffic to our web tier EC2 instances. The web tier is running Nginx webservers that are configured to serve a React.js website and redirects our API calls to the application tier’s internal facing load balancer. The internal facing load balancer then forwards that traffic to the application tier, which is written in Node.js. The application tier manipulates data in an Aurora MySQL multi-AZ database and returns it to our web tier. Load balancing, health checks and autoscaling groups are created at each layer to maintain the availability of this architecture.

## Algorithm
# AWS PROJECT
# CREATING 3 TIER ARCHITECTURE & INTEGRATING OTHER AWS RESOURCES

STEP1: DOWNLOAD CODE FROM GITHUB IN YOUR LOCAL SYSTEM

STEP2: CREATE TWO S3 BUCKETS 
		- CREATE ONE S3 BUCKET FOR STORING WEB-SERVER & APP-SERVER CODE 
		- UPLOAD THE CODE TO YOUR S3 FROM YOUR LOCAL SYSTEM
		- CREATE ANOTHER S3 BUCKET FOR VPC FLOW LOGS

STEP3: CREATE IAM ROLE WITH POLICIES:
        - S3 READ ONLY
        - SSM MANAGED INSTANCE CORE

STEP4: CREATE VPC, SUBNETS, IGW, NAT-GW, RT
		- ENABLE AUTO-ASSIGN PUBLIC IP FOR WEB-TIER PUBLIC SUBNETS
		- CREATE FLOW LOGS FOR VPC & USE THE S3 BUCKET CREATED ABOVE
		
STEP5: CREATE SECURITY GROUPS
        - 1. EXTERNAL-LOAD-BALANCER-SG --> HTTP (80): 0.0.0.0/0
        - 2. WEB-TIER-SG --> HTTP --> EXT-LB-SG
        - 3. INTERNAL-LOAD-BALANCER-SG --> HTTP --> WEB-TIER-SG
        - 4. APP-TIER-SG --> PORT 4000 ---> INTERNAL-LB-SG
        - 5. DB-TIER-SG --> MYSQL (3306) --> APP-TIER-SG

STEP6: CREATE DB SUBNET GROUP & RDS
        - CREATE DB SUBNET GROUP
        - CREATE RDS
          - Multi-AZ 
          - Place them in DB subnet group created above

STEP7: CREATE TEST APP SERVER, INSTALL PACKAGES, TEST CONNECTIONS
		- TEST APP-SERVER COMMANDS LINK: 
			https://github.com/pandacloud1/AWS_Project1/blob/main/app-server-commands
        - CREATE AMI
        - CREATE LAUNCH TEMPLATE USING AMI
        - CREATE TARGET GROUP
        - CREATE INTERNAL LOAD BALANCER
        - CREATE AUTOSCALING GROUP
		- EDIT NGINX.CONF FILE IN LOCAL SYSTEM BY ADDING INTERNAL-LB-DNS & UPLOAD THE FILE IN S3

STEP8: CREATE TEST WEB SERVER, INSTALL PACKAGES (NGINX, NODEJS(REACT), TEST CONNECTIONS
		- TEST WEB-SERVER COMMANDS LINK:
			https://github.com/pandacloud1/AWS_Project1/blob/main/web-server-commands
        - CREATE AMI
        - CREATE LAUNCH TEMPLATE USING AMI
        - CREATE TARGET GROUP
        - CREATE EXTERNAL LOAD BALANCER
        - CREATE AUTOSCALING GROUP

STEP9: ADD EXTERNAL-ALB-DNS RECORD IN ROUTE53

STEP10: CREATE CLOUDWATCH ALARMS ALONG WITH SNS

STEP11: CREATE CLOUDTRAIL

STEP12: DELETING THE ENTIRE INFRASTRUCTURE
        - DELETE CLOUDFRONT
        - DELETE CLOUDWATCH ALARMS
        - DELETE RECORDS FROM ROUTE53
        - DELETE LOAD BALANCERS, TARGET GROUPS, ASG, LAUNCH TEMPLATES
        - DELETE SECURITY GROUP
        - DELETE NAT GATEWAY (IT WILL TAKE 5 MINS)
        - RELEASE ELASTIC IP
        - DELETE VPC
        - DELETE RDS SUBNET GROUP, RDS

## Workshop Instructions:

See [AWS Three Tier Web Architecture](https://catalog.us-east-1.prod.workshops.aws/workshops/85cd2bb2-7f79-4e96-bdee-8078e469752a/en-US)
