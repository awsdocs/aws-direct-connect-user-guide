# Direct Connect Gateways<a name="direct-connect-gateways"></a>

You can use an *AWS Direct Connect gateway* to connect your AWS Direct Connect connection over a private virtual interface to one or more VPCs in your account that are located in the same or different regions\. You associate a Direct Connect gateway with the virtual private gateway for the VPC, and then create a private virtual interface for your AWS Direct Connect connection to the Direct Connect gateway\. You can attach multiple private virtual interfaces to your Direct Connect gateway\.

A Direct Connect gateway is a globally available resource\. You can create the Direct Connect gateway in any public region and access it from all other public regions\.

In the following diagram, the Direct Connect gateway enables you to use your AWS Direct Connect connection in the US East \(N\. Virginia\) region to access VPCs in your account in both the US East \(N\. Virginia\) and US West \(N\. California\) regions\.

![\[Direct connect gateway\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/dx-gateway-diagram.png)

The following rules apply:
+ You cannot use a Direct Connect gateway to connect to a VPC in the China regions\.
+ You cannot use a Direct Connect gateway that's in your account to connect to a VPC that's in a different AWS account\. To associate a Direct Connect gateway with a virtual private gateway, it must be in the same account as the virtual private gateway\.
+ There are limits for creating and using Direct Connect gateways\. For more information, see [AWS Direct Connect Limits](Welcome.md#directconnect_limits)\.
+ The VPCs to which you connect through a Direct Connect gateway cannot have overlapping CIDR blocks\. If you add an IPv4 CIDR block to a VPC that's associated with a Direct Connect gateway, ensure that the CIDR block does not overlap with an existing CIDR block for any other associated VPC\. For more information, see [Adding IPv4 CIDR Blocks to a VPC](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Subnets.html#vpc-resize) in the *Amazon VPC User Guide*\.
+ You cannot create a public virtual interface to a Direct Connect gateway\.
+ A Direct Connect gateway supports communication between attached private virtual interfaces and associated virtual private gateways only\. The following traffic flows are not supported:
  + Direct communication between the VPCs that are associated with the Direct Connect gateway\.
  + Direct communication between the virtual interfaces that are attached to the Direct Connect gateway\.
  + Direct communication between a virtual interface attached to a Direct Connect gateway and a VPN connection on a virtual private gateway that's associated with the same Direct Connect gateway\.
+ You cannot associate a virtual private gateway with more than one Direct Connect gateway and you cannot attach a private virtual interface to more than one Direct Connect gateway\.
+ A virtual private gateway that you associate with a Direct Connect gateway must be attached to a VPC\.
+ You cannot tag a Direct Connect gateway\.

To connect your AWS Direct Connect connection to a VPC in the same region only, you can create a Direct Connect gateway or you can create a private virtual interface and attach it to the virtual private gateway for the VPC\. For more information, see [Creating a Private Virtual Interface](create-vif.md#create-private-vif) and [VPN CloudHub](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPN_CloudHub.html)\.

To use your AWS Direct Connect connection with a VPC in another account, you can create a hosted private virtual interface for that account\. When the owner of the other account accepts the hosted virtual interface, they can choose to attach it to either a virtual private gateway or a Direct Connect gateway in their account\. For more information, see [Virtual Interfaces](WorkingWithVirtualInterfaces.md)\.

**Topics**
+ [Creating a Direct Connect Gateway](#create-direct-connect-gateway)
+ [Associating and Disassociating Virtual Private Gateways](#associate-vgw-with-direct-connect-gateway)
+ [Creating a Private Virtual Interface to the Direct Connect Gateway](#create-private-vif-for-gateway)
+ [Deleting a Direct Connect Gateway](#delete-direct-connect-gateway)

## Creating a Direct Connect Gateway<a name="create-direct-connect-gateway"></a>

You can create a Direct Connect gateway in any supported public region\. 

**To create a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Direct Connect Gateways**\.

1. Choose **Create Direct Connect Gateway**\.

1. Specify the following information, and choose **Create**\.
   + **Name**: Enter a name to help you identify the Direct Connect gateway\.
   + **Amazon side ASN**: Specify the ASN for the Amazon side of the BGP session\. The ASN must be in the 64,512 to 65,534 range or 4,200,000,000 to 4,294,967,294 range\.

**To create a Direct Connect gateway using the command line or API**
+ [create\-direct\-connect\-gateway](http://docs.aws.amazon.com/cli/latest/reference/directconnect/create-direct-connect-gateway.html) \(AWS CLI\)
+ [CreateDirectConnectGateway](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateDirectConnectGateway.html) \(AWS Direct Connect API\)

## Associating and Disassociating Virtual Private Gateways<a name="associate-vgw-with-direct-connect-gateway"></a>

To associate a virtual private gateway with a Direct Connect gateway, you must be in the region in which the virtual private gateway is located\. The virtual private gateway must be attached to the VPC to which you want to connect\. For more information, see [Create a Virtual Private Gateway](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_VPN.html#vpn-create-vpg) in the *Amazon VPC User Guide*\.

**Note**  
If you are planning to use the virtual private gateway for a Direct Connect gateway and a dynamic VPN connection, set the ASN on the virtual private gateway to the value you require for the VPN connection\. Otherwise, the ASN on the virtual private gateway can be set to any permitted value\. The Direct Connect gateway advertises all connected VPCs over the ASN assigned to it\.

**To associate a virtual private gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. Use the region selector to select the region in which your virtual private gateway is located\.

1. In the navigation pane, choose **Direct Connect Gateways** and select the Direct Connect gateway\.

1. Choose **Actions**, **Associate Virtual Private Gateway**\.

1. Select the virtual private gateways to associate, and choose **Associate**\.

You can view all the virtual private gateways in all regions that are associated with the Direct Connect gateway by choosing **Virtual Gateway Associations**\. To disassociate a virtual private gateway from a Direct Connect gateway, you must be in the region in which the virtual private gateway is located\.

**To disassociate a virtual private gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. Use the region selector to switch to the region in which your virtual private gateway is located\.

1. In the navigation pane, choose **Direct Connect Gateways** and select the Direct Connect gateway\.

1. Choose **Actions**, **Disassociate Virtual Private Gateway**\.

1. Select the virtual private gateways to disassociate, and choose **Disassociate**\.

**To associate a virtual private gateway using the command line or API**
+ [create\-direct\-connect\-gateway\-association](http://docs.aws.amazon.com/cli/latest/reference/directconnect/create-direct-connect-gateway-association.html) \(AWS CLI\)
+ [CreateDirectConnectGatewayAssociation](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)

**To view the virtual private gateways associated with a Direct Connect gateway using the command line or API**
+ [describe\-direct\-connect\-gateway\-associations](http://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-associations.html) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAssociations](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAssociations.html) \(AWS Direct Connect API\)

**To disassociate a virtual private gateway using the command line or API**
+ [delete\-direct\-connect\-gateway\-association](http://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway-association.html) \(AWS CLI\)
+ [DeleteDirectConnectGatewayAssociation](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)

## Creating a Private Virtual Interface to the Direct Connect Gateway<a name="create-private-vif-for-gateway"></a>

To connect your AWS Direct Connect connection to the remote VPC, you must create a private virtual interface for your connection and specify the Direct Connect gateway to which to connect\.

**Note**  
If you're accepting a hosted private virtual interface, you can associate it with a Direct Connect gateway in your account\. For more information, see [Accepting a Hosted Virtual Interface](accepthostedvirtualinterface.md)\.

**To provision a private virtual interface to a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Connections**, select the connection to use, and choose **Actions**, **Create Virtual Interface**\.

1. In the **Create a Virtual Interface** pane, select **Private**\.  
![\[Create a Virtual Interface screen\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/create_virtual_interface_private.png)

1. Under **Define Your New Private Virtual Interface**, do the following and choose **Continue**:

   1. For **Virtual Interface Name**, enter a name for the virtual interface\.

   1. For **Virtual Interface Owner**, select the **My AWS Account** option if the virtual interface is for your AWS account\.

   1. For **Connection To**, choose **Direct Connect Gateway** and select the Direct Connect gateway\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\.

   1. If you're configuring an IPv4 BGP peer, choose **IPv4**, and do the following:
      + To have AWS generate your router IP address and Amazon IP address, select **Auto\-generate peer IPs**\.
      + To specify these IP addresses yourself, clear the **Auto\-generate peer IPs** check box\. For **Your router peer IP**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to AWS\. 

   1. If you're configuring an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

   1. To have AWS generate a BGP key, select the **Auto\-generate BGP key** check box \.

      To provide your own BGP key, clear the **Auto\-generate BGP key** check box\. For **BGP Authentication Key**, enter your BGP MD5 key\.

After you've created the virtual interface, you can download the router configuration for your device\. For more information, see [Downloading the Router Configuration File](create-vif.md#vif-router-config)\.

**To create a private virtual interface using the command line or API**
+ [create\-private\-virtual\-interface](http://docs.aws.amazon.com/cli/latest/reference/directconnect/create-private-virtual-interface.html) \(AWS CLI\)
+ [CreatePrivateVirtualInterface](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreatePrivateVirtualInterface.html) \(AWS Direct Connect API\)

**To view the virtual interfaces that are attached to a Direct Connect gateway using the command line or API**
+ [describe\-direct\-connect\-gateway\-attachments](http://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-attachments.html) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAttachments](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAttachments.html) \(AWS Direct Connect API\)

## Deleting a Direct Connect Gateway<a name="delete-direct-connect-gateway"></a>

If you no longer require a Direct Connect gateway, you can delete it\. You must first [disassociate](#associate-vgw-with-direct-connect-gateway) all associated virtual private gateways and [delete](deletevif.md) the attached private virtual interface\.

**To delete a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Direct Connect Gateways** and select the Direct Connect gateway\.

1. Choose **Actions**, **Delete Direct Connect Gateway**\.

1. Choose **Delete**\.

**To delete a Direct Connect gateway using the command line or API**
+ [delete\-direct\-connect\-gateway](http://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway.html) \(AWS CLI\)
+ [DeleteDirectConnectGateway](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGateway.html) \(AWS Direct Connect API\)