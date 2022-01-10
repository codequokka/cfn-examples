CloudFormation template examples
================================

Templates
---------
### Overview
|CFn template|Purpose|
|------------|--------|
|iam.yml|Create policies, groups, roles, users.|
|vpc.yml|Create VPC, IGW, Subnets, Routetables, EIP, NATGW.|
|s3.yml|Create buckets.|
|ec2.yml|Create role, instance profiles, security groups, instances.|
|ssm-patchmanager.yml|Create patch baselines, maintainance windows, targets, tasks.|
|guardduty.yml|Enable a detector.|
|ssm-ansible.yml|Apply ansible playbooks with EC2 instances.|

### Deploy templates
```
# With aws cloudformatin
❯ aws cloudformation deploy --stack-name IAMStack --template-file templates/iam.yml --capabilities CAPABILITY_NAMED_IAM --parameter-overrides file://parameters/iam.json
❯ aws cloudformation deploy --stack-name VPCStack --template-file cfn/templates/vpc.yml
❯ aws cloudformation deploy --stack-name S3Stack --template-file cfn/templates/s3.yml
❯ aws cloudformation deploy --stack-name EC2Stack --template-file cfn/templates/ec2.yml
❯ aws cloudformation deploy --stack-name SSMPatchmanagerStack --template-file cfn/templates/ssm-patchmanager.yml
❯ aws cloudformation deploy --stack-name GuarddutyStack --template-file cfn/templates/guardduty.yml

# With rain
❯ rain deploy cfn/templates/iam.yml IAMStack
❯ rain deploy cfn/templates/vpc.yml VPCStack
❯ rain deploy cfn/templates/s3.yml S3Stack
❯ rain deploy cfn/templates/ec2.yml EC2Stack
❯ rain deploy cfn/templates/ssm-patchmanager.yml SSMPatchmanagerStack
❯ rain deploy cfn/templates/guardduty.yml GuarddutyStack
```

### Apply ansible playbooks
```
# Upload playbook to S3 bucket
❯ zip -r playbooks.zip ansible/playbooks
❯ aws s3 cp playbooks.zip s3://ansible-playbooks-<aws-account-id>/

# With aws cloudformatin
❯ aws cloudformation deploy --stack-name SSMAnsibleStack --template-file cfn/templates/ssm-ansible.yml

# With rain
❯ rain deploy cfn/templates/guardduty.yml GuarddutyStack
```

Development
-----------
##Check templates

###  Requirements
```
❯ cfn-lint -v
cfn-lint 0.56.3

❯ bundle exec cfn_nag -v
0.8.8
```

### Validation
```
❯ aws cloudformation validate-template --template-body file://cfn/templates/iam.yml
❯ aws cloudformation validate-template --template-body file://cfn/templates/vpc.yml
❯ aws cloudformation validate-template --template-body file://cfn/templates/s3.yml
❯ aws cloudformation validate-template --template-body file://cfn/templates/ec2.yml
❯ aws cloudformation validate-template --template-body file://cfn/templates/ssm-patchmanager.yml
❯ aws cloudformation validate-template --template-body file://cfn/templates/guardduty.yml
❯ aws cloudformation validate-template --template-body file://cfn/templates/ssm-ansible.yml
```

## Cfn-lint
```
❯ cfn-lint cfn/templates/*.yml
```

## Cfn_nag
```
❯ bundle exec cfn_nag cfn/templates/*.yml
```
# Resouces created by templates
## IAM
![](./docs/imgs/iam.jpg?raw=true "IAM")

## VPC
![](./docs/imgs/vpc.jpg?raw=true "VPC")

## S3
![](./docs/imgs/s3.jpg?raw=true "S3")

## EC2
![](./docs/imgs/ec2.jpg?raw=true "S3")

## SSM Patch manager
![](./docs/imgs/ssm-patchmanager.jpg?raw=true "S3")

## Guardduty
![](./docs/imgs/guardduty.jpg?raw=true "S3")

## SSM Ansible
![](./docs/imgs/ssm-ansible.jpg?raw=true "S3")