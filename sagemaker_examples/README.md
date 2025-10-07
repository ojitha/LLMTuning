# SageMaker CloudFormation Templates

This repository contains CloudFormation templates for deploying AWS SageMaker infrastructure with separated network components.

## Templates

- `network-infrastructure.yaml` - Network infrastructure (VPC, subnets, internet gateway)
- `sagemaker_quick_setup.yaml` - SageMaker Studio domain and user profile

## Deployment

Deploy the stacks in order:

### 1. Deploy Network Stack

```bash
aws cloudformation create-stack \
  --stack-name my-network-stack \
  --template-body file://network-infrastructure.yaml
```

### 2. Deploy SageMaker Stack

```bash
aws cloudformation create-stack \
  --stack-name my-sagemaker-stack \
  --template-body file://sagemaker_quick_setup.yaml \
  --parameters ParameterKey=NetworkStackName,ParameterValue=my-network-stack \
  --capabilities CAPABILITY_NAMED_IAM
```

## Cleanup

Delete stacks in reverse order:

```bash
aws cloudformation delete-stack --stack-name my-sagemaker-stack
```


```bash
aws cloudformation delete-stack --stack-name my-network-stack
```