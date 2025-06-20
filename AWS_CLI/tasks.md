#in AWS we use vpc, in Azure we use vnet for creating the public or private network
step 1: for VPC:
> aws ec2 create-vpc --cidr-block 10.0.0.0/16

step 2: for subnet:  
> aws ec2 create-subnet \
  --vpc-id vpc-xxxxxxxx \
  --cidr-block 10.0.1.0/24

step 3: Gateway:
> aws ec2 create-internet-gateway

> aws ec2 attach-internet-gateway \
  --vpc-id vpc-xxxxxxxx \
  --internet-gateway-id igw-xxxxxxxx

step 4: Route Table and its association
> aws ec2 create-route-table --vpc-id vpc-xxxxxxxx

aws ec2 create-route \
  --route-table-id rtb-xxxxxxxx \
  --destination-cidr-block 0.0.0.0/0 \
  --gateway-id igw-xxxxxxxx


>  aws ec2 associate-route-table \
  --subnet-id subnet-xxxxxxxx \
  --route-table-id rtb-xxxxxxxx

step 5: Now Launch an EC2 instance
> aws ec2 run-instances \
  --image-id ami-0c02fb55956c7d316 \  # Example Ubuntu AMI in us-east-1
  --count 1 \
  --instance-type t2.micro \
  --key-name myKeyPair \
  --subnet-id subnet-xxxxxxxx \
  --associate-public-ip-address \
  --security-group-ids sg-xxxxxxxx


