# IAM Overview
 
```ccard
type: folder_brief_live
```
 
**AWS中的权限**

  

  

  

RAM权限：

  

[https://docs.aws.amazon.com/zh_cn/organizations/latest/userguide/orgs_introduction.html](https://docs.aws.amazon.com/zh_cn/organizations/latest/userguide/orgs_introduction.html)

  

SCP

  

IAM用户 可以配置上权限

  

角色 代入才能使用的权限

  

谁能使用 我（resource） 基于资源的策略

我（resource）能使用哪些 resource  执行角色

  

  

  

  

  

  

  

lambda serviceless权限配置

  

Statements 配置执行权限

managedPolicies： managedPolicies  托管的已经建好的策略

permissionsBoundary 权限边界

stackPolicy 配置给cloudformula的部署时的权限策略

  

  

lambda文档的权限概念有：

执行角色

resource-based policies for AWS Lambda： 授权允许eventbus调用lambda

权限边界限制（执行角色）

  

  

  

  

{

    "Version": "2012-10-17",

    "Statement": [

        {

            "Effect": "Allow",

            "Action": [

                "logs:CreateLogGroup",

                "logs:CreateLogStream",

                "logs:PutLogEvents"

            ],

            "Resource": "*"

        }

    ]

}

  

  

{

    "Version": "2012-10-17",

    "Statement": [

        {

            "Action": [

                "s3:PutBucketNotification",

                "s3:PutObject",

                "s3:GetObject",

                "s3:ListBucket",

                "s3:GetObjectTagging"

            ],

            "Resource": [

                "arn:aws:s3:::beta-indico-document-directory/*",

                "arn:aws:s3:::beta-indico-document-directory"

            ],

            "Effect": "Allow"

        },

        {

            "Action": [

                "ec2:CreateNetworkInterface",

                "ec2:AttachNetworkInterface",

                "ec2:DescribeNetworkInterfaces",

                "ec2:DeleteNetworkInterface"

            ],

            "Resource": "*",

            "Effect": "Allow"

        },

        {

            "Action": [

                "kafka-cluster:AlterGroup",

                "kafka-cluster:WriteDataIdempotently",

                "kafka-cluster:DescribeCluster",

                "kafka-cluster:ReadData",

                "kafka-cluster:DescribeTopic",

                "kafka-cluster:DescribeGroup",

                "kafka-cluster:Connect",

                "kafka-cluster:WriteData"

            ],

            "Resource": [

                "arn:aws:kafka:us-east-1:742593912130:group/dip-gamma/869ee2b9-3dd7-4e48-8ce1-0af161a0c897-21/*",

                "arn:aws:kafka:us-east-1:742593912130:cluster/dip-gamma/869ee2b9-3dd7-4e48-8ce1-0af161a0c897-21",

                "arn:aws:kafka:us-east-1:742593912130:topic/dip-gamma/869ee2b9-3dd7-4e48-8ce1-0af161a0c897-21/*",

                "arn:aws:kafka:us-east-1:742593912130:group/dip-gamma/869ee2b9-3dd7-4e48-8ce1-0af161a0c897-21/*"

            ],

            "Effect": "Allow"

        }

    ]

}

  

  

  

  

{

  "id": "cdc73f9d-aea9-11e3-9d5a-835b769c0d9c",

  "detail-type": "Scheduled Event",

  "source": "aws.events",

  "account": "123456789012",

  "time": "1970-01-01T00:00:00Z",

  "region": "us-east-1",

  "resources": [

    "arn:aws:events:us-east-1:123456789012:rule/ExampleRule"

  ],

  "detail": {}

}