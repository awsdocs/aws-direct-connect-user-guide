# Getting Started with AWS Direct Connect<a name="getting_started"></a>

You can set up an AWS Direct Connect connection in one of the following ways:

+ At an AWS Direct Connect location\. 

+ Through a member of the AWS Partner Network \(APN\) or a network carrier\.

+ Through a hosted connection provided by a member of the APN\.

A partner in the APN can help you establish network circuits between an AWS Direct Connect location and your data center, office, or colocation environment, or provide colocation space within the same facility as the AWS Direct Connect location\. For more information, see [http://aws\.amazon\.com/directconnect/partners](http://aws.amazon.com/directconnect/partners)\. If you don't have equipment hosted in the same facility as AWS Direct Connect, you can use a network provider to connect to AWS Direct Connect\. The provider does not have to be a member of the APN to connect you\. 

Before you begin, verify that your equipment meets the specifications set out in [Network Requirements](Welcome.md#overview_requirements)\.


+ [Step 1: Sign Up for AWS](#get-started-signup)
+ [Step 2: Submit AWS Direct Connect Connection Request](#ConnectionRequest)
+ [Step 3: Download the LOA\-CFA](#DedicatedConnection)
+ [Step 4: \(Optional\) Configure Redundant Connections](#RedundantConnections)
+ [Step 5: Create a Virtual Interface](#createvirtualinterface)
+ [Step 6: Download Router Configuration](#routerconfig)
+ [Step 7: Verify Your Virtual Interface](#connected)

## Step 1: Sign Up for AWS<a name="get-started-signup"></a>

To use AWS Direct Connect, you need an AWS account if you don't already have one\.

**To sign up for an AWS account**

1. Open [https://aws\.amazon\.com/](https://aws.amazon.com/), and then choose **Create an AWS Account**\.
**Note**  
This might be unavailable in your browser if you previously signed into the AWS Management Console\. In that case, choose **Sign in to a different account**, and then choose **Create a new AWS account**\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a PIN using the phone keypad\.

## Step 2: Submit AWS Direct Connect Connection Request<a name="ConnectionRequest"></a>

You can submit a connection request using the AWS Direct Connect console\. Before you begin, ensure that you have the following information:

+ The port speed that you require: 1 Gbps or 10 Gbps\. You cannot change the port speed after you've created the connection request\. 

+ The AWS Direct Connect location to which to connect\.

If you require a port speed less than 1 Gbps, you cannot request a connection using the console\. Instead, contact an APN partner, who will create a hosted connection for you\. The hosted connection appears in your AWS Direct Connect console, and must be accepted before use\. Skip the following procedure and go to [Accept Your Hosted Connection](#get-started-accept-hosted-connection)\.

**To create a new AWS Direct Connect connection**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation bar, select the region in which to connect to AWS Direct Connect\. For more information, see [Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html)\.

1. On the **Welcome to AWS Direct Connect** screen, choose **Get Started with Direct Connect**\.

1. In the **Create a Connection** dialog box, do the following:  
![\[Create a Connection dialog box\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/create_connection.png)

   1. For **Connection Name**, enter a name for the connection\.

   1. For **LAG Association**, specify whether the connection is standalone, or if it should be associated with a link aggregation group \(LAG\) in your account\. If you associate the connection with a LAG, select the LAG ID\. The connection is created with the same port speed and location as specified in the LAG\. For more information, see [Link Aggregation Groups](lags.md)\.

   1. For **Location**, select the appropriate AWS Direct Connect location\.
**Note**  
If you don’t have equipment at an AWS Direct Connect location, choose **contact one of our partners**\.

   1. Select the appropriate port speed, and then choose **Create**\.

      Your connection is listed on the **Connections** pane of the AWS Direct Connect console\.

For more information about creating and working with AWS Direct Connect connections, see [Connections](WorkingWithConnections.md)\.

### Accept Your Hosted Connection<a name="get-started-accept-hosted-connection"></a>

If you requested a sub\-1G connection from your selected partner, they create a hosted connection for you\. You must accept it in the AWS Direct Connect console before you can create a virtual interface\.

**To accept a hosted connection**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. If necessary, select the region in which the hosted connection resides\. For more information, see [Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html)\.

1. In the navigation pane, choose **Connections**\.

1. In the **Connections** pane, select the hosted connection\.  
![\[Connections pane\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/accept_hosted_connection.png)

1. Select **I understand that Direct Connect port charges apply once I click "Accept This Connection"**, and then choose **Accept Connection**\.

1. Go to Step 4 to continue setting up your AWS Direct Connect connection\.

## Step 3: Download the LOA\-CFA<a name="DedicatedConnection"></a>

AWS makes a Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\) available to you to download, or emails you with a request for more information after you've created the connection request\. If you receive a request for more information, you must respond within 7 days or the connection is deleted\. The LOA\-CFA is the authorization to connect to AWS, and is required by the colocation provider or your network provider to establish the cross\-network connection \(cross\-connect\)\.

**To download the LOA\-CFA**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Connections**\.

1. Choose **Actions**, **Download LOA\-CFA**\. 
**Note**  
If the link is not enabled, the LOA\-CFA is not yet available for you to download\. Check your email for a request for more information\. If it's still unavailable, or you haven't received an email after 72 hours, contact [AWS Support](https://aws.amazon.com/support/createCase)\.

1. In the dialog box, optionally enter the name of your provider to have it to appear with your company name as the requester in the LOA\-CFA\. Choose **Download**\. The LOA\-CFA is downloaded to your computer as a PDF file\.

After you've downloaded the LOA\-CFA, do one of the following:

+ If you're working with a network provider, send the LOA\-CFA to your network provider so that they can order a cross connect for you\. You cannot order a cross connect for yourself in the AWS Direct Connect location if you do not have equipment there\. Your network provider does this for you\.

+ If you have equipment at the AWS Direct Connect location, contact the colocation provider to request a cross\-network connection\. For more information , see [Requesting Cross Connects at AWS Direct Connect Locations](Colocation.md)\. You must be a customer of the colocation provider, and you must present them with the LOA\-CFA that authorizes the connection to the AWS router, as well as the necessary information to connect to your network\.

The LOA\-CFA expires after 90 days\. To refresh the LOA\-CFA with a new issue date, you can download it again from the AWS Direct Connect console\. If you do not take any action, we delete the connection\.

**Note**  
Port\-hour billing starts 90 days after you created the connection, or after the connection between your router and the AWS router is established, whichever comes first\. For more information, see [AWS Direct Connect Pricing](https://aws.amazon.com/directconnect/pricing/)\. 

## Step 4: \(Optional\) Configure Redundant Connections<a name="RedundantConnections"></a>

To provide for failover, we recommend that you request and configure two dedicated connections to AWS, as shown in the following figure\. These connections can terminate on one or two routers in your network\.

![\[Redundant connection diagram\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/redundant_connection.png)

There are different configuration choices available when you provision two dedicated connections:

+ Active/Active \(BGP multipath\)\. This is the default configuration, where both connections are active\. AWS Direct Connect supports multipathing to multiple virtual interfaces within the same location, and traffic is load\-shared between interfaces based on flow\. If one connection becomes unavailable, all traffic is routed through the other connection\.

+ Active/Passive \(failover\)\. One connection is handling traffic, and the other is on standby\. If the active connection becomes unavailable, all traffic is routed through the passive connection\. You need to prepend the AS path to the routes on one of your links for that to be the passive link\.

How you configure the connections doesn't affect redundancy, but it does affect the policies that determine how your data is routed over both connections\. We recommend that you configure both connections as active\.

If you use a VPN connection for redundancy, ensure that you implement a health check and failover mechanism, and check your [route table routing](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/SetUpVPNConnections.html#vpn-configure-routing)\.

## Step 5: Create a Virtual Interface<a name="createvirtualinterface"></a>

After you have placed an order for an AWS Direct Connect connection, you must create a virtual interface to begin using it\. You can create a private virtual interface to connect to your VPC, or you can create a public virtual interface to connect to AWS services that aren't in a VPC\.

Before you begin, ensure that you have the following information:

+ A unique virtual local area network \(VLAN\) tag that's not in use on the AWS Direct Connect connection for another virtual interface\. The number must be between 1 and 4094\.

+ A public or private Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\)\. If you are using a public ASN, you must own it\. If you are using a private ASN, it must be in the 64512 to 65535 range\.

+ \(Public virtual interface\): For an IPv4 BGP peering session, unique public IPv4 addresses \(/30\) that you own for each side of the BGP peering connection, and a unique IPv4 CIDR range to announce via AWS Direct Connect\.

+ \(Private virtual interface\): The virtual private gateway to connect to\. For more information, see [Adding a Hardware Virtual Private Gateway to Your VPC](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_VPN.html) in the *Amazon VPC User Guide*\.

For more information, see [Prerequisites for Virtual Interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

**Note**  
A sub\-1G connection only supports one virtual interface\.

**To provision a public virtual interface to non\-VPC services**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the **Connections** pane, select the connection to use, and then choose **Actions**, **Create Virtual Interface**\.

1. In the **Create a Virtual Interface** pane, choose **Public**\.  
![\[Create a Virtual Interface screen\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/create_virtual_interface_public.png)

1. In the **Define Your New Public Virtual Interface** dialog box, do the following:

   1. For **Connection**, select an existing physical connection on which to create the virtual interface\.

   1. For **Virtual Interface Name**, enter a name for the virtual interface\.

   1. For **Virtual Interface Owner**, select the **My AWS Account** option if the virtual interface is for your AWS account ID\.

   1. For **VLAN**, enter the VLAN number\.

   1. If you're configuring an IPv4 BGP peer, choose **IPv4** and do the following:

      + For **Your router peer IP**, enter the IPv4 CIDR destination address to which Amazon should send traffic\.

      + For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to Amazon\.

   1. If you're configuring an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

   1. Select the **Auto\-generate BGP key** check box to have Amazon generate a BGP key\.

      To provide your own BGP key, clear the **Auto\-generate BGP key** check box\. For **BGP Authentication Key**, enter your BGP MD5 key\.

   1. For **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\.

1. Choose **Continue**, and then download your router configuration\. For more information, see [Step 6: Download Router Configuration](#routerconfig)\.

When you create a private virtual interface to a VPC, you need a private virtual interface for each VPC to which to connect\. For example, you need three private virtual interfaces to connect to three VPCs\.

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

1. Download your router configuration\. For more information, see [Step 6: Download Router Configuration](#routerconfig)\.

**Note**  
If you use the VPC wizard to create a VPC, route propagation is automatically enabled for you\. With route propagation, routes are automatically populated to the route tables in your VPC\. If you choose, you can disable route propagation\. For more information, see [Enable Route Propagation in Your Route Table](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_VPN.html#vpn-configure-routing) in the *Amazon VPC User Guide*\. 

## Step 6: Download Router Configuration<a name="routerconfig"></a>

After you have created a virtual interface for your AWS Direct Connect connection, you can download the router configuration file\.

**To download router configuration**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the **Virtual Interfaces** pane, select the virtual interface you created and then choose **Actions**, **Download Router Configuration**\.

1. In the **Download Router Configuration** dialog box, do the following:

   1. For **Vendor**, select the manufacturer of your router\.

   1. For **Platform**, select the model of your router\.

   1. For **Software**, select the software version for your router\.

1. Choose **Download**, and then use the appropriate configuration for your router to ensure that you can connect to AWS Direct Connect\.

   For example configuration files, see [Example Router Configuration Files](create-vif.md#vif-example-router-files)\.

## Step 7: Verify Your Virtual Interface<a name="connected"></a>

After you have established virtual interfaces to the AWS Cloud or to Amazon VPC, you can verify your AWS Direct Connect connection using the following procedures\. 

**To verify your virtual interface connection to the AWS Cloud**

+ Run `traceroute` and verify that the AWS Direct Connect identifier is in the network trace\.

**To verify your virtual interface connection to Amazon VPC**

1. Using a pingable AMI, such as an Amazon Linux AMI, launch an EC2 instance into the VPC that is attached to your virtual private gateway\. The Amazon Linux AMIs are available in the **Quick Start** tab when you use the instance launch wizard in the Amazon EC2 console\. For more information, see [Launch an Instance](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-instance_linux.html) in the *Amazon EC2 User Guide for Linux Instances\.* Ensure that the security group that's associated with the instance includes a rule permitting inbound ICMP traffic \(for the ping request\)\.

1. After the instance is running, get its private IPv4 address \(for example, 10\.0\.0\.4\)\. The Amazon EC2 console displays the address as part of the instance details\.

1. Ping the private IPv4 address and get a response\.