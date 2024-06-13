# Create RDS in Private subnet and connect it through EC2 instance in Public Subnet (Jump-Box).
## Set up VPC.
- Create VPC with Minimum 2 public and 2 private subnets make sure both are spread accros minimum 2 different AZ. (It is required as RDS needs minimum 2 AZ)
- Ex.: 1 private subnet in ap-south-1a and 1 private subnet in ap-south-1b.
- 1 public subnet in ap-south-1a or 1b.
## Set-up Subnet Group for the RDS:
- RDS -> Subnet-Groups -> Create new Group -> Select VPC -> Select AZ -> Select Private subnets from each AZ.
## Create RDS Instace:
- Set up As you require.
- Connectivity:
  - Computer Resource: no need
  - Select VPC.
  - Select Subnet Group.
  - Public Accesible: No.
  - Create New Security Group.
  - Create DataBase.
## EC2 Creation:
- Create EC2 just like we create normally. But Few things need to be taken care of.
- EC2 must be created in Our Newly created VPC.
- Subnet should be public subnet. (As it is publicly available.)
- Create New Security Group with desired Configuration.
- Select the SSH key or create new.
## Connect EC2 with RDS:
- Go to the RDS -> Open Security Group of RDS.
- Add Following rule to this security group.
  ```
  Type: MySQL/Aurora
  Source: Select security group of EC2 instance.
  ```
## Now it is connected.
- You can connect to the rds through SSH tunnuling.
  ```
  Over SSH:
  Server: IP
  Port: 22
  User: Ubuntu
  Use SSH Key...

  Host: endpoint of RDS
  Port: Able to find on RDS.
  User: xyz
  PasswordL xyz
  ```
