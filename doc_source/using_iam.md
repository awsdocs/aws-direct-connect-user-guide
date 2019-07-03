# Control Access to AWS Direct Connect Using AWS Identity and Access Management<a name="using_iam"></a>

You can use features of AWS Identity and Access Management to specify the AWS Direct Connect actions or resources that a user under your AWS account can perform\. For example, you can create an IAM policy that grants only certain users in your organization permission to use the `DescribeConnections` action to retrieve data about your AWS Direct Connect connections\.

In an IAM policy, you can specify any or all actions that AWS Direct Connect offers\. The action name must include the lowercase prefix `directconnect:`\. For example: `directconnect:DescribeConnections`, `directconnect:CreateConnection`, or `directconnect:*` \(for all AWS Direct Connect actions\)\. 

For information about the actions, resources, and keys that you can use with AWS Direct Connect, see [Actions, Resources, and Condition Keys for AWS Direct Connect](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awsdirectconnect.html#awsdirectconnect-resources-for-iam-policies) in the *IAM User Guide*\.

## Example Policies for AWS Direct Connect<a name="example_policy"></a>

The following example policy grants read access to AWS Direct Connect\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "directconnect:Describe*",
                "ec2:DescribeVpnGateways"
            ],
            "Resource": "*"
        }
    ]
}
```

The following example policy grants full access to AWS Direct Connect\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "directconnect:*",
                "ec2:DescribeVpnGateways"
            ],
            "Resource": "*"
        }
    ]
}
```

For more information about writing IAM policies, see [IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) in the *IAM User Guide*\.