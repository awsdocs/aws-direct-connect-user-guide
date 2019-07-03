# Virtual Private Gateway Associations<a name="virtualgateways"></a>

You can use an *AWS Direct Connect gateway* to connect your AWS Direct Connect connection over a private virtual interface to one or more VPCs in your account that are located in the same or different Regions\. You associate a Direct Connect gateway with the virtual private gateway for the VPC\. Then, you create a private virtual interface for your AWS Direct Connect connection to the Direct Connect gateway\. You can attach multiple private virtual interfaces to your Direct Connect gateway\.

In the following diagram, the Direct Connect gateway enables you to use your AWS Direct Connect connection in the US East \(N\. Virginia\) Region to access VPCs in your account in both the US East \(N\. Virginia\) and US West \(N\. California\) Regions\.

![\[Direct connect gateway\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/dx-gateway.png)

The following rules apply:
+ You cannot use a Direct Connect gateway to connect to a VPC in the China Regions\.
+ There are limits for creating and using Direct Connect gateways\. For more information, see [AWS Direct Connect Limits](limits.md)\.
+ The VPCs to which you connect through a Direct Connect gateway cannot have overlapping CIDR blocks\. If you add an IPv4 CIDR block to a VPC that's associated with a Direct Connect gateway, ensure that the CIDR block does not overlap with an existing CIDR block for any other associated VPC\. For more information, see [Adding IPv4 CIDR Blocks to a VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#vpc-resize) in the *Amazon VPC User Guide*\.
+ The transit virtual interface can be in any location, but currently the transit gateway must reside in the United States\.
+ You cannot create a public virtual interface to a Direct Connect gateway\.
+ A Direct Connect gateway supports communication between attached private virtual interfaces and associated virtual private gateways only\. The following traffic flows are not supported:
  + Direct communication between the VPCs that are associated with the Direct Connect gateway\.
  + Direct communication between the virtual interfaces that are attached to the Direct Connect gateway\.
  + Direct communication between a virtual interface attached to a Direct Connect gateway and a VPN connection on a virtual private gateway that's associated with the same Direct Connect gateway\.
+ You cannot associate a virtual private gateway with more than one Direct Connect gateway and you cannot attach a private virtual interface to more than one Direct Connect gateway\.
+ A virtual private gateway that you associate with a Direct Connect gateway must be attached to a VPC\.

To connect your AWS Direct Connect connection to a VPC in the same Region only, you can create a Direct Connect gateway\. Or, you can create a private virtual interface and attach it to the virtual private gateway for the VPC\. For more information, see [Creating a Private Virtual Interface](create-vif.md#create-private-vif) and [VPN CloudHub](https://docs.aws.amazon.com/vpc/latest/userguide/VPN_CloudHub.html)\.

To use your AWS Direct Connect connection with a VPC in another account, you can create a hosted private virtual interface for that account\. When the owner of the other account accepts the hosted virtual interface, they can choose to attach it either to a virtual private gateway or to a Direct Connect gateway in their account\. For more information, see [AWS Direct Connect Virtual Interfaces](WorkingWithVirtualInterfaces.md)\.

**Topics**
+ [Associating and Disassociating Virtual Private Gateways](#associate-vgw-with-direct-connect-gateway)
+ [Creating a Private Virtual Interface to the Direct Connect Gateway](#create-private-vif-for-gateway)
+ [Associating a Virtual Private Gateway Across Accounts](multi-account-associate-vgw.md)

## Associating and Disassociating Virtual Private Gateways<a name="associate-vgw-with-direct-connect-gateway"></a>

The virtual private gateway must be attached to the VPC to which you want to connect\. For more information, see [Create a Virtual Private Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_VPN.html#vpn-create-vpg) in the *Amazon VPC User Guide*\.

**Note**  
If you are planning to use the virtual private gateway for a Direct Connect gateway and a dynamic VPN connection, set the ASN on the virtual private gateway to the value that you require for the VPN connection\. Otherwise, the ASN on the virtual private gateway can be set to any permitted value\. The Direct Connect gateway advertises all connected VPCs over the ASN assigned to it\.

**To associate a virtual private gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect Gateways** and then select the Direct Connect gateway\.

1. Choose **View details**\.

1. Choose **Gateways associations** and then choose **Associate gateway**\.

1. For **Gateways**, choose the virtual private gateways to associate, and then choose **Associate gateway**\.

You can view all of the virtual private gateways that are associated with the Direct Connect gateway by choosing **Gateway associations**\. 

**To disassociate a virtual private gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect Gateways** and then select the Direct Connect gateway\.

1. Choose **View details**\.

1. Choose **Gateway associations** and then select the virtual private gateway\.

1. Choose **Disassociate**\.

**To associate a virtual private gateway using the command line or API**
+ [create\-direct\-connect\-gateway\-association](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-direct-connect-gateway-association.html) \(AWS CLI\)
+ [CreateDirectConnectGatewayAssociation](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)

**To view the virtual private gateways associated with a Direct Connect gateway using the command line or API**
+ [describe\-direct\-connect\-gateway\-associations](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-associations.html) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAssociations](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAssociations.html) \(AWS Direct Connect API\)

**To disassociate a virtual private gateway using the command line or API**
+ [delete\-direct\-connect\-gateway\-association](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway-association.html) \(AWS CLI\)
+ [DeleteDirectConnectGatewayAssociation](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)

## Creating a Private Virtual Interface to the Direct Connect Gateway<a name="create-private-vif-for-gateway"></a>

To connect your AWS Direct Connect connection to the remote VPC, you must create a private virtual interface for your connection\. Specify the Direct Connect gateway to which to connect\.

**Note**  
If you're accepting a hosted private virtual interface, you can associate it with a Direct Connect gateway in your account\. For more information, see [Accepting a Hosted Virtual Interface](accepthostedvirtualinterface.md)\.

**To provision a private virtual interface to a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Private**\.

1. Under **Virtual interface type**, choose **Private**\.

1. Under **Private virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **Virtual interface owner**, choose **My AWS account** if the virtual interface is for your AWS account\. 

   1. For **Gateway type**, choose **Direct Connect gateway**\.

   1.  For **Direct Connect gateway**, select the Direct Connect gateway\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

1. Under **Additional Settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To advertise prefixes to Amazon, for **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\. 

   1. To change the maximum transmission unit \(MTU\) from 1500 \(default\) to 9001 \(jumbo frames\), select **Jumbo MTU \(MTU size 9001\)**\.

   1. \(Optional\) Ador remove a tag\.

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create virtual interface**\.

After you've created the virtual interface, you can download the router configuration for your device\. For more information, see [Downloading the Router Configuration File](create-vif.md#vif-router-config)\.

**To create a private virtual interface using the command line or API**
+ [create\-private\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-private-virtual-interface.html) \(AWS CLI\)
+ [CreatePrivateVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreatePrivateVirtualInterface.html) \(AWS Direct Connect API\)

**To view the virtual interfaces that are attached to a Direct Connect gateway using the command line or API**
+ [describe\-direct\-connect\-gateway\-attachments](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-attachments.html) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAttachments](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAttachments.html) \(AWS Direct Connect API\)