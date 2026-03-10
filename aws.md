# ☁️ AWS — Interview Questions & Answers

> Top AWS interview questions with answers and practical examples.
> Source: [Intellipaat — AWS Interview Questions](https://intellipaat.com/blog/interview-question/amazon-aws-interview-questions/)

---

### Q1. What is AWS?

**Amazon Web Services (AWS)** is a cloud computing platform offering 200+ services including compute, storage, databases, networking, AI/ML, and DevOps tools. It operates on a **pay-as-you-go** model.

---

### Q2. AWS Shared Responsibility Model

| AWS Responsibility       | Customer Responsibility       |
| ------------------------ | ----------------------------- |
| Physical infrastructure  | Data & encryption             |
| Network/hypervisor       | IAM & access control          |
| Managed service patching | OS & application patching     |
| DDoS protection          | Firewall/security group rules |

---

### Q3. Regions and Availability Zones

- **Region**: Geographic area (e.g., us-east-1)
- **Availability Zone (AZ)**: Isolated data center(s) within a region (e.g., us-east-1a)
- Each region has 2-6 AZs for high availability

---

### Q4. EC2 (Elastic Compute Cloud)

Virtual servers in the cloud.

**Instance Types:**

| Type       | Use Case                   |
| ---------- | -------------------------- |
| **t3/t4g** | General purpose, burstable |
| **m5/m6g** | General purpose, balanced  |
| **c5/c6g** | Compute-optimized          |
| **r5/r6g** | Memory-optimized           |
| **p3/g4**  | GPU instances (ML, gaming) |

**Pricing:**

| Model         | Best For                                          |
| ------------- | ------------------------------------------------- |
| On-Demand     | Short-term, unpredictable workloads               |
| Reserved      | Steady-state, 1-3 year commitment (up to 72% off) |
| Spot          | Fault-tolerant workloads (up to 90% off)          |
| Savings Plans | Flexible commitment with savings                  |

---

### Q5. S3 (Simple Storage Service)

**Storage Classes:**

| Class                       | Use Case                          | Cost     |
| --------------------------- | --------------------------------- | -------- |
| **S3 Standard**             | Frequently accessed               | Highest  |
| **S3 IA**                   | Infrequent access                 | Lower    |
| **S3 One Zone-IA**          | Infrequent, non-critical          | Lower    |
| **S3 Glacier**              | Archive (minutes-hours retrieval) | Very low |
| **S3 Glacier Deep Archive** | Long-term archive (12h retrieval) | Lowest   |

```bash
# AWS CLI commands
aws s3 mb s3://my-bucket                        # Create bucket
aws s3 cp file.txt s3://my-bucket/              # Upload
aws s3 sync ./folder s3://my-bucket/folder      # Sync directory
aws s3 ls s3://my-bucket                         # List objects
```

---

### Q6. VPC (Virtual Private Cloud)

**Components:**

- **Subnets**: Public (internet-facing) and Private (internal)
- **Internet Gateway**: Connects VPC to the internet
- **NAT Gateway**: Allows private subnets to access internet
- **Route Tables**: Define traffic routing rules
- **Security Groups**: Stateful firewall (instance-level)
- **NACLs**: Stateless firewall (subnet-level)

---

### Q7. IAM (Identity and Access Management)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    },
    {
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

**Best practices:** MFA, least privilege, use roles over access keys, rotate credentials.

---

### Q8. Load Balancers

| Type                  | Layer             | Use Case                                |
| --------------------- | ----------------- | --------------------------------------- |
| **ALB** (Application) | Layer 7 (HTTP)    | Path/host-based routing, microservices  |
| **NLB** (Network)     | Layer 4 (TCP/UDP) | Ultra-low latency, millions of requests |
| **CLB** (Classic)     | Layer 4 & 7       | Legacy                                  |

---

### Q9. Lambda (Serverless)

- Run code without managing servers
- Pay only for compute time (per 1ms)
- Auto-scales to handle any load
- Max execution: 15 minutes

```python
# lambda_function.py
import json

def lambda_handler(event, context):
    name = event.get('name', 'World')
    return {
        'statusCode': 200,
        'body': json.dumps(f'Hello, {name}!')
    }
```

---

### Q10. RDS (Relational Database Service)

Managed database service supporting MySQL, PostgreSQL, Oracle, SQL Server, MariaDB, Aurora.

**Features:** Automated backups, Multi-AZ deployment (high availability), Read replicas (performance), encryption at rest & in transit.

---

### Q11. CloudFormation

IaC for AWS — define infrastructure in YAML/JSON templates.

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t3.micro
      ImageId: ami-0c55b159cbfafe1f0
      SecurityGroupIds:
        - !Ref MySecurityGroup
  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow HTTP
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
```

---

### Q12. CloudWatch

Monitoring & observability service.

```bash
# Create alarm for high CPU
aws cloudwatch put-metric-alarm \
    --alarm-name "HighCPU" \
    --metric-name CPUUtilization \
    --namespace AWS/EC2 \
    --statistic Average \
    --period 300 \
    --threshold 80 \
    --comparison-operator GreaterThanThreshold \
    --evaluation-periods 2
```

---

### Q13. Auto Scaling

Automatically adjusts EC2 instances based on demand.

**Scaling Policies:**

- **Target Tracking:** Maintain CPU at 60%
- **Step Scaling:** Scale based on CloudWatch alarm thresholds
- **Scheduled:** Scale at specific times

---

### Q14. Route 53 (DNS)

- Domain registration, DNS routing, health checking
- **Routing policies:** Simple, Weighted, Latency-based, Failover, Geolocation

---

### Q15. SNS, SQS, and EventBridge

| Service         | Type          | Use Case                  |
| --------------- | ------------- | ------------------------- |
| **SNS**         | Pub/Sub       | Notifications, fan-out    |
| **SQS**         | Message Queue | Decoupling services       |
| **EventBridge** | Event Bus     | Event-driven architecture |

---
