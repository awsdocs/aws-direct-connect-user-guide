# Control Access to AWS Direct Connect Using Tags<a name="using_tags"></a>

You can control access to resources and requests by using tag key conditions\. You can also use a condition in your IAM policy to control whether specific tag keys can be used on a resource or in a request\. 

For information about how to use tags with AWS Identity and Access Management policies, see [Controlling Access Using Tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_iam-tags.html) in the *IAM User Guide*\.

## Example: Controlling Access to Resources<a name="actions"></a>

You can use conditions in your IAM policies to control access to AWS resources based on the tags on that resource\. You can do this by using the global **ResourceTag/`key-name`** condition key, or a service\-specific key such as **ResourceTag/`key-name`**\. You can also use these condition keys to allow untagging resources only with specific tag key–value pairs\.

**Note**  
Do not use the **ResourceTag** condition key in a policy with the **iam:PassRole **action\. You cannot use the tag on an IAM role to control who has access to pass that role\. For more information about the permissions required to pass a role to a service, see [Granting a User Permissions to Pass a Role to an AWS Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_passrole.html) in the *IAM User Guide*\.

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

## Example: Controlling Access to Requests<a name="requests"></a>

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

## Example: Controlling Tag Keys<a name="keys"></a>

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