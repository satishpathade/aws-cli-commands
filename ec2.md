# AWS CLI - EC2 Commands

This file contains AWS CLI commands**Amazon EC2 (Elastic Compute Cloud)** instances.  
Amazon EC2 provides scalable computing capacity in the AWS cloud, allowing you to run virtual servers on-demand.

Using AWS CLI, you can manage EC2 instances, security groups, volumes, and networking quickly and efficiently.

---

**Require**
```
    --key component : 
        --image-id → AMI ID to launch instance from.
        --count → Number of instances to launch.
        --instance-type → Instance size.
        --key-name → Key pair for SSH access.
        --security-group-ids → Security group IDs.
        --subnet-id → Subnet ID for networking.  
```

**EC2 low level command | Common EC2 Operations**

#### list all ec2 instances:
    aws ec2 describe-instances

#### find instances-Id
    aws ec2 describe-instances --query "Reservations[].Instances[].InstanceId" --output table

#### check ec2 state
    aws ec2 describe-instances --query "Reservations[].Instances[].{InstanceId:InstanceId, State:State.Name}" --output table

#### start ec2
    aws ec2 start-instances --instance-ids 'your-instanceID'                (id-single ec2 | ids-multiple ec2)

**launch EC2: Default VPC**
**Require**
```
    --key component
        --image-id → AMI ID to launch instance from.
        --count → Number of instances to launch.
        --instance-type → Instance size.
        --key-name → Key pair for SSH access.
        --security-group-ids → Security group IDs.
```

#### create key pair
    aws ec2 create-key-pair --key-name newkeypair --query "KeyMaterial" --output text > newkeypair.pem

#### Get key pair
    aws ec2 describe-key-pairs --key-names newkeypair --query "KeyPairs[*].[KeyName,KeyPairId]" --output table

#### AMI ID
    aws ec2 describe-images --owners amazon --filters "Name=name,Values=amzn2-ami-hvm-*-x86_64-gp2" --query "Images[*].[ImageId,Name]" --output table

#### Get VPC Id
    aws ec2 describe-vpcs --filters "Name=isDefault,Values=true" --query "Vpcs[*].VpcId" --output text

#### create security group
    aws ec2 create-security-group --group-name MySecurityGroup --description "Security group for EC2 instance" --vpc-id <vpc-id>

#### Get security groutId
    aws ec2 describe-security-groups --group-names MySecurityGroup --query "SecurityGroups[0].GroupId" --output text

#### Allow port- SSH 22, HTTP 80
    aws ec2 authorize-security-group-ingress --group-id <sg-id> --protocol tcp --port 22 --cidr 0.0.0.0/0
    aws ec2 authorize-security-group-ingress --group-id <sg-id> --protocol tcp --port 80 --cidr 0.0.0.0/0

#### lounch ec2
    aws ec2 run-instances --image-id <ami-id> --count 1 --instance-type t2.micro --key-name MyKeyPair --security-group-ids <sg-id>