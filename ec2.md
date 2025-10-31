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
    ```
    aws ec2 describe-instances
    ```
### find instances-Id:
    aws ec2 describe-instances --query "Reservations[].Instances[].InstanceId" --output table

### check ec2 state:
    ```
    aws ec2 describe-instances --query "Reservations[].Instances[].{InstanceId:InstanceId, State:State.Name}" --output table
    ```