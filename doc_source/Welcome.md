# What is AWS Direct Connect?<a name="Welcome"></a>

AWS Direct Connect links your internal network to an AWS Direct Connect location over a standard Ethernet fiber\-optic cable\. One end of the cable is connected to your router, the other to an AWS Direct Connect router\. With this connection, you can create *virtual interfaces* directly to public AWS services \(for example, to Amazon S3\) or to Amazon VPC, bypassing internet service providers in your network path\. An AWS Direct Connect location provides access to AWS in the Region with which it is associated\. You can use a single connection in a public Region or AWS GovCloud \(US\) to access public AWS services in all other public Regions\.

The following diagram shows how AWS Direct Connect interfaces with your network\. 

![\[AWS Direct Connect\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/direct-connect-overview.png)

**Topics**
+ [AWS Direct Connect components](#overview-components)
+ [Network requirements](#overview_requirements)
+ [Pricing for AWS Direct Connect](#Paying)
+ [Accessing a remote AWS Region](remote_regions.md)
+ [Routing policies and BGP communities](routing-and-bgp.md)

## AWS Direct Connect components<a name="overview-components"></a>

The following are the key components that you use for AWS Direct Connect:

**Connections**  
Create a *connection* in an AWS Direct Connect location to establish a network connection from your premises to an AWS Region\. For more information, see [AWS Direct Connect connections](WorkingWithConnections.md)\. 

**Virtual interfaces**  
Create a *virtual interface* to enable access to AWS services\. A public virtual interface enables access to public services, such as Amazon S3\. A private virtual interface enables access to your VPC\. For more information, see [AWS Direct Connect virtual interfaces](WorkingWithVirtualInterfaces.md) and [Prerequisites for virtual interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

## Network requirements<a name="overview_requirements"></a>

To use AWS Direct Connect in an AWS Direct Connect location, your network must meet one of the following conditions:
+ Your network is colocated with an existing AWS Direct Connect location\. For more information about available AWS Direct Connect locations, see [AWS Direct Connect Product Details](http://aws.amazon.com/directconnect/details)\. 
+ You are working with an AWS Direct Connect partner who is a member of the AWS Partner Network \(APN\)\. For information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com//directconnect/partners/)\.
+ You are working with an independent service provider to connect to AWS Direct Connect\.

In addition, your network must meet the following conditions:
+ Your network must use single\-mode fiber with a 1000BASE\-LX \(1310 nm\) transceiver for 1 gigabit Ethernet, a 10GBASE\-LR \(1310 nm\) transceiver for 10 gigabit, or a 100GBASE\-LR4 for 100 gigabit Ethernet\.
+ Auto\-negotiation for a port must be disabled for a connection with a port speed of more than 1 Gbps\. However, depending on the AWS Direct Connect endpoint serving your connection, auto\-negotiation might need to be enabled or disabled for 1 Gbps connections\. If your virtual interface remains down, see [Troubleshooting layer 2 \(data link\) issues](Troubleshooting.md#ts-layer-2)\.
+ 802\.1Q VLAN encapsulation must be supported across the entire connection, including intermediate devices\.
+ Your device must support Border Gateway Protocol \(BGP\) and BGP MD5 authentication\.
+ \(Optional\) You can configure Bidirectional Forwarding Detection \(BFD\) on your network\. BFD is a feature of BGP that applies to both public and private transit virtual interfaces\. Asynchronous BFD is automatically enabled for AWS Direct Connect virtual interfaces, but does not take effect until you configure it on your router\. For more information, see [Enable BFD for a Direct Connect connection](https://aws.amazon.com/premiumsupport/knowledge-center/enable-bfd-direct-connect/)\. 

AWS Direct Connect supports both the IPv4 and IPv6 communication protocols\. IPv6 addresses provided by public AWS services are accessible through AWS Direct Connect public virtual interfaces\.

AWS Direct Connect supports an Ethernet frame size of 1522 or 9023 bytes \(14 bytes Ethernet header \+ 4 bytes VLAN tag \+ bytes for the IP datagram \+ 4 bytes FCS\) at the link layer\. You can set the MTU of your private virtual interfaces\. For more information, see [Set network MTU for private virtual interfaces or transit virtual interfaces](set-jumbo-frames-vif.md)\.

## Pricing for AWS Direct Connect<a name="Paying"></a>

AWS Direct Connect has two billing elements: port hours and outbound data transfer\. Port hour pricing is determined by capacity and connection type \(dedicated connection or hosted connection\)\. 

Data Transfer Out charges for private interfaces and transit virtual interfaces are allocated to the AWS account responsible for the Data Transfer\. There are no additional charges to use a multi\-account AWS Direct Connect gateway\.

For publicly addressable AWS resources \(for example, Amazon S3 buckets, Classic EC2 instances, or EC2 traffic that goes through an internet gateway\), if the outbound traffic is destined for public prefixes owned by the same AWS payer account and actively advertised to AWS through an AWS Direct Connect public virtual Interface, the Data Transfer Out \(DTO\) usage is metered toward the resource owner at AWS Direct Connect data transfer rate\.

For more information, see [AWS Direct Connect Pricing](https://aws.amazon.com/directconnect/pricing/)\.