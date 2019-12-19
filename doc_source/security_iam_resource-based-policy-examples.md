# AWS Direct Connect Resource\-Based Policy Examples<a name="security_iam_resource-based-policy-examples"></a>

You can control access to resources and requests by using tag key conditions\. You can also use a condition in your IAM policy to control whether specific tag keys can be used on a resource or in a request\. 

For information about how to use tags with AWS Identity and Access Management policies, see [Controlling Access Using Tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_iam-tags.html) in the *IAM User Guide*\.

## Associating Direct Connect Virtual Interfaces Based on Tags<a name="security_iam_resource-based-policy-examples-associate-interface"></a>

The following example shows how you might create a policy that allows associating a virtual interface only if the tag contains the environment key and the preprod or production values\. 

```
       {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "directconnect:AssociateVirtualInterface"
          ],
          "Resource": "arn:aws:directconnect:*:*:dxvif/*",
          "Condition": {
            "StringEquals": {
              "aws:ResourceTag/environment": [
                "preprod",
                "production"
              ]
            }
          }
        },
        {
          "Effect": "Allow",
          "Action": "directconnect:DescribeVirtualInterfaces",
          "Resource": "*"
        }
      ]
    }
```

## Controlling Access to Requests Based on Tags<a name="security_iam_resource-based-policy-examples-associate-interface-requests"></a>

You can use conditions in your IAM policies to control which tag key–value pairs can be passed in a request that tags an AWS resource\. The following example shows how you might create a policy that allows using the AWS Direct Connect TagResource action to attach tags to a virtual interface only if the tag contains the environment key and the preprod or production values\. As a best practice, use the `ForAllValues` modifier with the `aws:TagKeys` condition key to indicate that only the key environment is allowed in the request\. 

```
    {
        "Version": "2012-10-17",
        "Statement": {
            "Effect": "Allow",
            "Action": "directconnect:TagResource",
            "Resource": "arn:aws:directconnect:*:*:dxvif/*",
            "Condition": {
                "StringEquals": {
                    "aws:RequestTag/environment": [
                        "preprod",
                        "production"
                    ]
                },
                "ForAllValues:StringEquals": {"aws:TagKeys": "environment"}
            }
        }
    }
```

## Controlling Tag Keys<a name="security_iam_resource-based-policy-examples-associate-interface-keys"></a>

You can use a condition in your IAM policies to control whether specific tag keys can be used on a resource or in a request\. 

The following example shows how you might create a policy that allows you to tag resources, but only with the tag key environment

```
     {
      "Version": "2012-10-17",
      "Statement": {
        "Effect": "Allow",
        "Action": "directconnect:TagResource",
        "Resource": "*",
        "Condition": {
          "ForAllValues:StringEquals": {
            "aws:TagKeys": [
              "environment"
            ]
          }
        }
      }
    }
```