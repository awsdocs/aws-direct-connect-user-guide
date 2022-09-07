# Development and test<a name="dev-test-resiliency"></a>

You can achieve development and test resiliency for non\-critical workloads by using separate connections that terminate on separate devices in one location \(as shown in the following figure\)\. This model provides resiliency against device failure, but does not provide resiliency against location failure\.

![\[Development and Test Model\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/dc-devtest.png)

The following procedures demonstrate how to use the AWS Direct Connect Resiliency Toolkit to configure a development and test resiliency model\.

**Topics**
+ [Step 1: Sign up for AWS](#dev-test-signup)
+ [Step 2: Configure the resiliency model](#dev-test-select-model)
+ [Step 3: Create a virtual interface](#dev-test-createvirtualinterface)
+ [Step 4: Verify your virtual interface resiliency configuration](#dev-test-resiliency-failover)
+ [Step 5: Verify your virtual interface](#dev-test-connected)

## Step 1: Sign up for AWS<a name="dev-test-signup"></a>

### <a name="dev-test-signup"></a>

To use AWS Direct Connect, you need an AWS account if you don't already have one\.

**To sign up for an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

## Step 2: Configure the resiliency model<a name="dev-test-select-model"></a>

**To configure the resiliency model**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. On the **AWS Direct Connect** screen, under **Get started**, choose **Create a connection**\.

1. Under **Connection ordering type**, choose **Connection wizard**\.

1. Under **Resiliency level**, choose **Development and test**, and then choose **Next**\.

1. On the **Configure connections** pane, under **Connection settings,** do the following:

   1. For **bandwidth**, choose the connection bandwidth\.

      This bandwidth applies to all of the created connections\.

   1. For **First location service provider**, select the appropriate AWS Direct Connect location\.

   1. If applicable, for **First Sub location**, choose the floor closest to you or your network provider\. This option is only available if the location has meet\-me rooms \(MMRs\) on multiple floors of the building\.

   1. If you selected **Other** for **First location service provider**, for **Name of other provider**, enter the name of the partner that you use\.

   1. \(Optional\) Add or remove a tag\.

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Next**\.

1. Review your connections, and then choose **Continue**\.

   If your LOAs are ready, you can choose **Download LOA**, and then click **Continue**\.

   It can take up to 72 hours for AWS to review your request and provision a port for your connection\. During this time, you might receive an email with a request for more information about your use case or the specified location\. The email is sent to the email address that you used when you signed up for AWS\. You must respond within 7 days or the connection is deleted\. 

## Step 3: Create a virtual interface<a name="dev-test-createvirtualinterface"></a>

To begin using your AWS Direct Connect connection, you must create a virtual interface\. You can create a private virtual interface to connect to your VPC\. Or, you can create a public virtual interface to connect to public AWS services that aren't in a VPC\. When you create a private virtual interface to a VPC, you need a private virtual interface for each VPC that you're connecting to\. For example, you need three private virtual interfaces to connect to three VPCs\.

Before you begin, ensure that you have the following information:


| Resource | Required information | 
| --- | --- | 
| Connection | The AWS Direct Connect connection or link aggregation group \(LAG\) for which you are creating the virtual interface\. | 
| Virtual interface name | A name for the virtual interface\. | 
| Virtual interface owner | If you're creating the virtual interface for another account, you need the AWS account ID of the other account\. | 
| \(Private virtual interface only\) Connection | For connecting to a VPC in the same AWS Region, you need the virtual private gateway for your VPC\. The ASN for the Amazon side of the BGP session is inherited from the virtual private gateway\. When you create a virtual private gateway, you can specify your own private ASN\. Otherwise, Amazon provides a default ASN\. For more information, see [Create a Virtual Private Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/SetUpVPNConnections.html#vpn-create-vpg) in the Amazon VPC User Guide\. For connecting to a VPC through a Direct Connect gateway, you need the Direct Connect gateway\. For more information, see [Direct Connect Gateways](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways.html)\. | 
| VLAN | A unique virtual local area network \(VLAN\) tag that's not already in use on your connection\. The value must be between 1 and 4094 and must comply with the Ethernet 802\.1Q standard\. This tag is required for any traffic traversing the AWS Direct Connect connection\. If you have a hosted connection, your AWS Direct Connect Partner provides this value\. You can’t modify the value after you have created the virtual interface\. | 
| Peer IP addresses |  A virtual interface can support a BGP peering session for IPv4, IPv6, or one of each \(dual\-stack\)\. Do not use Elastic IPs \(EIPs\) from the Amazon Pool to create a public virtual interface\. You cannot create multiple BGP sessions for the same IP addressing family on the same virtual interface\. The IP address ranges are assigned to each end of the virtual interface for the BGP peering session\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/dev-test-resiliency.html)  | 
| Address family | Whether the BGP peering session will be over IPv4 or IPv6\. | 
| BGP information | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/dev-test-resiliency.html) | 
| \(Public virtual interface only\) Prefixes you want to advertise |   Public IPv4 routes or IPv6 routes to advertise over BGP\. You must advertise at least one prefix using BGP, up to a maximum of 1,000 prefixes\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/dev-test-resiliency.html) | 
| \(Private virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames apply only to propagated routes from AWS Direct Connect\. If you add static routes to a route table that point to your virtual private gateway, then traffic routed through the static routes is sent using 1500 MTU\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo frame capable on the virtual interface General configuration page\. | 
| \(Transit virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames are supported up to 8500 MTU for Direct Connect\. Static routes and propagated routes configured in the Transit Gateway Route Table will support Jumbo Frames, including from EC2 instances with VPC static route table entries to the Transit Gateway Attachment\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo frame capable on the virtual interface General configuration page\. | 

If your public prefixes or ASNs belong to an ISP or network carrier, we request additional information from you\. This can be a document using an official company letterhead, or an email from the company's domain name verifying that the network prefix/ASN can be used by you\.

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

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

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

## Step 4: Verify your virtual interface resiliency configuration<a name="dev-test-resiliency-failover"></a>

After you have established virtual interfaces to the AWS Cloud or to Amazon VPC, perform a virtual interface failover test to verify that your configuration meets your resiliency requirements\. For more information, see [AWS Direct Connect Failover Test](resiliency_failover.md)\. 

## Step 5: Verify your virtual interface<a name="dev-test-connected"></a>

After you have established virtual interfaces to the AWS Cloud or to Amazon VPC, you can verify your AWS Direct Connect connection using the following procedures\. 

**To verify your virtual interface connection to the AWS Cloud**
+ Run `traceroute` and verify that the AWS Direct Connect identifier is in the network trace\.

**To verify your virtual interface connection to Amazon VPC**

1. Using a pingable AMI, such as an Amazon Linux AMI, launch an EC2 instance into the VPC that is attached to your virtual private gateway\. The Amazon Linux AMIs are available in the **Quick Start** tab when you use the instance launch wizard in the Amazon EC2 console\. For more information, see [Launch an Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-instance_linux.html) in the *Amazon EC2 User Guide for Linux Instances\.* Ensure that the security group that's associated with the instance includes a rule permitting inbound ICMP traffic \(for the ping request\)\.

1. After the instance is running, get its private IPv4 address \(for example, 10\.0\.0\.4\)\. The Amazon EC2 console displays the address as part of the instance details\.

1. Ping the private IPv4 address and get a response\.