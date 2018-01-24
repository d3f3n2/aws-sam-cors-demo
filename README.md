# AWS SAM CORS Demo

## Getting Started

Development and deployment of the framework will require the following:

### System Deployment Prerequisites

* [Python](https://www.python.org/download/releases/2.7/):  AWS Lambda supported Python language runtime 2.7.
* [PIP](https://pip.pypa.io/en/stable/) : Install and manage Python Modules
* [AWS Command Line Interface](https://aws.amazon.com/cli/): Unified tool to manage your AWS services.
* [Boto3](https://boto3.readthedocs.io/en/latest/) : Amazon Web Services SDK for Python.

### Installing System Deployment Prerequisites

```bash
# Install PIP
python get-pip.py

# Install AWS CLI
pip install awscli

# Configure AWS CLI
aws configure
AWS Access Key ID [None]: <Access Key>
AWS Secret Access Key [None]: <Secret>
Default region name [None]: <Region>
Default output format [None]: ENTER

# Install Boto3
pip install boto3==1.4.4
```

## Deployment

### SAM
```bash

# Install packages listed in requirements to a directory for package deployment

mkdir ./build
cp -p -r ./movies ./build/movies
pip install -r requirements.txt -t ./build

# Replace Swagger AWS account id and region placeholders with your own

sed -i "s/account_placeholder/AWS_ACCOUNT_ID/g" 'swagger.yaml'
sed -i "s/region_placeholder/AWS_REGION/g" 'swagger.yaml'

# Package SAM code and replace MY_S3_Bucket with your own

aws cloudformation package --template-file template.yaml --output-template-file template-out.yaml --s3-bucket MY_S3_Bucket

# Deploy SAM as an S3 CloudFormation Stack
## Replacing YOUR_SECRET ANDS_APP_ID SUBNET_ID SECURITY_GROUP ES_URL
aws cloudformation deploy --template-file template-out.yaml --stack-name MoviesAPI --capabilities CAPABILITY_IAM

```
