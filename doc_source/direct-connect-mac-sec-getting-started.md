# Get started with MACsec on dedicated connections<a name="direct-connect-mac-sec-getting-started"></a>

The following tasks help you become familiar with MACsec on AWS Direct Connect dedicated connections\.

Follow these steps to create a connection with MACsec support, and then associate a CKN/CAK pair with the connection\.

**Topics**
+ [MACsec prerequisites](#mac-sec-prerequisites)
+ [Service\-Linked roles](#mac-sec-service-linked-roles)
+ [MACsec pre\-shared CKN/CAK key considerations](#mac-sec-key-consideration)
+ [Step 1: Create a connection](#step-create-connection)
+ [\(Optional\) Step 2: Create a link aggregation group \(LAG\)](#step-create-lag)
+ [Step 3: Associate the CKN/CAK with the connection or LAG](#step-associate-key)
+ [Step 4: Configure your on\-premises router](#associate-key-router)
+ [Step 5: \(Optional\) Remove the association between the CKN/CAK and the connection or LAG](#step-disassociate-key)

## MACsec prerequisites<a name="mac-sec-prerequisites"></a>

Complete the following tasks before you configure MACsec on a dedicated connection\.
+ Create a CKN/CAK pair for the MACsec secret key\.

  You can create the pair using an open standard tool\. The pair must meet the requirements specified in [Step 4: Configure your on\-premises router](#associate-key-router)\.
+ MACsec is available on dedicated connections for certain AWS Direct Connect Partners\. For information about which AWS Direct Connect Partners support MACsec, see [AWS Direct Connect](https://aws.amazon.com/directconnect/?nc=sn&loc=0)\.
+ Make sure that you have a device on your end of the connection that supports MACsec\.

## Service\-Linked roles<a name="mac-sec-service-linked-roles"></a>

AWS Direct Connect uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to AWS Direct Connect\. Service\-linked roles are predefined by AWS Direct Connect and include all of the permissions that the service requires to call other AWS services on your behalf\. A service\-linked role makes setting up AWS Direct Connect easier because you don’t have to manually add the necessary permissions\. AWS Direct Connect defines the permissions of its service\-linked roles, and unless defined otherwise, only AWS Direct Connect can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\. For more information, see [Using Service\-Linked Roles for AWS Direct Connect](using-service-linked-roles.md)\.

## MACsec pre\-shared CKN/CAK key considerations<a name="mac-sec-key-consideration"></a>

AWS Direct Connect uses Service Linked Secrets \(SLS\), a feature of AWS Secrets Manager, to store the pre\-shared keys that you associate with connections or LAGs\. Secrets Manager stores your pre\-shared CKN and CAK pairs as a secret that Secrets Manager’s master key encrypts\. The stored key is read\-only by design, but you can schedule a seven\- to thirty\-day deletion using the AWS Secrets Manager console or API\. When you schedule a deletion, the CKN cannot be read, and this might affect your network connectivity\. We apply the following rules when this happens:
+ If the connection is in a pending state, we disassociate the CKN from the connection\.
+ If the connection is in an available state, we notify the connection owner by email\. If you do not take any action within 30 days, we disassociate the CKN from your connection\.

When we disassociate the last CKN from your connection and the connection encryption mode is set to "must encrypt", we set the mode to "should\_encrypt" to prevent sudden packet loss\.

## Step 1: Create a connection<a name="step-create-connection"></a>

 To start using MACsec, you must turn the feature on when you create a dedicated connection\. For more information, see [Create a connection](create-connection.md)\.

## \(Optional\) Step 2: Create a link aggregation group \(LAG\)<a name="step-create-lag"></a>

 If you use multiple connections for redundancy, you can create a LAG that supports MACsec\. For more information, see [MACsec considerations](lags.md#lag-macsec-considerations) and [Create a LAG](create-lag.md)\.

## Step 3: Associate the CKN/CAK with the connection or LAG<a name="step-associate-key"></a>

After you create the connection or LAG that supports MACsec, you need to associate a CKN/CAK with the connection\. For more information, see one of the following:
+ [Associate a MACsec CKN/CAK with a connection](associate-key-connection.md)
+ [Associate a MACsec CKN/CAK with a LAG](associate-key-lag.md)

## Step 4: Configure your on\-premises router<a name="associate-key-router"></a>

Update your on\-premises router with the MACsec secret key\. The MACsec secret key on the on\-premises router and in the AWS Direct Connect location must match\. For more information, see [Download the router configuration file](create-vif.md#vif-router-config)\.

## Step 5: \(Optional\) Remove the association between the CKN/CAK and the connection or LAG<a name="step-disassociate-key"></a>

If you need to remove the association between the MACsec key and the connection or LAG, see one of the following:
+ [Remove the association between a MACsec secret key and a connection](disassociate-key-connection.md)
+ [Remove the association between a MACsec secret key and a LAG](disassociate-key-lag.md)