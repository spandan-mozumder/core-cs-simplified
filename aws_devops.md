# ☁️🔧 AWS DevOps — Interview Questions & Answers

> Top AWS DevOps interview questions with answers and examples.
> Source: [Intellipaat — AWS DevOps Interview Questions](https://intellipaat.com/blog/interview-question/aws-devops-interview-questions/)

---

### Q1. What is AWS DevOps?

The integration of **AWS cloud services** with **DevOps practices** (CI/CD, IaC, monitoring, automation) to accelerate software delivery.

---

### Q2. AWS DevOps Tool Suite

| Tool                  | Purpose                                  |
| --------------------- | ---------------------------------------- |
| **CodeCommit**        | Git-based source control (like GitHub)   |
| **CodeBuild**         | Build & test automation                  |
| **CodeDeploy**        | Automated deployment to EC2, Lambda, ECS |
| **CodePipeline**      | CI/CD orchestration                      |
| **CodeStar**          | Unified project dashboard                |
| **CloudFormation**    | Infrastructure as Code                   |
| **Elastic Beanstalk** | PaaS — deploy without managing infra     |

---

### Q3. CodePipeline

```yaml
# buildspec.yml (for CodeBuild)
version: 0.2
phases:
  install:
    runtime-versions:
      nodejs: 18
  pre_build:
    commands:
      - npm install
  build:
    commands:
      - npm run build
      - npm test
  post_build:
    commands:
      - echo "Build completed on $(date)"
artifacts:
  files:
    - "**/*"
  base-directory: "build"
```

---

### Q4. CodeDeploy — Deployment Strategies

| Strategy       | Description                             | Risk   |
| -------------- | --------------------------------------- | ------ |
| **In-place**   | Update existing instances one at a time | Medium |
| **Blue/Green** | Deploy to new instances, switch traffic | Low    |
| **Canary**     | Route small % of traffic to new version | Low    |
| **Rolling**    | Replace instances in batches            | Medium |

```yaml
# appspec.yml (CodeDeploy)
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html
hooks:
  BeforeInstall:
    - location: scripts/install_deps.sh
      timeout: 300
  AfterInstall:
    - location: scripts/start_server.sh
      timeout: 300
  ValidateService:
    - location: scripts/health_check.sh
      timeout: 300
```

---

### Q5. ECS (Elastic Container Service)

```json
{
  "family": "web-app",
  "containerDefinitions": [
    {
      "name": "web",
      "image": "123456789.dkr.ecr.us-east-1.amazonaws.com/myapp:latest",
      "memory": 512,
      "cpu": 256,
      "portMappings": [{ "containerPort": 3000, "hostPort": 80 }],
      "essential": true
    }
  ]
}
```

---

### Q6. Lambda in DevOps

```python
# Automated response to S3 upload
import boto3

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']

    # Process uploaded file
    response = s3.get_object(Bucket=bucket, Key=key)
    content = response['Body'].read().decode('utf-8')

    # Trigger CodePipeline
    cp = boto3.client('codepipeline')
    cp.start_pipeline_execution(name='MyPipeline')

    return {'status': 'Pipeline triggered'}
```

---

### Q7. CloudFormation vs Elastic Beanstalk

| Feature     | CloudFormation        | Elastic Beanstalk     |
| ----------- | --------------------- | --------------------- |
| Level       | IaC (full control)    | PaaS (managed)        |
| Complexity  | You define everything | Auto-configures infra |
| Flexibility | Maximum               | Limited               |
| Use case    | Custom architectures  | Quick deployments     |

---

### Q8. Microservices on AWS

| Component    | AWS Service           |
| ------------ | --------------------- |
| Compute      | ECS, EKS, Lambda      |
| API Gateway  | API Gateway           |
| Service Mesh | App Mesh              |
| Messaging    | SQS, SNS, EventBridge |
| Storage      | S3, DynamoDB, RDS     |
| Monitoring   | CloudWatch, X-Ray     |

---

### Q9. VPC in DevOps Context

- **Public subnet**: Web servers, load balancers
- **Private subnet**: Databases, application servers
- **NAT Gateway**: Private subnet internet access for updates
- **VPC Peering**: Connect VPCs across accounts/regions

---

### Q10. Infrastructure as Code with AWS

```bash
# CloudFormation
aws cloudformation create-stack \
    --stack-name my-stack \
    --template-body file://template.yaml

# CDK (Cloud Development Kit) — IaC in programming languages
cdk init app --language=typescript
cdk synth    # Generate CloudFormation template
cdk deploy   # Deploy stack
```

---

### Q11. Monitoring & Logging in AWS DevOps

| Tool           | Purpose                      |
| -------------- | ---------------------------- |
| **CloudWatch** | Metrics, logs, alarms        |
| **CloudTrail** | API call auditing            |
| **X-Ray**      | Distributed tracing          |
| **Config**     | Resource compliance tracking |
| **GuardDuty**  | Threat detection             |

---

### Q12. Kubernetes on AWS (EKS)

```bash
# Create EKS cluster
eksctl create cluster \
    --name my-cluster \
    --region us-east-1 \
    --nodegroup-name workers \
    --node-type t3.medium \
    --nodes 3

# Deploy application
kubectl apply -f deployment.yaml
kubectl get pods
kubectl get services
```

---
