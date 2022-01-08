CloudFormation template examples
================================

Templates
---------
### Overview
|CFn template|Purpose|
|------------|--------|
|iam.yml|Create IAM policies, groups, roles, users, instance profiles.|
|vpc.yml|Create VPC, IGW, Subnets, Routetables.|
|s3.yml|Create bukets.|
|ec2.yml|Create security groups, EC2 instances.|
|ssm-patchmanager.yml|Create patch baselines, maintainance windows, targets, tasks.|
|guardduty.yml|Enable a detector.|
|ssm-ansible.yml|Apply ansible playbooks with EC2 instances.|

### Deploy templates
```
❯ aws cloudformation deploy --stack-name IAMStack --template-file templates/iam.yml --capabilities CAPABILITY_NAMED_IAM --parameter-overrides file://parameters/iam.json
❯ aws cloudformation deploy --stack-name VPCStack --template-file cfn/templates/vpc.yml
❯ aws cloudformation deploy --stack-name S3Stack --template-file cfn/templates/s3.yml
❯ aws cloudformation deploy --stack-name EC2Stack --template-file cfn/templates/ec2.yml
❯ aws cloudformation deploy --stack-name SSMPatchmanagerStack --template-file cfn/templates/ssm-patchmanager.yml
❯ aws cloudformation deploy --stack-name GuarddutyStack --template-file cfn/templates/guardduty.yml
```

### Apply ansible playbooks
```
❯ zip -r playbooks.zip ansible/playbooks
aws s3 cp playbooks.zip s3://ansible-playbooks-<aws-account-id>/
❯ aws cloudformation deploy --stack-name SSMAnsibleStack --template-file cfn/templates/ssm-ansible.yml
```


DEvelopment
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
❯ cfn-lint templates/iam.yml
```

## Cfn_nag
```
❯ bundle exec cfn_nag templates/iam.yml
```

#
```
❯ aws cloudformation list-stacks | jq -r '.StackSummaries[] | select( .StackStatus != "DELETE_COMPLETE" and .StackName == "VPCStack" )'
{
  "StackId": "arn:aws:cloudformation:ap-northeast-1:000000000000:stack/VPCStack/e95f6440-68f2-11ec-90f2-06de64987995
",
  "StackName": "VPCStack",
  "TemplateDescription": "Create VPC.",
  "CreationTime": "2021-12-29T22:01:44.903000+00:00",
  "LastUpdatedTime": "2021-12-29T22:01:50.276000+00:00",
  "StackStatus": "CREATE_COMPLETE",
  "DriftInformation": {
    "StackDriftStatus": "NOT_CHECKED"
  }
}
```

# Resouces created by templates
## IAM
![IAM](./docs/imgs/graph-iam.jpg?raw=true "IAM")