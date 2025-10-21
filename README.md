## **Using AWS Systems Manager**

## **Overview**

This lab demonstrates how to use AWS Systems Manager (SSM) to centralize operational management and automate tasks across AWS resources.
You worked with multiple Systems Manager capabilities — Fleet Manager, Run Command, Parameter Store, and Session Manager — to securely manage EC2 instances, install applications, update configurations, and access instances without SSH.

## **Objectives & Learning Outcomes**

After completing this lab, I will be able to:

Generate inventory lists for managed instances using Fleet Manager

Install applications remotely using Run Command

Manage configurations and secrets with Parameter Store

Access EC2 instances securely using Session Manager

Perform operational tasks without opening inbound ports or using SSH keys



## **Architecture**

<img width="600" height="400" alt="58a8131c-72c6-4fc8-a328-9bd041fcd462" src="https://github.com/user-attachments/assets/c69c8bb0-a473-4ab2-a30e-ac0736a2c2a2" />

Architecture Description:

The User connects to the AWS Console to interact with Systems Manager.

Fleet Manager inventories and monitors managed EC2 instances.

Run Command installs the Widget Manufacturing Dashboard on an EC2 instance.

Parameter Store manages app configuration flags (e.g., /dashboard/show-beta-features).

Session Manager provides secure, SSH-free access to the EC2 instance’s command line.


## **Commands and Steps**

```bash
# Step 1: Generate inventory list using Fleet Manager
# Systems Manager Console → Fleet Manager → Set up inventory
# Name: Inventory-Association
# Target: Managed Instance
# Confirm success banner: "Setup inventory request succeeded"

# Step 2: Install a custom web application via Run Command
# Systems Manager Console → Run Command → Choose document (Install Dashboard App)
# Select Managed Instance → Choose Run
# Wait for "Success" status
# Validate installation using the public IP from the lab details
# Browser output: Widget Manufacturing Dashboard displayed

# Step 3: Manage app settings via Parameter Store
# Systems Manager → Parameter Store → Create parameter
# Name: /dashboard/show-beta-features
# Value: True
# Refresh web app to reveal new chart feature
# Delete parameter to hide the beta chart

# Step 4: Access instance using Session Manager
# Systems Manager → Session Manager → Start session → Managed Instance
ls /var/www/html
# Confirm application files installed

# Get AWS Region dynamically and describe EC2 instances
AZ=`curl -s http://.........../latest/meta-data/placement/availability-zone`
export AWS_DEFAULT_REGION=${AZ::-1}
aws ec2 describe-instances
```

## **Screenshots**

Fleet Manager Inventory Tab – showing applications and configurations collected.
<img width="1737" height="542" alt="1" src="https://github.com/user-attachments/assets/ef50f057-4e8f-4425-bc2c-50ace1f90c87" />

Run Command Success Page – with Command ID and overall status = Success.
<img width="1608" height="531" alt="2" src="https://github.com/user-attachments/assets/e03db4bb-647d-414d-859d-94727e4de534" />

Widget Manufacturing Dashboard – displayed in browser.
<img width="1532" height="417" alt="3" src="https://github.com/user-attachments/assets/96212659-ed98-4ff2-a06e-0e68ea7cce6f" />

Parameter Store Entry – showing /dashboard/show-beta-features=True.
<img width="1514" height="439" alt="5" src="https://github.com/user-attachments/assets/42e3f53c-fb34-44e5-89a1-d6b08257aeff" />

Session Manager Console – showing active shell session and output of ls /var/www/html.
<img width="900" height="300" alt="6" src="https://github.com/user-attachments/assets/356a8dfc-a1be-4231-a0db-487ad1c85b45" />

## **Tools Used**

AWS Systems Manager (Fleet Manager, Run Command, Parameter Store, Session Manager)

Amazon EC2

AWS Identity and Access Management (IAM)

AWS Management Console


## **What Actually Happened**

Generated inventory data from a managed EC2 instance using Fleet Manager.

Used Run Command to install a custom dashboard app remotely — without SSH.

Created a Parameter Store variable that toggled hidden (“beta”) features in the web app.

Accessed the EC2 instance securely via Session Manager, listing and validating files.

Verified that no inbound ports or SSH keys were needed for instance access.


## **Key Takeaways**

Systems Manager allows unified visibility and automation for EC2 and hybrid environments.

Run Command automates bulk software deployment across instances.

Parameter Store securely manages dynamic configuration data.

Session Manager replaces SSH with secure, auditable web-based access.


## **Author**

Amarachi Emeziem

Cloud Security Engineer | AWS & Azure Certified |Per-Schola Fellow
