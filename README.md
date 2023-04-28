## Pre-requisites
- Net new account (In Scope)
- Account ID and its Environmnt mapping details 
- Active login to the account with required access to run the lambdas and create s3 buckets

## Services and resources involved
- AWS Simple Storage Service(S3)
- Cloud Watch Events
- Cloud Watch log Groups
- AWS Lambdas
- CloudShell
- Identity and Access management(IAM)
- CloudTrail

## Installation steps
This can be installed using three ways
- Cloudshell of the account
- AWS Code Pipeline 


Steps

Step 1 - Install Custodian using python
- <https://cloudcustodian.io/docs/quickstart/index.html#install-cc>

step 2 - Install c7n-org

```
pip install c7n-org
```

Step 3 - Create a Lambda service role and have the below Trust relationship updated to the role created

Role Name - custodian-role

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "lambda.amazonaws.com",
                "AWS": "*"
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

Step 4- For custodian to get triggered when there is a new resources , it requires active trails to be created in Cloud trail. Enable the trail with all management events getting captured.

step 5 - Run the command to create lambda 
```
c7n-org run -c accounts.yaml -s output -u test.yaml
```

