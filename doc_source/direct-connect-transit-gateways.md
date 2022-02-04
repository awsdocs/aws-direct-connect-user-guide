# Transit gateway associations<a name="direct-connect-transit-gateways"></a>

You can use an *AWS Direct Connect gateway* to connect your AWS Direct Connect connection over a transit virtual interface to the VPCs or VPNs that are attached to your transit gateway\. You associate a Direct Connect gateway with the transit gateway\. Then, create a transit virtual interface for your AWS Direct Connect connection to the Direct Connect gateway\. 

The following rules apply to transit gateway associations:
+ You cannot attach a Direct Connect gateway to a transit gateway when the Direct Connect gateway is already associated with a virtual private gateway or is attached to a private virtual interface\.
+ There are limits for creating and using Direct Connect gateways\. For more information, see [AWS Direct Connect quotas](limits.md)\.
+ A Direct Connect gateway supports communication between attached transit virtual interfaces and associated transit gateways only\. 
+ If you connect to multiple transit gateways that are in different Regions, use unique ASNs for each transit gateway\.
+ A transit gateway can only be used with a 1 Gbps or faster Direct Connect connection\.

## Associating and disassociating transit gateways<a name="associate-tgw-with-direct-connect-gateway"></a>

**To associate a transit gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect Gateways** and then select the Direct Connect gateway\.

1. Choose **View details**\.

1. Choose **Gateway associations** and then choose **Associate gateway**\.

1. For **Gateways**, choose the transit gateway to associate\.

1. In **Allowed prefixes**, enter the prefixes \(separated by a comma, or on a new line\) which the Direct Connect gateway advertises to the on\-premises data center\.

1. Choose **Associate gateway**

You can view all of the gateways that are associated with the Direct Connect gateway by choosing **Gateway associations**\. 

**To disassociate a transit gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect gateways** and then select the Direct Connect gateway\.

1. Choose **View details**\.

1. Choose **Gateway associations** and then select the transit gateway\.

1. Choose **Disassociate**\.

**To associate a transit gateway using the command line or API**
+ [create\-direct\-connect\-gateway\-association](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-direct-connect-gateway-association.html) \(AWS CLI\)
+ [CreateDirectConnectGatewayAssociation](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)

**To view the transit gateways associated with a Direct Connect gateway using the command line or API**
+ [describe\-direct\-connect\-gateway\-associations](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-associations.html) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAssociations](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAssociations.html) \(AWS Direct Connect API\)

**To disassociate a transit gateway using the command line or API**
+ [delete\-direct\-connect\-gateway\-association](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway-association.html) \(AWS CLI\)
+ [DeleteDirectConnectGatewayAssociation](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)

## Creating a transit virtual interface to the Direct Connect gateway<a name="create-transit-vif-for-gateway"></a>

To connect your AWS Direct Connect connection to the transit gateway, you must create a transit interface for your connection\. Specify the Direct Connect gateway to which to connect\.

**Important**  
If you associate your transit gateway with one or more Direct Connect gateways, the Autonomous System Number \(ASN\) used by the transit gateway and the Direct Connect gateway must be different\. For example, if you use the default ASN 64512 for both the transit gateway and the Direct Connect gateway, the association request fails\.

**To provision a transit virtual interface to a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Transit**\.

1. Under **Transit virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **Virtual interface owner**, choose **My AWS account** if the virtual interface is for your AWS account\.

   1.  For **Direct Connect gateway**, select the Direct Connect gateway\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol Autonomous System Number of your on\-premises peer router for the new virtual interface\.

      The valid values are 1\-2147483647\.

1. Under **Additional Settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To change the maximum transmission unit \(MTU\) from 1500 \(default\) to 8500 \(jumbo frames\), select **Jumbo MTU \(MTU size 8500\)**\.

   1. \(Optional\) Add or remove a tag\.

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create virtual interface**\.

After you've created the virtual interface, you can download the router configuration for your device\. For more information, see [Download the router configuration file](create-vif.md#vif-router-config)\.

**To create a transit virtual interface using the command line or API**
+ [create\-transit\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-transit-virtual-interface.html) \(AWS CLI\)
+ [CreateTransitVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateTransitVirtualInterface.html) \(AWS Direct Connect API\)

**To view the virtual interfaces that are attached to a Direct Connect gateway using the command line or API**
+ [describe\-direct\-connect\-gateway\-attachments](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-attachments.html) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAttachments](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAttachments.html) \(AWS Direct Connect API\)