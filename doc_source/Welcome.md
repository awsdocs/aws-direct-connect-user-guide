# What is AWS Direct Connect?<a name="Welcome"></a>

AWS Direct Connect links your internal network to an AWS Direct Connect location over a standard Ethernet fiber\-optic cable\. One end of the cable is connected to your router, the other to an AWS Direct Connect router\. With this connection in place, you can create *virtual interfaces* directly to public AWS services \(for example, to Amazon S3\) or to Amazon VPC, bypassing Internet service providers in your network path\. An AWS Direct Connect location provides access to AWS in the region with which it is associated, and you can use a single connection in a public region or AWS GovCloud \(US\) to access public AWS services in all other public regions\.

The following diagram shows how AWS Direct Connect interfaces with your network\. 

![\[AWS Direct Connect\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/direct_connect_overview.png)

**Topics**
+ [AWS Direct Connect Components](#overview-components)
+ [Network Requirements](#overview_requirements)
+ [AWS Direct Connect Limits](#directconnect_limits)
+ [Accessing a Remote AWS Region](remote_regions.md)
+ [Routing Policies and BGP Communities](routing-and-bgp.md)

## AWS Direct Connect Components<a name="overview-components"></a>

The following are the key components that you'll use for AWS Direct Connect:

**Connections**  
Create a *connection* in an AWS Direct Connect location to establish a network connection from your premises to an AWS Region\. For more information, see [AWS Direct Connect Connections](WorkingWithConnections.md)\. 

**Virtual interfaces**  
Create a *virtual interface* to enable access to AWS services\. A public virtual interface enables access to public\-facing services, such as Amazon S3\. A private virtual interface enables access to your VPC\. For more information, see [AWS Direct Connect Virtual Interfaces](WorkingWithVirtualInterfaces.md) and [Prerequisites for Virtual Interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

## Network Requirements<a name="overview_requirements"></a>

To use AWS Direct Connect in an AWS Direct Connect location, your network must meet one of the following conditions:
+ Your network is colocated with an existing AWS Direct Connect location\. For more information about available AWS Direct Connect locations, see [AWS Direct Connect Product Details](http://aws.amazon.com/directconnect/details)\. 
+ You are working with an AWS Direct Connect partner who is a member of the AWS Partner Network \(APN\)\. For information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com//directconnect/partners/)\.
+ You are working with an independent service provider to connect to AWS Direct Connect\.

In addition, your network must meet the following conditions:
+ Your network must use single\-mode fiber with a 1000BASE\-LX \(1310nm\) transceiver for 1 gigabit Ethernet or a 10GBASE\-LR \(1310nm\) transceiver for 10 gigabit Ethernet\.
+ Auto\-negotiation for the port must be disabled\. Port speed and full\-duplex mode must be configured manually\.
+ 802\.1Q VLAN encapsulation must be supported across the entire connection, including intermediate devices\.
+ Your device must support Border Gateway Protocol \(BGP\) and BGP MD5 authentication\.
+ \(Optional\) You can configure Bidirectional Forwarding Detection \(BFD\) on your network\. Asynchronous BFD is automatically enabled for AWS Direct Connect virtual interfaces, but will not take effect until you configure it on your router\. 

AWS Direct Connect supports both the IPv4 and IPv6 communication protocols\. IPv6 addresses provided by public AWS services are accessible through AWS Direct Connect public virtual interfaces\.

AWS Direct Connect supports a maximum transmission unit \(MTU\) of up to 1522 bytes at the physical connection layer \(14 bytes Ethernet header \+ 4 bytes VLAN tag \+ 1500 bytes IP datagram \+ 4 bytes FCS\)\.

## AWS Direct Connect Limits<a name="directconnect_limits"></a>

The following table lists the limits related to AWS Direct Connect\. Unless indicated otherwise, you can request an increase for any of these limits using the [AWS Direct Connect Limits form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-direct-connect)\.


| Component | Limit | Comments | 
| --- | --- | --- | 
|  Virtual interfaces per AWS Direct Connect connection  |  50  |  This limit cannot be increased  | 
|  Active AWS Direct Connect connections per region per account  |  10  |  | 
|  Routes per Border Gateway Protocol \(BGP\) session on a private virtual interface  |  100  |  This limit cannot be increased  | 
|  Routes per Border Gateway Protocol \(BGP\) session on a public virtual interface  |  1,000  |  This limit cannot be increased  | 
|  Connections per link aggregation group \(LAG\)  | 4 |  | 
|  Link aggregation groups \(LAGs\) per region  |  10  |  | 
|  Direct Connect gateways per account  |  200  |  | 
|  Virtual private gateways per Direct Connect gateway  |  10  |  This limit cannot be increased  | 
|  Virtual interfaces per Direct Connect gateway  |  30  |  | 

AWS Direct Connect supports these port speeds over single\-mode fiber: 1 Gbps: 1000BASE\-LX \(1310nm\) and 10 Gbps: 10GBASE\-LR \(1310nm\)\.