 # SETTING UP A SCALABLE FILE STORAGE SYSTEM USING AMAZON ELASTIC FILE SYSTEM
  ## AIM
  To set up a scalable file storage system using Amazon Elastic File System (EFS) for two EC2 instances in different availability zones, enabling shared access to data.
## PROBLEM STATEMENT

   This experiment demonstrates how to configure Amazon EFS to provide a shared storage solution for two Linux EC2 instances across different availability zones, enabling easy data sharing. The aim is to ensure both instances can mount and access the EFS file system and validate data consistency across instances.

## ALGORITHM

## Step 1:Launch Two EC2 Instances in Different Availability Zones

Go to the EC2 service in the AWS Management Console.
Launch two Linux-based EC2 instances (e.g., Amazon Linux 2) and place them in different availability zones within the same VPC.
Assign each instance a security group that allows NFS access on port 2049.

## Step 2:Set Up Security Group for EFS

Create or configure a security group that allows inbound NFS traffic on port 2049 from the security group of both EC2 instances.
Attach this security group to the EFS file system to permit access from both instances.

## Step 3: Create an EFS File System

In the AWS Console, navigate to the EFS service and select Create file system.
Select the same VPC as your EC2 instances and configure mount targets in the availability zones where your instances are located.
Complete the setup and take note of the file system ID (e.g., fs-064645ac116a12816).

## Step 4: Configure EC2 Instances to Access EFS

## Instance 1
SSH into the first EC2 instance.
Switch to superuser
Install the HTTP server and EFS utilities
Mount the EFS file system to the web server's root directory
Navigate to the mounted directory and create a sample file:

## Instance 2
SSH into the second EC2 instance.
Switch to superuser
Install the HTTP server and EFS utilities
Mount the EFS file system to the web server's root directory
Navigate to the mounted directory, list files, and view the content of the file created on Instance 1

## COMMANDS
## EC2 Instance 1
sudo su
yum install httpd -y
yum install -y amazon-efs-utils
mount -t efs -o tls fs-064645ac116a12816:/ /var/www/html
cd /var/www/html
vi file  # Create a file and add some text
## EC2 Instance 2
sudo su
yum install httpd -y
yum install -y amazon-efs-utils
mount -t efs -o tls fs-064645ac116a12816:/ /var/www/html
cd /var/www/html
ls
cat file  # Verify shared access by reading content created in Instance 1

## OUTPUT
Both EC2 instances showing EFS mounting.
![image](https://github.com/user-attachments/assets/60706b8d-06c8-4774-9fa2-973d73588ed3)

![image](https://github.com/user-attachments/assets/918e77c3-8370-4825-b6fd-979b8f59964f)

The creation of a file on Instance 1.

![image](https://github.com/user-attachments/assets/b14b53bd-cc29-4801-89b1-3b612fba77a3)
The display of that file’s contents on Instance 2 to verify shared access

![image](https://github.com/user-attachments/assets/8c03d586-81b8-4506-a38c-0a65f1cb3324)

### REG NUMBER:212223040059
### NAME:Hariprasath R
 
## RESULT
 Successfully set up a scalable file storage system using Amazon EFS shared between two Linux EC2 instances in different availability zones, enabling consistent data sharing.

  


