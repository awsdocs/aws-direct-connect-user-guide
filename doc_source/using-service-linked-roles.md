# Using Service\-Linked Roles for AWS Direct Connect<a name="using-service-linked-roles"></a>

AWS Direct Connect uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to AWS Direct Connect\. Service\-linked roles are predefined by AWS Direct Connect and include all the permissions that the service requires to call other AWS services on your behalf\. 

A service\-linked role makes setting up AWS Direct Connect easier because you don’t have to manually add the necessary permissions\. AWS Direct Connect defines the permissions of its service\-linked roles, and unless defined otherwise, only AWS Direct Connect can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

You can delete a service\-linked role only after first deleting their related resources\. This protects your AWS Direct Connect resources because you can't inadvertently remove permission to access the resources\.

For information about other services that support service\-linked roles, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes **in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-Linked Role Permissions for AWS Direct Connect<a name="slr-permissions"></a>

AWS Direct Connect uses the service\-linked role named **AWSServiceRoleForDirectConnect** – Allows AWS Direct Connect to retrieve the MACsec secrets that are stored in AWS Secrets Manager on your behalf\.

The AWSServiceRoleForDirectConnect service\-linked role trusts the following services to assume the role:
+ `directconnect.amazon.com`

The role permissions policy allows AWS Direct Connect to complete the following actions on the specified resources:
+ Action: `secretsmanager:DescribeSecret` on `AWS Secrets Manager with prefixed resources, for example: arn:aws:secretsmanager:*:*:secret:*directconnect*`
+ Action: `secretsmanager:ListSecretVersionIds` on `AWS Secrets Manager with prefixed resources, for example: arn:aws:secretsmanager:*:*:secret:*directconnect*`
+ Action: `secretsmanager:GetSecretValue` on `AWS Secrets Manager with prefixed resources, for example: arn:aws:secretsmanager:*:*:secret:*directconnect*`

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating a Service\-Linked Role for AWS Direct Connect<a name="create-slr"></a>

You don't need to manually create a service\-linked role\. When you run the `associate-mac-sec-key command`, AWS creates a service linked role that allows AWS Direct Connect team to retrieve AWS Direct Connect to retrieve the MACsec secrets that are stored in AWS Secrets Manager on your behalf in the AWS Management Console, the AWS CLI, or the AWS API, AWS Direct Connect creates the service\-linked role for you\. 

**Important**  
This service\-linked role can appear in your account if you completed an action in another service that uses the features supported by this role\. To learn more, see [A New Role Appeared in My IAM Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_roles.html#troubleshoot_roles_new-role-appeared)\.

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. AWS Direct Connect creates the service\-linked role for you again\. 

You can also use the IAM console to create a service\-linked role with the **AWS Direct Connect** use case\. In the AWS CLI or the AWS API, create a service\-linked role with the `directconnect.amazon.com` service name\. For more information, see [Creating a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\. If you delete this service\-linked role, you can use this same process to create the role again\.

## Editing a Service\-Linked Role for AWS Direct Connect<a name="edit-slr"></a>

AWS Direct Connect does not allow you to edit the AWSServiceRoleForDirectConnect service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.