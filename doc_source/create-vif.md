# Create a virtual interface<a name="create-vif"></a>

You can create a transit virtual interface to connect to a transit gateway, a public virtual interface to connect to public resources \(non\-VPC services\), or a private virtual interface to connect to a VPC\.

To create a virtual interface for accounts within your AWS Organizations, or AWS Organizations that are different from yours, create a hosted virtual interface\. For more information, see [Create a hosted virtual interface](createhostedvirtualinterface.md)\.

**Prerequisites**  
Before you begin, ensure that you have read the information in [Prerequisites for virtual interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

## Create a public virtual interface<a name="create-public-vif"></a>

When you create a public virtual interface, it can take up to 72 hours for us to review and approve your request\.

**To provision a public virtual interface**

1. Open the **AWS Direct Connect** console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Public**\.

1. Under **Public virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol Autonomous System Number of your on\-premises peer router for the new virtual interface\.

      The valid values are 1\-2147483647\.

1. Under **Additional settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to AWS\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To provide your own BGP key, enter your BGP MD5 key\.

      If you do not enter a value, we generate a BGP key\. If you provided your own key, or if we generated the key for you, that value displays in the **BGP authentication key** column on the virtual interface details page of **Virtual interfaces**\.

   1. To advertise prefixes to Amazon, for **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\. 
**Important**  
You may add additional prefixes to an existing public VIF and advertise those by contacting [AWS support](https://aws.amazon.com/support/createCase)\. In your support case, provide a list of additional CIDR prefixes you want to add to the public VIF and advertise\.

   1. \(Optional\) Add or remove a tag\.

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create virtual interface**\.

1. Download the router configuration for your device\. For more information, see [Download the router configuration file](#vif-router-config)\.

**To create a public virtual interface using the command line or API**
+ [create\-public\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-public-virtual-interface.html) \(AWS CLI\)
+ [CreatePublicVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreatePublicVirtualInterface.html) \(AWS Direct Connect API\)

## Create a private virtual interface<a name="create-private-vif"></a>

You can provision a private virtual interface to a virtual private gateway in the same Region as your AWS Direct Connect connection\. For more information about provisioning a private virtual interface to an AWS Direct Connect gateway, see [Working with Direct Connect gateways](direct-connect-gateways.md)\.

If you use the VPC wizard to create a VPC, route propagation is automatically enabled for you\. With route propagation, routes are automatically populated to the route tables in your VPC\. If you choose, you can disable route propagation\. For more information, see [Enable Route Propagation in Your Route Table](https://docs.aws.amazon.com/vpc/latest/userguide/SetUpVPNConnections.html#vpn-configure-routing) in the *Amazon VPC User Guide*\.

The maximum transmission unit \(MTU\) of a network connection is the size, in bytes, of the largest permissible packet that can be passed over the connection\. The MTU of a virtual private interface can be either 1500 or 9001 \(jumbo frames\)\. The MTU of a transit virtual interface can be either 1500 or 8500 \(jumbo frames\)\. You can specify the MTU when you create the interface or update it after you create it\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) or 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find **Jumbo Frame Capable** on the **Summary** tab\.

**To provision a private virtual interface to a VPC**

1. Open the **AWS Direct Connect** console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Private**\.

1. Under **Private virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **Gateway type**, choose **Virtual private gateway**, or **Direct Connect gateway**\. 

   1. For **Virtual interface owner**, choose **Another AWS account**, and then enter the AWS account\.

   1. For **Virtual private gateway**, choose the virtual private gateway to use for this interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol Autonomous System Number of your on\-premises peer router for the new virtual interface\.

      The valid values are 1 to 2147483647\.

1. Under **Additional Settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.
**Important**  
If you let AWS auto\-assign IPv4 addresses, a /29 CIDR will be allocated from 169\.254\.0\.0/16 IPv4 Link\-Local according to RFC 3927 for point\-to\-point connectivity\. AWS does not recommend this option if you intend to use the customer router peer IP address as the source and/or destination for VPC traffic\. Instead you should use RFC 1918 or other addressing, and specify the address yourself\.  
For more information about RFC 1918, see [Address Allocation for Private Internets](https://datatracker.ietf.org/doc/html/rfc1918)\.
For more information about RFC 3927, see [Dynamic Configuration of IPv4 Link\-Local Addresses](https://datatracker.ietf.org/doc/html/rfc3927)\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To change the maximum transmission unit \(MTU\) from 1500 \(default\) to 9001 \(jumbo frames\), select **Jumbo MTU \(MTU size 9001\)**\.

   1. \(Optional\) Under **Enable SiteLink**, choose **Enabled** to enable direct connectivity between Direct Connect points of presence\.

   1. \(Optional\) Add or remove a tag\.

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create virtual interface**\.

1. Download the router configuration for your device\. For more information, see [Download the router configuration file](#vif-router-config)\.

**To create a private virtual interface using the command line or API**
+ [create\-private\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-private-virtual-interface.html) \(AWS CLI\)
+ [CreatePrivateVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreatePrivateVirtualInterface.html) \(AWS Direct Connect API\)

## Create a transit virtual interface to the Direct Connect gateway<a name="create-transit-vif"></a>

To connect your AWS Direct Connect connection to the transit gateway, you must create a transit interface for your connection\. Specify the Direct Connect gateway to which to connect\.

The maximum transmission unit \(MTU\) of a network connection is the size, in bytes, of the largest permissible packet that can be passed over the connection\. The MTU of a virtual private interface can be either 1500 or 9001 \(jumbo frames\)\. The MTU of a transit virtual interface can be either 1500 or 8500 \(jumbo frames\)\. You can specify the MTU when you create the interface or update it after you create it\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) or 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find **Jumbo Frame Capable** on the **Summary** tab\.

**Important**  
If you associate your transit gateway with one or more Direct Connect gateways, the Autonomous System Number \(ASN\) used by the transit gateway and the Direct Connect gateway must be different\. For example, if you use the default ASN 64512 for both the transit gateway and the Direct Connect gateway, the association request fails\.

**To provision a transit virtual interface to a Direct Connect gateway**

1. Open the **AWS Direct Connect** console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

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

      The valid values are 1 to 2147483647\.

1. Under **Additional Settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.
**Important**  
If you let AWS auto\-assign IPv4 addresses, a /29 CIDR will be allocated from 169\.254\.0\.0/16 IPv4 Link\-Local according to RFC 3927 for point\-to\-point connectivity\. AWS does not recommend this option if you intend to use the customer router peer IP address as the source and/or destination for VPC traffic\. Instead you should use RFC 1918 or other addressing, and specify the address yourself\.  
For more information about RFC 1918, see [Address Allocation for Private Internets](https://datatracker.ietf.org/doc/html/rfc1918)\.
For more information about RFC 3927, see [Dynamic Configuration of IPv4 Link\-Local Addresses](https://datatracker.ietf.org/doc/html/rfc3927)\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To change the maximum transmission unit \(MTU\) from 1500 \(default\) to 8500 \(jumbo frames\), select **Jumbo MTU \(MTU size 8500\)**\.

   1. \(Optional\) Under **Enable SiteLink**, choose **Enabled** to enable direct connectivity between Direct Connect points of presence\.

   1. \(Optional\) Add or remove a tag\.

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create virtual interface**\.

After you create the virtual interface, you can download the router configuration for your device\. For more information, see [Download the router configuration file](#vif-router-config)\.

**To create a transit virtual interface using the command line or API**
+ [create\-transit\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-transit-virtual-interface.html) \(AWS CLI\)
+ [CreateTransitVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateTransitVirtualInterface.html) \(AWS Direct Connect API\)

**To view the virtual interfaces that are attached to a Direct Connect gateway using the command line or API**
+ [describe\-direct\-connect\-gateway\-attachments](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-attachments.html) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAttachments](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAttachments.html) \(AWS Direct Connect API\)

## Download the router configuration file<a name="vif-router-config"></a>

After you create the virtual interface and the interface state is up, you can download the router configuration file for your router\.

If you use any of the following routers for virtual interfaces that have MACsec turned on, we automatically create the configuration file for your router:
+ Cisco Nexus 9K\+ Series switches running NX\-OS 9\.3 or later software
+ Juniper Networks M/MX Series Routers running JunOS 9\.5 or later software

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and then choose **View details**\.

1. Choose **Download router configuration**\.

1. For **Download router configuration**, do the following:

   1. For **Vendor**, select the manufacturer of your router\.

   1. For **Platform**, select the model of your router\.

   1. For **Software**, select the software version for your router\.

1. Choose **Download**, and then use the appropriate configuration for your router to ensure that you can connect to AWS Direct Connect\.

### MACsec considerations<a name="masec-consideration"></a>

If you need to manually configure your router for MACsec, use the following table as a guideline\.


| Parameter | Description | 
| --- | --- | 
| CKN length | This is a 64 hexadecimal character \(0–9, A–E\) string\. Use the full length to maximize cross\-platform compatibility\. | 
| CAK length | This is a 64 hexadecimal character \(0–9, A–E\) string\. Use the full length to maximize cross\-platform compatibility\. | 
| Cryptographic algorithm | AES\_256\_CMAC | 
| SAK Cipher Suite |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/create-vif.html)  | 
| Key Cipher Suite | 16 | 
| Confidentiality Offset | 0 | 
| ICV Indicator | No | 
| SAK Rekey Time | PN Rollover> | 