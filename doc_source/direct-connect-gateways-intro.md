# Direct Connect Gateways<a name="direct-connect-gateways-intro"></a>

Use *AWS Direct Connect gateway* to connect your VPCs\. You associate an *AWS Direct Connect gateway* with either of the following gateways: 
+ A transit gateway when you have multiple VPCs in the same Region
+ A virtual private gateway

 A Direct Connect gateway is a globally available resource\. You can create the Direct Connect gateway in any public Region and access it from all other public Regions\.

**Topics**
+ [Creating a Direct Connect Gateway](#create-direct-connect-gateway)
+ [Deleting Direct Connect Gateways](#delete-direct-connect-gateway)
+ [Migrating from a Virtual Private Gateway to a Direct Connect Gateway](#migrate-to-direct-connect-gateway)

## Creating a Direct Connect Gateway<a name="create-direct-connect-gateway"></a>

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

## Deleting Direct Connect Gateways<a name="delete-direct-connect-gateway"></a>

If you no longer require a Direct Connect gateway, you can delete it\. You must first disassociate all associated virtual private gateways and delete the attached private virtual interface\.

**To delete a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect Gateways**\.

1. Select the gateways and choose **Delete**\.

**To delete a Direct Connect gateway using the command line or API**
+ [delete\-direct\-connect\-gateway](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway.html) \(AWS CLI\)
+ [DeleteDirectConnectGateway](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGateway.html) \(AWS Direct Connect API\)

## Migrating from a Virtual Private Gateway to a Direct Connect Gateway<a name="migrate-to-direct-connect-gateway"></a>

If you had a virtual private gateway attached to a virtual interface, and you want to migrate to a Direct Connect gateway, perform the following steps:

**To migrate to a Direct Connect gateway**

1. Create a Direct Connect gateway\. For more information, see [Creating a Direct Connect Gateway](#create-direct-connect-gateway)\.

1. Create a virtual interface for the Direct Connect gateway\. For more information, see [Creating a Virtual Interface](create-vif.md)\.

1. Associate the virtual private gateway with the Direct Connect gateway\. For more information, see [Associating and Disassociating Virtual Private Gateways](virtualgateways.md#associate-vgw-with-direct-connect-gateway)\.

1. Delete the virtual interface that was associated with the virtual private gateway\. For more information, see [Deleting Virtual Interfaces](deletevif.md)\.