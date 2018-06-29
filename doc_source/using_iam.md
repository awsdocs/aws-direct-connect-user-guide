# Control Access to AWS Direct Connect Using AWS Identity and Access Management<a name="using_iam"></a>

You can use features of AWS Identity and Access Management to specify which AWS Direct Connect actions a user under your AWS account can perform\. For example, you could create an IAM policy that grants only certain users in your organization permission to use the `DescribeConnections` action to retrieve data about your AWS Direct Connect connections\.

Permissions granted using IAM cover all AWS resources you use with AWS Direct Connect\. You cannot use IAM to control access to specific AWS resources \(also known as resource\-level permissions\)\. For example, you cannot grant a user access to data for only a specific virtual interface\.

## AWS Direct Connect Actions<a name="actions"></a>

In an IAM policy, you can specify any or all actions that AWS Direct Connect offers\. The action name must include the lowercase prefix `directconnect:`\. For example: `directconnect:DescribeConnections`, `directconnect:CreateConnection`, or `directconnect:*` \(for all AWS Direct Connect actions\)\. For a list of the actions, see the [AWS Direct Connect API Reference](http://docs.aws.amazon.com/directconnect/latest/APIReference/)\.

## AWS Direct Connect Resources<a name="iam-dx-resources"></a>

AWS Direct Connect does not support resource\-level permissions; therefore, you cannot control access to specific AWS Direct Connect resources\. You must use an asterisk \(`*`\) to specify the resource when writing a policy to control access to AWS Direct Connect actions\. 

## AWS Direct Connect Keys<a name="keys"></a>

AWS Direct Connect implements the following policy keys:
+ `aws:CurrentTime` \(for date/time conditions\)
+ `aws:EpochTime` \(the date in epoch or UNIX time, for use with date/time conditions\)
+ `aws:SecureTransport` \(Boolean representing whether the request was sent using SSL\)
+ `aws:SourceIp` \(the requester's IP address, for use with IP address conditions\)
+ `aws:UserAgent` \(information about the requester's client application, for use with string conditions\)

If you use `aws:SourceIp`, and the request comes from an Amazon EC2 instance, the instance's public IP address is used to determine if access is allowed\.

For services that use only SSL, such as Amazon Relational Database Service and Amazon Route 53, the `aws:SecureTransport` key has no meaning\.

For more information, see [Condition](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

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

For more information about writing IAM policies, see [IAM Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) in the *IAM User Guide*\.