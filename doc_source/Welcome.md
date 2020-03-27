# What is AWS Direct Connect?<a name="Welcome"></a>

AWS Direct Connect links your internal network to an AWS Direct Connect location over a standard Ethernet fiber\-optic cable\. One end of the cable is connected to your router, the other to an AWS Direct Connect router\. With this connection, you can create *virtual interfaces* directly to public AWS services \(for example, to Amazon S3\) or to Amazon VPC, bypassing internet service providers in your network path\. An AWS Direct Connect location provides access to AWS in the Region with which it is associated\. You can use a single connection in a public Region or AWS GovCloud \(US\) to access public AWS services in all other public Regions\.

The following diagram shows how AWS Direct Connect interfaces with your network\. 

![\[AWS Direct Connect\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/direct_connect_overview.png)

**Topics**
+ [AWS Direct Connect Components](#overview-components)
+ [Network Requirements](#overview_requirements)
+ [Pricing for AWS Direct Connect](#Paying)
+ [Accessing a Remote AWS Region](remote_regions.md)
+ [Routing Policies and BGP Communities](routing-and-bgp.md)

## AWS Direct Connect Components<a name="overview-components"></a>

The following are the key components that you use for AWS Direct Connect:

**Connections**  
Create a *connection* in an AWS Direct Connect location to establish a network connection from your premises to an AWS Region\. For more information, see [AWS Direct Connect Connections](WorkingWithConnections.md)\. 

**Virtual interfaces**  
Create a *virtual interface* to enable access to AWS services\. A public virtual interface enables access to public services, such as Amazon S3\. A private virtual interface enables access to your VPC\. For more information, see [AWS Direct Connect Virtual Interfaces](WorkingWithVirtualInterfaces.md) and [Prerequisites for Virtual Interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

## Network Requirements<a name="overview_requirements"></a>

To use AWS Direct Connect in an AWS Direct Connect location, your network must meet one of the following conditions:
+ Your network is colocated with an existing AWS Direct Connect location\. For more information about available AWS Direct Connect locations, see [AWS Direct Connect Product Details](http://aws.amazon.com/directconnect/details)\. 
+ You are working with an AWS Direct Connect partner who is a member of the AWS Partner Network \(APN\)\. For information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com//directconnect/partners/)\.
+ You are working with an independent service provider to connect to AWS Direct Connect\.

In addition, your network must meet the following conditions:
+ Your network must use single\-mode fiber with a 1000BASE\-LX \(1310 nm\) transceiver for 1 gigabit Ethernet or a 10GBASE\-LR \(1310 nm\) transceiver for 10 gigabit Ethernet\.
+ Auto\-negotiation for the port must be disabled\. Port speed and full\-duplex mode must be configured manually\.
+ 802\.1Q VLAN encapsulation must be supported across the entire connection, including intermediate devices\.
+ Your device must support Border Gateway Protocol \(BGP\) and BGP MD5 authentication\.
+ \(Optional\) You can configure Bidirectional Forwarding Detection \(BFD\) on your network\. Asynchronous BFD is automatically enabled for AWS Direct Connect virtual interfaces, but does not take effect until you configure it on your router\.

AWS Direct Connect supports both the IPv4 and IPv6 communication protocols\. IPv6 addresses provided by public AWS services are accessible through AWS Direct Connect public virtual interfaces\.

AWS Direct Connect supports an Ethernet frame size of 1522 or 9023 bytes \(14 bytes Ethernet header \+ 4 bytes VLAN tag \+ 20 bytes for the IP datagram \+ 4 bytes FCS\) at the link layer\. You can set the MTU of your private virtual interfaces\. For more information, see [Setting Network MTU for Private Virtual Interfaces or Transit Virtual Interfaces](set-jumbo-frames-vif.md)\.

## Pricing for AWS Direct Connect<a name="Paying"></a>

AWS Direct Connect has two billing elements: port hours and outbound data transfer\. Port hour pricing is determined by capacity and connection type \(dedicated connection or hosted connection\)\. 

Data Transfer Out charges for private interfaces and transit virtual interfaces are allocated to the AWS account responsible for the Data Transfer\. There are no additional charges to use multi\-account Direct Connect gateway\. 

For publicly addressable AWS resources \(for example, Amazon S3 buckets, Classic EC2 instances, or EC2 traffic that goes through an internet gateway\), if the outbound traffic is destined for public prefixes owned by the same AWS payer account and actively advertised to AWS through an AWS Direct Connect public virtual Interface, the Data Transfer Out \(DTO\) usage is metered toward the resource owner at AWS Direct Connect data transfer rate\.



For more information, see [Amazon Direct Connect Pricing](https://aws.amazon.com/directconnect/pricing/)\.
