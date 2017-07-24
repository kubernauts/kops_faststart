# Configure AWS

---

Creation of the AWS Kops group / user and the state store must be completed before installing the first Kubernetes cluster.

---

## Configure AWS Credentials

Configure the AWS client to use your main AWS credentials.  This is needed so that you are able to create the `kops` group and `kops` user in the next step.

```
$ aws configure
AWS Access Key ID [None]: → provide your access key
AWS Secret Access Key [None]: → provide your secret key
Default region name [None]: eu-central-1 # provide your region
Default output format [None]: → enter
```


## Create the Kops Group and User

Create a `kops` user group, add the required permissions to the group, and then add the `kops` user to the user group.  This will create a new access and secret key.

```
aws iam create-group --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonEC2FullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonRoute53FullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/IAMFullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonVPCFullAccess --group-name kops
aws iam create-user --user-name kops
aws iam add-user-to-group --user-name kops --group-name kops
aws iam create-access-key --user-name kops
```

Verify that the `kops` user is created.

```
$ aws iam list-users | grep kops
            "UserName": "kops",
            "Arn": "arn:aws:iam::111111111111111:user/kops"
```

After running the command `aws iam create-access-key --user-name kops` in the previous steps you will have been shown JSON output similar to the following.

```
{
    "AccessKey": {
        "UserName": "kops",
        "Status": "Active",
        "CreateDate": "2017-07-14T21:54:00.678Z",
        "SecretAccessKey": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
        "AccessKeyId": "XXXXXXXXXXXXXXXXXXXXX"
    }
}
```

Update your AWS client credentials to use the access and secret key values for the `kops` user (as seen in the above JSON output).

```
$ vi .aws/credentials
[default]
aws_access_key_id = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
aws_secret_access_key = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```


## Create the state store

Create an Amazon S3 bucket for your Kubernetes state store. 

**NOTES**<br/>
* There is currently an [issue](https://github.com/aws/aws-sdk-js/issues/475) that requires the state store to be created in `us-east-1`.
* Replace `<kubernauts-io>` with your own domain name.

```
$ aws s3api create-bucket --bucket k8s-<kubernauts-io>-state-store --region us-east-1
```

Add versioning for this bucket to revert or recover a previous version of the cluster:

```
$ aws s3api put-bucket-versioning --bucket k8s-<kubernauts-io>-state-store  --versioning-configuration Status=Enabled
```



We’re using a gossip-based cluster, set these environment variables:

```
$ export KOPS_STATE_STORE=s3://k8s-<kubernauts-io>-state-store
$ export NAME=kubernauts.k8s.local
```

Find the desired availability zones in your region (I’m using `eu-central-1`).

```
$ aws ec2 describe-availability-zones --region eu-central-1
{
    "AvailabilityZones": [
        {
            "State": "available",
            "RegionName": "eu-central-1",
            "Messages": [],
            "ZoneName": "eu-central-1a"
        },
        {
            "State": "available",
            "RegionName": "eu-central-1",
            "Messages": [],
            "ZoneName": "eu-central-1b"
        },
        {
            "State": "available",
            "RegionName": "eu-central-1",
            "Messages": [],
            "ZoneName": "eu-central-1c"
        }
    ]
}
```

These availability zones will be used in later steps.

---

**NEXT**<br/>
[Create First Cluster](lab_4_create_first_cluster.md)<br/><br/>
**PREVIOUS**<br/>
[Install Kubectl](lab_2_install_kubectl.md)