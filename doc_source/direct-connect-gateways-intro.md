# Direct Connect gateways<a name="direct-connect-gateways-intro"></a>

Use *AWS Direct Connect gateway* to connect your VPCs\. You associate an *AWS Direct Connect gateway* with either of the following gateways: 
+ A transit gateway when you have multiple VPCs in the same Region
+ A virtual private gateway

 A Direct Connect gateway is a globally available resource\. You can create the Direct Connect gateway in any public Region and access it from all other public Regions\. You can use a Direct Connect gateway in the following scenarios\.

A Direct Connect gateway does not allow gateway associations that are on the same Direct Connect gateway to send traffic to each other \(for example, a virtual private gateway to another virtual private gateway\)\. A Direct Connect gateway does not prevent traffic from being sent from one gateway association back to the gateway association itself\. For example when you have an on\-premises supernet route that contains the prefixes from the gateway association\. If you have a configuration with multiple VPCs connected to the same transit gateway, the VPCs could communicate\. To prevent the VPCs from communicating, use separate transit gateway attachments, and then associate a route table with the attachments that have the **blackhole** option set\.

## Virtual private gateway associations<a name="virtual-private-gateway"></a>

In the following diagram, the Direct Connect gateway enables you to use your AWS Direct Connect connection in the US East \(N\. Virginia\) Region to access VPCs in your account in both the US East \(N\. Virginia\) and US West \(N\. California\) Regions\.

![\[Direct connect gateway\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/dx-gateway.png)

## Virtual private gateway associations across accounts<a name="virtual-private-gateway-across-accounts"></a>

Consider this scenario of a Direct Connect gateway owner \(Account Z\) who owns the Direct Connect gateway\. Account A and Account B want to use the Direct Connect gateway\. Account A and Account B each send an association proposal to Account Z\. Account Z accepts the association proposals and can optionally update the prefixes that are allowed from Account A's virtual private gateway or Account B's virtual private gateway\. After Account Z accepts the proposals, Account A and Account B can route traffic from their virtual private gateway to the Direct Connect gateway\. Account Z also owns the routing to the customers because Account Z owns the gateway\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/ma-vpc.png)

## Transit gateway associations<a name="transit-gateway"></a>

The following diagram illustrates how the Direct Connect gateway enables you to create a single connection to your Direct Connect connection that all of your VPCs can use\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/direct-connect-tgw.png)

The solution involves the following components:
+ A transit gateway that has VPC attachments\.
+ A Direct Connect gateway\.
+ An association between the Direct Connect gateway and the transit gateway\.
+ A transit virtual interface that is attached to the Direct Connect gateway\.

This configuration offers the following benefits\. You can:
+ Manage a single connection for multiple VPCs or VPNs that are in the same Region\.
+ Advertise prefixes from on\-premises to AWS and from AWS to on\-premises\.

For information about configuring transit gateways, see [Working with Transit Gateways](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-dcg-attachments.html) in the *Amazon VPC Transit Gateways Guide*\.

## Transit gateway associations across accounts<a name="transit-gateway-across-accounts"></a>

Consider this scenario of a Direct Connect gateway owner \(Account Z\) who owns the Direct Connect gateway\. Account A owns the transit gateway and wants to use the Direct Connect gateway\. Account Z accepts the association proposals and can optionally update the prefixes that are allowed from Account A's transit gateway\. After Account Z accepts the proposals, The VPCs attached to the transit gateway can route traffic from the transit gateway to the Direct Connect gateway\. Account Z also owns the routing to the customers because Account Z owns the gateway\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/direct-connect-ma-tgw.png)

**Topics**
+ [Virtual private gateway associations](#virtual-private-gateway)
+ [Virtual private gateway associations across accounts](#virtual-private-gateway-across-accounts)
+ [Transit gateway associations](#transit-gateway)
+ [Transit gateway associations across accounts](#transit-gateway-across-accounts)
+ [Creating a Direct Connect gateway](#create-direct-connect-gateway)
+ [Deleting Direct Connect gateways](#delete-direct-connect-gateway)
+ [Migrating from a virtual private gateway to a Direct Connect gateway](#migrate-to-direct-connect-gateway)

## Creating a Direct Connect gateway<a name="create-direct-connect-gateway"></a>

You can create a Direct Connect gateway in any supported public Region\. 

**To create a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect Gateways**\.

1. Choose **Create Direct Connect gateway**\.

1. Specify the following information, and choose **Create Direct Connect gateway**\.
   + **Name**: Enter a name to help you identify the Direct Connect gateway\.
   + **Amazon side ASN**: Specify the ASN for the Amazon side of the BGP session\. The ASN must be in the 64,512 to 65,534 range or 4,200,000,000 to 4,294,967,294 range\.
   + **Virtual private gateway**: To associate a virtual private gateway, choose the virtual private gateway\.

**To create a Direct Connect gateway using the command line or API**
+ [create\-direct\-connect\-gateway](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-direct-connect-gateway.html) \(AWS CLI\)
+ [CreateDirectConnectGateway](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateDirectConnectGateway.html) \(AWS Direct Connect API\)

## Deleting Direct Connect gateways<a name="delete-direct-connect-gateway"></a>

If you no longer require a Direct Connect gateway, you can delete it\. You must first disassociate all associated virtual private gateways and delete the attached private virtual interface\.

**To delete a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect Gateways**\.

1. Select the gateways and choose **Delete**\.

**To delete a Direct Connect gateway using the command line or API**
+ [delete\-direct\-connect\-gateway](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway.html) \(AWS CLI\)
+ [DeleteDirectConnectGateway](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGateway.html) \(AWS Direct Connect API\)

## Migrating from a virtual private gateway to a Direct Connect gateway<a name="migrate-to-direct-connect-gateway"></a>

If you had a virtual private gateway attached to a virtual interface, and you want to migrate to a Direct Connect gateway, perform the following steps:

**To migrate to a Direct Connect gateway**

1. Create a Direct Connect gateway\. For more information, see [Creating a Direct Connect gateway](#create-direct-connect-gateway)\.

1. Create a virtual interface for the Direct Connect gateway\. For more information, see [Creating a virtual interface](create-vif.md)\.

1. Associate the virtual private gateway with the Direct Connect gateway\. For more information, see [Associating and disassociating virtual private gateways](virtualgateways.md#associate-vgw-with-direct-connect-gateway)\.

1. Delete the virtual interface that was associated with the virtual private gateway\. For more information, see [Deleting virtual interfaces](deletevif.md)\.