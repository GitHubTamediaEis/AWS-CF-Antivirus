# AWS-CF-AntivirusDeployment

Used to deploy the Antivirus on Amazon EC2 instances based on tag.

# AntivirusDeployment.yaml

This file is a CloudFormation template that deploys the Antivirus.

# Instructions

The Antivirus Deployment is available in the [Service Catalog](https://docs.aws.amazon.com/servicecatalog/latest/userguide/end-user-console.html) of your account and can easily be deployed from there.

**Make sure your instances meet the Prerequisites, see section [Instance considerations](#instance-considerations)**

Upon deployment you have to specify custom parameters which are explained hereafter.

# Custom parameters

| Parameter | Default | Possible values | Notes |
| ------ | ------ | ------ | ------ |
|AVTagName | Antivirus | string | Tag name (key) for instances to include as targets for installing the Antivirus |
|AVTagValue | yes | string | Tag value for instances to include as targets for installing the Antivirus |

# Instance considerations

:heavy_exclamation_mark: **The instance will be restarted to uninstall Windows Defender** :heavy_exclamation_mark:

Prerequisites to be able to deploy the Antivirus:
- Python 2.7+ or 3.0+ installed
- SSM agent installed
- AWS CLI installed

Instances must be listed in the [Managed Instances](https://console.aws.amazon.com/systems-manager/managed-instances) list of AWS Systems Manager. To show up in this list, the instances must meet the [Systems Manager Prerequisites](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html).

You also need to add access to the s3 bucket containing Cybereason sensor to the IAM role assigned to the EC2 instance.
Here is the content to add:
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::cybereasonsensor/*",
                "arn:aws:s3:::cybereasonsensor"
            ]
	]
}
