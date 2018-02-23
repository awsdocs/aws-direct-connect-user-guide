# Getting Started with AWS Direct Connect<a name="getting_started"></a>

AWS Direct Connect enables you to directly interface your on\-premises network with a device at an AWS Direct Connect location\. The following procedures demonstrate the common scenarios to get set up with an AWS Direct Connect connection\. You can also refer to the article [How do I provision an AWS Direct Connect connection?](https://aws.amazon.com/premiumsupport/knowledge-center/provision-direct-connection/) in the Knowledge Center\.

You can set up an AWS Direct Connect connection in one of the following ways\.


****  

| Port speed | Method | 
| --- | --- | 
|  1 Gbps or higher  |  Connect directly to an AWS device from your router at an AWS Direct Connect location\.  | 
|  1 Gbps or higher  |  Work with a partner in the [AWS Partner Network](http://aws.amazon.com/directconnect/partners) \(APN\) or a network provider that will help you connect a router from your data center, office, or colocation environment to an AWS Direct Connect location\. The network provider does not have to be a member of the APN to connect you\.   | 
|  Sub\-1 Gbps  |  Work with a partner in the [AWS Partner Network](http://aws.amazon.com/directconnect/partners) \(APN\) who will create a hosted connection for you\. Sign up for AWS, and then follow the instructions to [accept your hosted connection](#get-started-accept-hosted-connection)\.  | 


+ [Prerequisites](#get-started-prerequisites)
+ [Step 1: Sign Up for AWS](#get-started-signup)
+ [Step 2: Request an AWS Direct Connect Connection](#ConnectionRequest)
+ [Step 3: Download the LOA\-CFA](#DedicatedConnection)
+ [Step 4: Create a Virtual Interface](#createvirtualinterface)
+ [Step 5: Download the Router Configuration](#routerconfig)
+ [Step 6: Verify Your Virtual Interface](#connected)
+ [\(Optional\) Configure Redundant Connections](#RedundantConnections)

## Prerequisites<a name="get-started-prerequisites"></a>

For connections to AWS Direct Connect with port speeds of 1 Gbps or higher, ensure that your network meets the following requirements\.

+ Your network must use single mode fiber with a 1000BASE\-LX \(1310nm\) transceiver for 1 gigabit Ethernet, or a 10GBASE\-LR \(1310nm\) transceiver for 10 gigabit Ethernet\. 

+ Auto\-negotiation for the port must be disabled\. Port speed and full\-duplex mode must be configured manually\.

+ 802\.1Q VLAN encapsulation must be supported across the entire connection, including intermediate devices\.

+ Your device must support Border Gateway Protocol \(BGP\) and BGP MD5 authentication\. 

+ \(Optional\) You can configure Bidirectional Forwarding Detection \(BFD\) on your network\. Asynchronous BFD is automatically enabled for AWS Direct Connect virtual interfaces, but will not take effect until you configure it on your router\. 

## Step 1: Sign Up for AWS<a name="get-started-signup"></a>

To use AWS Direct Connect, you need an AWS account if you don't already have one\.

**To sign up for an AWS account**

1. Open [https://aws\.amazon\.com/](https://aws.amazon.com/), and then choose **Create an AWS Account**\.
**Note**  
This might be unavailable in your browser if you previously signed into the AWS Management Console\. In that case, choose **Sign in to a different account**, and then choose **Create a new AWS account**\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a PIN using the phone keypad\.

## Step 2: Request an AWS Direct Connect Connection<a name="ConnectionRequest"></a>

For connections of 1 Gbps or higher, you can submit a connection request using the AWS Direct Connect console\. Ensure that you have the following information:

+ The port speed that you require: 1 Gbps or 10 Gbps\. You cannot change the port speed after you've created the connection request\. 

+ The AWS Direct Connect location at which the connection will be terminated\.

If you require a port speed less than 1 Gbps, you cannot request a connection using the console\. Instead, contact an APN partner, who will create a hosted connection for you, which you then accept\. Skip the following procedure and go to [\(Sub\-1 Gbps Only\) Accept Your Hosted Connection](#get-started-accept-hosted-connection)\.

**To create a new AWS Direct Connect connection**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation bar, select the region in which to connect to AWS Direct Connect\. For more information, see [Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html)\.

1. On the **Welcome to AWS Direct Connect** screen, choose **Get Started with Direct Connect**\.

1. In the **Create a Connection** dialog box, do the following:  
![\[Create a Connection dialog box\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/create_connection.png)

   1. For **Connection Name**, enter a name for the connection\.

   1. For **LAG Association**, specify whether the connection is standalone, or if it should be associated with a link aggregation group \(LAG\) in your account\. This option is only available if you have a LAG in your account\. To associate the connection with a LAG, select the LAG ID\. The connection is created with the same port speed and location as specified in the LAG\. For more information, see [Link Aggregation Groups](lags.md)\.

   1. For **Location**, select the appropriate AWS Direct Connect location\.

   1. If applicable, for **Sub Location**, choose the floor closest to you or your network provider\. This option is only available if the location has meet\-me rooms \(MMRs\) in multiple floors of the building\.

   1. Select the appropriate port speed, and then choose **Create**\.

      Your connection is listed on the **Connections** pane of the AWS Direct Connect console\.

It can take up to 72 hours for AWS to review your request and provision a port for your connection\. During this time, you may receive an email with a request for more information about your use case or the specified location\. The email is sent to the email address that you used when you signed up for AWS\. You must respond within 7 days or the connection is deleted\.

For more information about creating and working with AWS Direct Connect connections, see [Connections](WorkingWithConnections.md)\.

### \(Sub\-1 Gbps Only\) Accept Your Hosted Connection<a name="get-started-accept-hosted-connection"></a>

If you requested a sub\-1G connection from your selected partner, they create a hosted connection for you \(you cannot create it yourself\)\. You must accept it in the AWS Direct Connect console before you can create a virtual interface\.

**To accept a hosted connection**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. If necessary, select the region in which the hosted connection resides\. For more information, see [Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html)\.

1. In the navigation pane, choose **Connections**\.

1. In the **Connections** pane, select the hosted connection\.  
![\[Connections pane\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/accept_hosted_connection.png)

1. Select **I understand that Direct Connect port charges apply once I click Accept Connection**, and then choose **Accept Connection**\.

1. Go to [Step 4](#RedundantConnections) to continue setting up your AWS Direct Connect connection\.

## Step 3: Download the LOA\-CFA<a name="DedicatedConnection"></a>

After you request a connection, AWS makes a Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\) available to you to download, or emails you with a request for more information\. The LOA\-CFA is the authorization to connect to AWS, and is required by the colocation provider or your network provider to establish the cross\-network connection \(cross\-connect\)\.

**To download the LOA\-CFA**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Connections** and select your connection\.

1. Choose **Actions**, **Download LOA\-CFA**\. 
**Note**  
If the link is not enabled, the LOA\-CFA is not yet available for you to download\. Check your email for a request for more information\. If it's still unavailable, or you haven't received an email after 72 hours, contact [AWS Support](https://aws.amazon.com/support/createCase)\.

1. Optionally enter the name of your provider to have it to appear with your company name as the requester in the LOA\-CFA\. Choose **Download**\. The LOA\-CFA is downloaded to your computer as a PDF file\.

1. After you've downloaded the LOA\-CFA, do one of the following:

   + If you're working with an APN member or network provider, send them the LOA\-CFA so that they can order a cross\-connect for you at the AWS Direct Connect location\. If they cannot order the cross\-connect for you, you can [contact the colocation provider](Colocation.md) directly\.

   + If you have equipment at the AWS Direct Connect location, contact the colocation provider to request a cross\-network connection\. You must be a customer of the colocation provider, and you must present them with the LOA\-CFA that authorizes the connection to the AWS router, as well as the necessary information to connect to your network\.

AWS Direct Connect locations that are listed as multiple sites \(for example, Equinix DC1\-DC6 & DC10\-DC11\) are set up as a campus\. If your or your network provider’s equipment is located in any of these sites, you will be able to request a cross connect to your assigned port even if it resides in a different building on the campus\. 

If you or your network partner experience issues establishing a physical connection, see [Troubleshooting Layer 1 \(Physical\) Issues](Troubleshooting.md#ts_layer_1)\.

## Step 4: Create a Virtual Interface<a name="createvirtualinterface"></a>

To begin using your AWS Direct Connect connection, you must create a virtual interface\. You can create a private virtual interface to connect to your VPC, or you can create a public virtual interface to connect to public AWS services that aren't in a VPC\. When you create a private virtual interface to a VPC, you need a private virtual interface for each VPC to which to connect\. For example, you need three private virtual interfaces to connect to three VPCs\.

Before you begin, ensure that you have the following information:

+ **Connection**: The AWS Direct Connect connection or link aggregation group \(LAG\) for which you are creating the virtual interface\.

+ **Virtual interface name**: A name for the virtual interface\.

+ **Virtual interface owner**: If you're creating the virtual interface for another account, you need the AWS account ID of the other account\.

+ \(Private virtual interface only\) **Connection to**: For connecting to a VPC in the same region, you need the virtual private gateway for your VPC\. The ASN for the Amazon side of the BGP session is inherited from the virtual private gateway\. When you create a virtual private gateway, you can specify your own private ASN\. Otherwise, Amazon provides a default ASN\. For more information, see [Create a Virtual Private Gateway](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/SetUpVPNConnections.html#vpn-create-vpg ) in the *Amazon VPC User Guide*\. For connecting to a VPC through a Direct Connect gateway, you need the Direct Connect gateway\. For more information, see [Direct Connect Gateways](http://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways.html)\.

+ **VLAN**: A unique virtual local area network \(VLAN\) tag that's not already in use on your connection\. The value must be between 1 and 4094 and must comply with the Ethernet 802\.1Q standard\. This tag is required for any traffic traversing the AWS Direct Connect connection\.

+ **Address family**: Whether the BGP peering session will be over IPv4 or IPv6\.

+ **Peer IP addresses**: A virtual interface can support a BGP peering session for IPv4, IPv6, or one of each \(dual\-stack\)\. You cannot create multiple BGP sessions for the same IP addressing family on the same virtual interface\. The IP address ranges are assigned to each end of the virtual interface for the BGP peering session\. 

  + IPv4: 

    + \(Public virtual interface only\) You must specify unique public IPv4 addresses \(/30\) that you own\.

    + \(Private virtual interface only\) Amazon can generate private IPv4 addresses for you\. If you specify your own, ensure that you specify private CIDRs for your router interface and the AWS Direct Connect interface only \(for example, do not specify other IP addresses from your local network\)\.

  + IPv6: Amazon automatically allocates you a /125 IPv6 CIDR\. You cannot specify your own peer IPv6 addresses\.

+ **BGP information**:

  + A public or private Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) for your side of the BGP session\. If you are using a public ASN, you must own it\. If you are using a private ASN, it must be in the 64512 to 65535 range\. Autonomous System \(AS\) prepending does not work if you use a private ASN for a public virtual interface\.

  + An MD5 BGP authentication key\. You can provide your own, or you can let Amazon generate one for you\.

+ \(Public virtual interface only\) **Prefixes you want to advertise**: Public IPv4 routes or IPv6 routes to advertise over BGP\. You must advertise at least one prefix using BGP, up to a maximum of 1,000 prefixes\.

  + IPv4: The IPv4 CIDR must not overlap with another public IPv4 CIDR announced via AWS Direct Connect\. If you do not have public IPv4 addresses, [contact AWS Support](https://aws.amazon.com/support/createCase)\. 

  + IPv6: Specify a prefix length of /64 or shorter\.

**To provision a public virtual interface to non\-VPC services**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Connections**, select the connection to use, and then choose **Actions**, **Create Virtual Interface**\.

1. In the **Create a Virtual Interface** pane, choose **Public**\.  
![\[Create a Virtual Interface screen\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/create_virtual_interface_public.png)

1. In the **Define Your New Public Virtual Interface** dialog box, do the following and choose **Continue**:

   1. For **Connection**, select an existing physical connection on which to create the virtual interface\.

   1. For **Virtual Interface Name**, enter a name for the virtual interface\.

   1. For **Virtual Interface Owner**, select the **My AWS Account** option if the virtual interface is for your AWS account\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\.

   1. If you're configuring an IPv4 BGP peer, choose **IPv4**, and do the following:

      + For **Your router peer IP**, enter the IPv4 CIDR destination address to which Amazon should send traffic\.

      + For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to Amazon\.

   1. If you're configuring an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

   1. To have AWS generate a BGP key, select the **Auto\-generate BGP key** check box\.

      To provide your own BGP key, clear the **Auto\-generate BGP key** check box\. For **BGP Authentication Key**, enter your BGP MD5 key\.

   1. For **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\.

1. Download your router configuration\. For more information, see [Step 5: Download the Router Configuration](#routerconfig)\.

**Note**  
AWS requests additional information from you if your public prefixes or ASNs belong to an ISP or network carrier\. This can be a document using an official company letterhead or an email from the company's domain name verifying that the network prefix/ASN may be used by you\.

When you create a public virtual interface, it can take up to 72 hours for AWS to review and approve your request\.

**To provision a private virtual interface to a VPC**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Connections**, select the connection to use, and choose **Actions**, **Create Virtual Interface**\.

1. In the **Create a Virtual Interface** pane, select **Private**\.  
![\[Create a Virtual Interface screen\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/create_virtual_interface_private.png)

1. Under **Define Your New Private Virtual Interface**, do the following and choose **Continue**:

   1. For **Virtual Interface Name**, enter a name for the virtual interface\.

   1. For **Virtual Interface Owner**, select the **My AWS Account** option if the virtual interface is for your AWS account\.

   1. For **Connection To**, choose **Virtual Private Gateway** and select the virtual private gateway to which to connect\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\.

   1. If you're configuring an IPv4 BGP peer, choose **IPv4**, and do the following:

      + To have AWS generate your router IP address and Amazon IP address, select **Auto\-generate peer IPs**\.

      + To specify these IP addresses yourself, clear the **Auto\-generate peer IPs** check box\. For **Your router peer IP**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to AWS\. 

   1. If you're configuring an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

   1. To have AWS generate a BGP key, select the **Auto\-generate BGP key** check box\.

      To provide your own BGP key, clear the **Auto\-generate BGP key** check box\. For **BGP Authentication Key**, enter your BGP MD5 key\.

1. Download your router configuration\. For more information, see [Step 5: Download the Router Configuration](#routerconfig)\.

**Note**  
If you use the VPC wizard to create a VPC, route propagation is automatically enabled for you\. With route propagation, routes are automatically populated to the route tables in your VPC\. If you choose, you can disable route propagation\. For more information, see [Enable Route Propagation in Your Route Table](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_VPN.html#vpn-configure-routing) in the *Amazon VPC User Guide*\. 

## Step 5: Download the Router Configuration<a name="routerconfig"></a>

After you have created a virtual interface for your AWS Direct Connect connection, you can download the router configuration file\. The file contains the necessary commands to configure your router for use with your private or public virtual interface\.

**To download a router configuration**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the **Virtual Interfaces** pane, select the virtual interface and then choose **Actions**, **Download Router Configuration**\.

1. In the **Download Router Configuration** dialog box, do the following:

   1. For **Vendor**, select the manufacturer of your router\.

   1. For **Platform**, select the model of your router\.

   1. For **Software**, select the software version for your router\.

1. Choose **Download**, and then use the appropriate configuration for your router to ensure that you can connect to AWS Direct Connect\.

For example configuration files, see [Example Router Configuration Files](http://docs.aws.amazon.com/directconnect/latest/UserGuide/create-vif.html#vif-example-router-files)\.

After you configure your router, the status of the virtual interface goes to `UP`\. If the virtual interface remains down and you cannot ping the AWS Direct Connect device's peer IP address, see [Troubleshooting Layer 2 \(Data Link\) Issues](Troubleshooting.md#ts-layer-2)\. If you can ping the peer IP address, see [Troubleshooting Layer 3/4 \(Network/Transport\) Issues](Troubleshooting.md#ts-layer-3)\. If the BGP peering session is established but you cannot route traffic, see [Troubleshooting Routing Issues](Troubleshooting.md#ts-routing)\.

## Step 6: Verify Your Virtual Interface<a name="connected"></a>

After you have established virtual interfaces to the AWS Cloud or to Amazon VPC, you can verify your AWS Direct Connect connection using the following procedures\. 

**To verify your virtual interface connection to the AWS Cloud**

+ Run `traceroute` and verify that the AWS Direct Connect identifier is in the network trace\.

**To verify your virtual interface connection to Amazon VPC**

1. Using a pingable AMI, such as an Amazon Linux AMI, launch an EC2 instance into the VPC that is attached to your virtual private gateway\. The Amazon Linux AMIs are available in the **Quick Start** tab when you use the instance launch wizard in the Amazon EC2 console\. For more information, see [Launch an Instance](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-instance_linux.html) in the *Amazon EC2 User Guide for Linux Instances\.* Ensure that the security group that's associated with the instance includes a rule permitting inbound ICMP traffic \(for the ping request\)\.

1. After the instance is running, get its private IPv4 address \(for example, 10\.0\.0\.4\)\. The Amazon EC2 console displays the address as part of the instance details\.

1. Ping the private IPv4 address and get a response\.

## \(Optional\) Configure Redundant Connections<a name="RedundantConnections"></a>

To provide for failover, we recommend that you request and configure two dedicated connections to AWS, as shown in the following figure\. These connections can terminate on one or two routers in your network\.

![\[Redundant connection diagram\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/redundant_connection.png)

There are different configuration choices available when you provision two dedicated connections:

+ Active/Active \(BGP multipath\)\. This is the default configuration, where both connections are active\. AWS Direct Connect supports multipathing to multiple virtual interfaces within the same location, and traffic is load\-shared between interfaces based on flow\. If one connection becomes unavailable, all traffic is routed through the other connection\.

+ Active/Passive \(failover\)\. One connection is handling traffic, and the other is on standby\. If the active connection becomes unavailable, all traffic is routed through the passive connection\. You need to prepend the AS path to the routes on one of your links for that to be the passive link\.

How you configure the connections doesn't affect redundancy, but it does affect the policies that determine how your data is routed over both connections\. We recommend that you configure both connections as active\.

If you use a VPN connection for redundancy, ensure that you implement a health check and failover mechanism, and check your [route table routing](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/SetUpVPNConnections.html#vpn-configure-routing)\.

For more information about high availability options, see [Multiple Data Center HA Network Connectivity](https://aws.amazon.com/answers/networking/aws-multiple-data-center-ha-network-connectivity/)\.