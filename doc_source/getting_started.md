# Classic<a name="getting_started"></a>

Select Classic when you have existing connections\.

The following procedures demonstrate the common scenarios to get set up with an AWS Direct Connect connection\.

**Topics**
+ [Prerequisites](#get-started-prerequisites)
+ [Step 1: Sign up for AWS](#get-started-signup)
+ [Step 2: Request an AWS Direct Connect dedicated connection or accept a hosted connection](#ConnectionRequest)
+ [\(Dedicated connection\) Step 3: Download the LOA\-CFA](#DedicatedConnection)
+ [Step 4: Create a virtual interface](#createvirtualinterface)
+ [Step 5: Download the router configuration](#routerconfig)
+ [Step 6: Verify your virtual interface](#connected)
+ [\(Recommended\) Step 7: Configure redundant connections](#RedundantConnections)

## Prerequisites<a name="get-started-prerequisites"></a>

For connections to AWS Direct Connect with port speeds of 1 Gbps or higher, ensure that your network meets the following requirements:
+ Your network must use single\-mode fiber with a 1000BASE\-LX \(1310 nm\) transceiver for 1 gigabit Ethernet, a 10GBASE\-LR \(1310 nm\) transceiver for 10 gigabit, or a 100GBASE\-LR4 for 100 gigabit Ethernet\.
+ Auto\-negotiation for a port must be disabled for a connection with a port speed of more than 1 Gbps\. However, depending on the AWS Direct Connect endpoint serving your connection, auto\-negotiation might need to be enabled or disabled for 1 Gbps connections\. If your virtual interface remains down, see [Troubleshooting layer 2 \(data link\) issues](Troubleshooting.md#ts-layer-2)\.
+ 802\.1Q VLAN encapsulation must be supported across the entire connection, including intermediate devices\.
+ Your device must support Border Gateway Protocol \(BGP\) and BGP MD5 authentication\.
+ \(Optional\) You can configure Bidirectional Forwarding Detection \(BFD\) on your network\. BFD is a feature of BGP that applies to both public and private transit virtual interfaces\. Asynchronous BFD is automatically enabled for AWS Direct Connect virtual interfaces, but does not take effect until you configure it on your router\. For more information, see [Enable BFD for a Direct Connect connection](https://aws.amazon.com/premiumsupport/knowledge-center/enable-bfd-direct-connect/)\. 

## Step 1: Sign up for AWS<a name="get-started-signup"></a>

To use AWS Direct Connect, you need an account if you don't already have one\.

**To sign up for an account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

## Step 2: Request an AWS Direct Connect dedicated connection or accept a hosted connection<a name="ConnectionRequest"></a>

For dedicated connections, you can submit a connection request using the AWS Direct Connect console\. For hosted connections, work with an AWS Direct Connect Partner to request a hosted connection\. Ensure that you have the following information:
+ The port speed that you require\. You cannot change the port speed after you create the connection request\. 
+ The AWS Direct Connect location at which the connection is to be terminated\.

You cannot use the AWS Direct Connect console to request a hosted connection\. Instead, contact an AWS Direct Connect Partner, who can create a hosted connection for you, which you then accept\. Skip the following procedure and go to [ Accept your hosted connection](#get-started-accept-hosted-connection)\.

**To create a new AWS Direct Connect connection**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. On the **AWS Direct Connect** screen, under **Get started**, choose **Create a connection**\.

1. Choose **Classic**\.

1. On the **Create Connection** pane, under **Connection settings,** do the following:

   1. For **Name**, enter a name for the connection\.

   1. For **Location**, select the appropriate AWS Direct Connect location\.

   1. If applicable, for **Sub Location**, choose the floor closest to you or your network provider\. This option is only available if the location has meet\-me rooms \(MMRs\) in multiple floors of the building\.

   1. For **Port Speed**, choose the connection bandwidth\.

   1. For **On\-premises**, select **Connect through an AWS Direct Connect partner** when you use this connection to connect to your data center\.

   1. For **Service provider**, select the AWS Direct Connect Partner\. If you use a partner that is not in the list, select **Other**\.

   1. If you selected **Other** for **Service provider**, for** Name of other provider**, enter the name of the partner that you use\.

   1. \(Optional\) Add or remove a tag\.

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create Connection**\.

It can take up to 72 hours for AWS to review your request and provision a port for your connection\. During this time, you might receive an email with a request for more information about your use case or the specified location\. The email is sent to the email address that you used when you signed up for AWS\. You must respond within 7 days or the connection is deleted\.

For more information, see [AWS Direct Connect connections](WorkingWithConnections.md)\.

### Accept your hosted connection<a name="get-started-accept-hosted-connection"></a>

 You must accept the hosted connection in the AWS Direct Connect console before you can create a virtual interface\.

**To accept a hosted virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and then choose **View details**\.

1. Choose **Accept**\.

1. This applies to private virtual interfaces and transit virtual interfaces\.

   \(Transit virtual interface\) In the **Accept virtual interface** dialog box, select a Direct Connect gateway, and then choose **Accept virtual interface**\.

   \(Private virtual interface\) In the **Accept virtual interface** dialog box, select a virtual private gateway or Direct Connect gateway, and then choose **Accept virtual interface**\.

1. After you accept the hosted virtual interface, the owner of the AWS Direct Connect connection can download the router configuration file\. The **Download router configuration** option is not available for the account that accepts the hosted virtual interface\.

1. Go to [Step 4](#createvirtualinterface) to continue setting up your AWS Direct Connect connection\.

## \(Dedicated connection\) Step 3: Download the LOA\-CFA<a name="DedicatedConnection"></a>

After you request a connection, we make a Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\) available to you to download, or emails you with a request for more information\. The LOA\-CFA is the authorization to connect to AWS, and is required by the colocation provider or your network provider to establish the cross\-network connection \(cross\-connect\)\.

**To download the LOA\-CFA**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Connections**\.

1. Select the connection and choose **View Details**\.

1. Choose **Download LOA\-CFA**\.

   The LOA\-CFA is downloaded to your computer as a PDF file\.
**Note**  
If the link is not enabled, the LOA\-CFA is not yet available for you to download\. Check your email for a request for more information\. If it's still unavailable, or you haven't received an email after 72 hours, contact [AWS Support](https://aws.amazon.com/support/createCase)\.

1. After you download the LOA\-CFA, do one of the following:
   + If you're working with an AWS Direct Connect Partner or network provider, send them the LOA\-CFA so that they can order a cross\-connect for you at the AWS Direct Connect location\. If they cannot order the cross\-connect for you, you can [contact the colocation provider](Colocation.md) directly\.
   + If you have equipment at the AWS Direct Connect location, contact the colocation provider to request a cross\-network connection\. You must be a customer of the colocation provider\. You must also present them with the LOA\-CFA that authorizes the connection to the AWS router, and the necessary information to connect to your network\.

AWS Direct Connect locations that are listed as multiple sites \(for example, Equinix DC1\-DC6 & DC10\-DC11\) are set up as a campus\. If your or your network provider’s equipment is located in any of these sites, you can request a cross\-connect to your assigned port even if it resides in a different campus building\. 

**Important**  
A campus is treated as a single AWS Direct Connect location\. To achieve high availability, configure connections to different AWS Direct Connect locations\.

If you or your network provider experience issues establishing a physical connection, see [Troubleshooting layer 1 \(physical\) issues](Troubleshooting.md#ts_layer_1)\.

## Step 4: Create a virtual interface<a name="createvirtualinterface"></a>

To begin using your AWS Direct Connect connection, you must create a virtual interface\. You can create a private virtual interface to connect to your VPC\. Or, you can create a public virtual interface to connect to public AWS services that aren't in a VPC\. When you create a private virtual interface to a VPC, you need a private virtual interface for each VPC to which to connect\. For example, you need three private virtual interfaces to connect to three VPCs\.

Before you begin, ensure that you have the following information:


| Resource | Required information | 
| --- | --- | 
| Connection | The AWS Direct Connect connection or link aggregation group \(LAG\) for which you are creating the virtual interface\. | 
| Virtual interface name | A name for the virtual interface\. | 
| Virtual interface owner | If you're creating the virtual interface for another account, you need the AWS account ID of the other account\. | 
| \(Private virtual interface only\) Connection | For connecting to a VPC in the same AWS Region, you need the virtual private gateway for your VPC\. The ASN for the Amazon side of the BGP session is inherited from the virtual private gateway\. When you create a virtual private gateway, you can specify your own private ASN\. Otherwise, Amazon provides a default ASN\. For more information, see [Create a Virtual Private Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/SetUpVPNConnections.html#vpn-create-vpg) in the Amazon VPC User Guide\. For connecting to a VPC through a Direct Connect gateway, you need the Direct Connect gateway\. For more information, see [Direct Connect Gateways](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways.html)\. | 
| VLAN | A unique virtual local area network \(VLAN\) tag that's not already in use on your connection\. The value must be between 1 and 4094 and must comply with the Ethernet 802\.1Q standard\. This tag is required for any traffic traversing the AWS Direct Connect connection\. If you have a hosted connection, your AWS Direct Connect Partner provides this value\. You can’t modify the value after you have created the virtual interface\. | 
| Peer IP addresses |  A virtual interface can support a BGP peering session for IPv4, IPv6, or one of each \(dual\-stack\)\. Do not use Elastic IPs \(EIPs\) from the Amazon Pool to create a public virtual interface\. You cannot create multiple BGP sessions for the same IP addressing family on the same virtual interface\. The IP address ranges are assigned to each end of the virtual interface for the BGP peering session\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/getting_started.html)  | 
| Address family | Whether the BGP peering session will be over IPv4 or IPv6\. | 
| BGP information | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/getting_started.html) | 
| \(Public virtual interface only\) Prefixes you want to advertise |   Public IPv4 routes or IPv6 routes to advertise over BGP\. You must advertise at least one prefix using BGP, up to a maximum of 1,000 prefixes\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/getting_started.html) | 
| \(Private virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames apply only to propagated routes from AWS Direct Connect\. If you add static routes to a route table that point to your virtual private gateway, then traffic routed through the static routes is sent using 1500 MTU\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo frame capable on the virtual interface General configuration page\. | 
| \(Transit virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames are supported up to 8500 MTU for Direct Connect\. Static routes and propagated routes configured in the Transit Gateway Route Table will support Jumbo Frames, including from EC2 instances with VPC static route table entries to the Transit Gateway Attachment\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo frame capable on the virtual interface General configuration page\. | 

We request additional information from you if your public prefixes or ASNs belong to an ISP or network carrier\. This can be a document using an official company letterhead or an email from the company's domain name verifying that the network prefix/ASN may be used by you\.

For private virtual interface and public virtual interfaces, the maximum transmission unit \(MTU\) of a network connection is the size, in bytes, of the largest permissible packet that can be passed over the connection\. The MTU of a virtual private interface can be either 1500 or 9001 \(jumbo frames\)\. The MTU of a transit virtual interface can be either 1500 or 8500 \(jumbo frames\)\. You can specify the MTU when you create the interface or update it after you create it\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) or 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find **Jumbo Frame Capable** on the **Summary** tab\.

When you create a public virtual interface, it can take up to 72 hours for AWS to review and approve your request\.

**To provision a public virtual interface to non\-VPC services**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Public**\.

1. Under **Public virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the The Border Gateway Protocol Autonomous System Number of your on\-premises peer router for the new virtual interface\.

      The valid values are 1\-2147483647\.

1. Under **Additional settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to AWS\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To provide your own BGP key, enter your BGP MD5 key\.

      If you do not enter a value, we generate a BGP key\.

   1. To advertise prefixes to Amazon, for **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\. 

   1. \(Optional\) Add or remove a tag\.

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create virtual interface**\.

**To provision a private virtual interface to a VPC**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

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
If you let AWS auto\-assign IPv4 addresses, a /30 CIDR will be allocated from 169\.254\.0\.0/16 IPv4 Link\-Local according to RFC 3927 for point\-to\-point connectivity\. AWS does not recommend this option if you intend to use the customer router peer IP address as the source and/or destination for VPC traffic\. Instead you should use RFC 1918 or other addressing, and specify the address yourself\.  
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

1. You need to use your BGP device to advertise the network that you use for the public VIF connection\. 

## Step 5: Download the router configuration<a name="routerconfig"></a>

After you have created a virtual interface for your AWS Direct Connect connection, you can download the router configuration file\. The file contains the necessary commands to configure your router for use with your private or public virtual interface\.

**To download a router configuration**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the connection and choose **View Details**\.

1. Choose **Download router configuration**\.

1. For **Download router configuration**, do the following:

   1. For **Vendor**, select the manufacturer of your router\.

   1. For **Platform**, select the model of your router\.

   1. For **Software**, select the software version for your router\.

1. Choose **Download**, and then use the appropriate configuration for your router to ensure that you can connect to AWS Direct Connect\.

For example configuration files, see [Example Router Configuration Files](https://docs.aws.amazon.com/directconnect/latest/UserGuide/create-vif.html#vif-example-router-files)\.

After you configure your router, the status of the virtual interface goes to `UP`\. If the virtual interface remains down and you cannot ping the AWS Direct Connect device's peer IP address, see [Troubleshooting layer 2 \(data link\) issues](Troubleshooting.md#ts-layer-2)\. If you can ping the peer IP address, see [Troubleshooting layer 3/4 \(Network/Transport\) issues](Troubleshooting.md#ts-layer-3)\. If the BGP peering session is established but you cannot route traffic, see [Troubleshooting routing issues](Troubleshooting.md#ts-routing)\.

## Step 6: Verify your virtual interface<a name="connected"></a>

After you have established virtual interfaces to the AWS Cloud or to Amazon VPC, you can verify your AWS Direct Connect connection using the following procedures\. 

**To verify your virtual interface connection to the AWS Cloud**
+ Run `traceroute` and verify that the AWS Direct Connect identifier is in the network trace\.

**To verify your virtual interface connection to Amazon VPC**

1. Using a pingable AMI, such as an Amazon Linux AMI, launch an EC2 instance into the VPC that is attached to your virtual private gateway\. The Amazon Linux AMIs are available in the **Quick Start** tab when you use the instance launch wizard in the Amazon EC2 console\. For more information, see [Launch an Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-instance_linux.html) in the *Amazon EC2 User Guide for Linux Instances\.* Ensure that the security group that's associated with the instance includes a rule permitting inbound ICMP traffic \(for the ping request\)\.

1. After the instance is running, get its private IPv4 address \(for example, 10\.0\.0\.4\)\. The Amazon EC2 console displays the address as part of the instance details\.

1. Ping the private IPv4 address and get a response\.

## \(Recommended\) Step 7: Configure redundant connections<a name="RedundantConnections"></a>

To provide for failover, we recommend that you request and configure two dedicated connections to AWS, as shown in the following figure\. These connections can terminate on one or two routers in your network\.

![\[Redundant connection diagram\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/redundant_connection.png)

There are different configuration choices available when you provision two dedicated connections:
+ Active/Active \(BGP multipath\)\. This is the default configuration, where both connections are active\. AWS Direct Connect supports multipathing to multiple virtual interfaces within the same location, and traffic is load\-shared between interfaces based on flow\. If one connection becomes unavailable, all traffic is routed through the other connection\.
+ Active/Passive \(failover\)\. One connection is handling traffic, and the other is on standby\. If the active connection becomes unavailable, all traffic is routed through the passive connection\. You need to prepend the AS path to the routes on one of your links for that to be the passive link\.

How you configure the connections doesn't affect redundancy, but it does affect the policies that determine how your data is routed over both connections\. We recommend that you configure both connections as active\.

If you use a VPN connection for redundancy, ensure that you implement a health check and failover mechanism\. If you use either of the following configurations, then you need to check your [route table routing](https://docs.aws.amazon.com/vpc/latest/userguide/SetUpVPNConnections.html#vpn-configure-routing) to route to the new network interface\. 
+ You use your own instances for routing, for example the instance is the firewall\. 
+ You use your own instance that terminates a VPN connection\.

To achieve high availability, we strongly recommend that you configure connections to different AWS Direct Connect locations\. 

For more information about AWS Direct Connect resiliency, see [AWS Direct Connect Resiliency Recommendations](https://aws.amazon.com/directconnect/resiliency-recommendation/)\.