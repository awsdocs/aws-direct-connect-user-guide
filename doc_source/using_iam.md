# Using AWS Identity and Access Management with AWS Direct Connect<a name="using_iam"></a>

You can use AWS Identity and Access Management with AWS Direct Connect to specify which AWS Direct Connect actions a user under your AWS account can perform\. For example, you could create an IAM policy that gives only certain users in your organization permission to use the `DescribeConnections` action to retrieve data about your AWS Direct Connect connections\.

Permissions granted using IAM cover all the AWS resources you use with AWS Direct Connect, so you cannot use IAM to control access to AWS Direct Connect data for specific resources\. For example, you cannot give a user access to AWS Direct Connect data for only a specific virtual interface\.

**Important**  
Using AWS Direct Connect with IAM doesn't change how you use AWS Direct Connect\. There are no changes to AWS Direct Connect actions, and no new AWS Direct Connect actions related to users and access control\. For an example of a policy that covers AWS Direct Connect actions, see [Example Policy for AWS Direct Connect](#example_policy)\.

## AWS Direct Connect Actions<a name="actions"></a>

In an IAM policy, you can specify any or all actions that AWS Direct Connect offers\. The action name must include the lowercase prefix `directconnect:`\. For example: `directconnect:DescribeConnections`, `directconnect:CreateConnection`, or `directconnect:*` \(for all AWS Direct Connect actions\)\. For a list of the actions, see the *AWS Direct Connect API Reference*\.

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

**Note**  
For services that use only SSL, such as Amazon Relational Database Service and Amazon Route 53, the `aws:SecureTransport` key has no meaning\.

Key names are case\-insensitive\. For example, `aws:CurrentTime` is equivalent to `AWS:currenttime`\.

For more information about policy keys, see [Condition](http://docs.aws.amazon.com/IAM/latest/UserGuide/AccessPolicyLanguage_ElementDescriptions.html#Condition) in *IAM User Guide*\.

## Example Policy for AWS Direct Connect<a name="example_policy"></a>

This section shows a simple policy for controlling user access to AWS Direct Connect\.

**Note**  
In the future, AWS Direct Connect might add new actions that should logically be included in the following policy, based on the policy’s stated goals\.

Example

The following sample policy allows a group to retrieve any AWS Direct Connect data, but not create or delete any resources\.

```
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "directconnect:Describe*"
      ],
      "Resource": "*"
    }
  ]
}
```

For more information about writing IAM policies, see [Overview of IAM Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) in the *IAM User Guide*\.