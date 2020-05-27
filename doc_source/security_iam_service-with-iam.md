# How AWS Direct Connect works with IAM<a name="security_iam_service-with-iam"></a>

Before you use IAM to manage access to Direct Connect, you should understand what IAM features are available to use with Direct Connect\. To get a high\-level view of how Direct Connect and other AWS services work with IAM, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide*\.

**Topics**
+ [Direct Connect identity\-based policies](#security_iam_service-with-iam-id-based-policies)
+ [Direct Connect resource\-based policies](#security_iam_service-with-iam-resource-based-policies)
+ [Authorization based on Direct Connect tags](#security_iam_service-with-iam-tags)
+ [Direct Connect IAM roles](#security_iam_service-with-iam-roles)

## Direct Connect identity\-based policies<a name="security_iam_service-with-iam-id-based-policies"></a>

With IAM identity\-based policies, you can specify allowed or denied actions and resources as well as the conditions under which actions are allowed or denied\. Direct Connect supports specific actions, resources, and condition keys\. To learn about all of the elements that you use in a JSON policy, see [IAM JSON Policy Elements Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html) in the *IAM User Guide*\.

### Actions<a name="security_iam_service-with-iam-id-based-policies-actions"></a>

The `Action` element of an IAM identity\-based policy describes the specific action or actions that will be allowed or denied by the policy\. Policy actions usually have the same name as the associated AWS API operation\. The action is used in a policy to grant permissions to perform the associated operation\. 

Policy actions in Direct Connect use the following prefix before the action: `directconnect:`\. For example, to grant someone permission to run an Amazon EC2 instance with the Amazon EC2 `DescribeVpnGateways` API operation, you include the `ec2:DescribeVpnGateways` action in their policy\. Policy statements must include either an `Action` or `NotAction` element\. Direct Connect defines its own set of actions that describe tasks that you can perform with this service\.

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



To see a list of Direct Connect actions, see [Actions Defined by AWS Direct Connect](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awskeymanagementservice.html#awskeymanagementservice-actions-as-permissions) in the *IAM User Guidelist\_awsdirectconnect\.html*\.

### Resources<a name="security_iam_service-with-iam-id-based-policies-resources"></a>

The `Resource` element specifies the object or objects to which the action applies\. Statements must include either a `Resource` or a `NotResource` element\. You specify a resource using an ARN or using the wildcard \(\*\) to indicate that the statement applies to all resources\.



Direct Connect uses the following ARNs:


**Direct connect resource ARNs**  

| Resource Type | ARN | 
| --- | --- | 
| dxcon | arn:$\{Partition\}:directconnect:$\{Region\}:$\{Account\}:dxcon/$\{ConnectionId\} | 
| dxlag |  arn:$\{Partition\}:directconnect:$\{Region\}:$\{Account\}:dxlag/$\{LagId\} | 
| dx\-vif | arn:$\{Partition\}:directconnect:$\{Region\}:$\{Account\}:dxvif/$\{VirtualInterfaceId\} | 
| dx\-gateway | arn:$\{Partition\}:directconnect::$\{Account\}:dx\-gateway/$\{DirectConnectGatewayId\} | 

For more information about the format of ARNs, see [Amazon Resource Names \(ARNs\) and AWS Service Namespaces](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)\.

For example, to specify the `dxcon-11aa22bb` interface in your statement, use the following ARN:

```
"Resource": "arn:aws:directconnect:us-east-1:123456789012:dxcon/dxcon-11aa22bb
```

To specify all virtual interfaces that belong to a specific account, use the wildcard \(\*\):

```
"Resource": "arn:aws:directconnect:*:*:dxvif/*"
```

Some Direct Connect actions, such as those for creating resources, cannot be performed on a specific resource\. In those cases, you must use the wildcard \(\*\)\.

```
"Resource": "*"
```

To see a list of Direct Connect resource types and their ARNs, see [Resource Types Defined by AWS Direct Connect](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awsdirectconnect.html#awsdirectconnect-resources-for-iam-policies) in the *IAM User Guide*\. To learn with which actions you can specify the ARN of each resource, see [Actions Defined by AWS Direct Connect](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awskeymanagementservice.html#awskeymanagementservice-actions-as-permissions)\.

### Condition keys<a name="security_iam_service-with-iam-id-based-policies-conditionkeys"></a>

The `Condition` element \(or `Condition` *block*\) lets you specify conditions in which a statement is in effect\. The `Condition` element is optional\. You can build conditional expressions that use [condition operators](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html), such as equals or less than, to match the condition in the policy with values in the request\. 

If you specify multiple `Condition` elements in a statement, or multiple keys in a single `Condition` element, AWS evaluates them using a logical `AND` operation\. If you specify multiple values for a single condition key, AWS evaluates the condition using a logical `OR` operation\. All of the conditions must be met before the statement's permissions are granted\.

 You can also use placeholder variables when you specify conditions\. For example, you can grant an IAM user permission to access a resource only if it is tagged with their IAM user name\. For more information, see [IAM Policy Elements: Variables and Tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_variables.html) in the *IAM User Guide*\. 

Direct Connect defines its own set of condition keys and also supports using some global condition keys\. To see all AWS global condition keys, see [AWS Global Condition Context Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) in the *IAM User Guide*\.



You can use condition keys with the tag resource\. For more information, see [Example: Restricting Access to a Specific Region](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ExamplePolicies_EC2.html#iam-example-region)\. 

To see a list of Direct Connect condition keys, see [Condition Keys for AWS Direct Connect](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awskeymanagementservice.html#awskeymanagementservice-policy-keys) in the *IAM User Guide*\. To learn with which actions and resources you can use a condition key, see [Actions Defined by AWS Direct Connect](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awskeymanagementservice.html#awskeymanagementservice-actions-as-permissions)\.

### Examples<a name="security_iam_service-with-iam-id-based-policies-examples"></a>



To view examples of Direct Connect identity\-based policies, see [AWS Direct Connect identity\-based policy examples](security_iam_id-based-policy-examples.md)\.

## Direct Connect resource\-based policies<a name="security_iam_service-with-iam-resource-based-policies"></a>

You can control access to resources and requests by using tag key conditions\. You can also use a condition in your IAM policy to control whether specific tag keys can be used on a resource or in a request\. 

For information about how to use tags with AWS Identity and Access Management policies, see [Controlling Access Using Tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_iam-tags.html) in the *IAM User Guide*\.

### Examples<a name="security_iam_service-with-iam-resource-based-policies-examples"></a>



To view examples of Direct Connect resource\-based policies, see [AWS Direct Connect resource\-based policy examples](security_iam_resource-based-policy-examples.md)\.

## Authorization based on Direct Connect tags<a name="security_iam_service-with-iam-tags"></a>

You can attach tags to Direct Connect resources or pass tags in a request to Direct Connect\. To control access based on tags, you provide tag information in the [condition element](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) of a policy using the `directconnect:ResourceTag/key-name`, `aws:RequestTag/key-name`, or `aws:TagKeys` condition keys\. For more information about tagging Direct Connect resources, see [Tagging AWS Direct Connect resources](using-tags.md)\.\.

To view an example identity\-based policy for limiting access to a resource based on the tags on that resource, see [Associating Direct Connect virtual interfaces based on tags](security_iam_resource-based-policy-examples.md#security_iam_resource-based-policy-examples-associate-interface)\.

## Direct Connect IAM roles<a name="security_iam_service-with-iam-roles"></a>

An [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) is an entity within your AWS account that has specific permissions\.

### Using temporary credentials with Direct Connect<a name="security_iam_service-with-iam-roles-tempcreds"></a>

You can use temporary credentials to sign in with federation, assume an IAM role, or to assume a cross\-account role\. You obtain temporary security credentials by calling AWS STS API operations such as [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) or [GetFederationToken](https://docs.aws.amazon.com/STS/latest/APIReference/API_GetFederationToken.html)\. 

Direct Connect supports using temporary credentials\. 

### Service\-linked roles<a name="security_iam_service-with-iam-roles-service-linked"></a>

[Service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role) allow AWS services to access resources in other services to complete an action on your behalf\. Service\-linked roles appear in your IAM account and are owned by the service\. An IAM administrator can view but not edit the permissions for service\-linked roles\.

Direct Connect does not support service\-linked roles\.

### Service roles<a name="security_iam_service-with-iam-roles-service"></a>

This feature allows a service to assume a [service role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-role) on your behalf\. This role allows the service to access resources in other services to complete an action on your behalf\. Service roles appear in your IAM account and are owned by the account\. This means that an IAM administrator can change the permissions for this role\. However, doing so might break the functionality of the service\.

Direct Connect supports service roles\. 