# AWS Direct Connect virtual interfaces<a name="WorkingWithVirtualInterfaces"></a>

You must create one of the following virtual interfaces to begin using your AWS Direct Connect connection\. 
+ Private virtual interface: Access an Amazon VPC using private IP addresses\.
+ Public virtual interface: Access AWS services from your on\-premises data center\. Allow AWS services, or AWS customers access to your public networks over the interface instead of traversing the internet\.
+ Transit virtual interface: Access one or more Amazon VPC Transit Gateways associated with Direct Connect gateways\. You can use transit virtual interfaces with 1/2/5/10/100 Gbps AWS Direct Connect connections\. For information about Direct Connect gateway configurations, see [Direct Connect gateways](direct-connect-gateways-intro.md)\.

To connect to other AWS services using IPv6 addresses, check the service documentation to verify that IPv6 addressing is supported\.

## Public virtual interface prefix advertisement rules<a name="advertise-prefixes"></a>

We advertise appropriate Amazon prefixes to you so that you can reach either your VPCs or other AWS services\. You can access all AWS prefixes through this connection; for example, Amazon EC2, Amazon S3, and Amazon\.com\. You do not have access to non\-Amazon prefixes\. For a current list of prefixes advertised by AWS, see [AWS IP Address Ranges](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the *Amazon Web Services General Reference*\.

**Note**  
We recommend that you use a firewall filter \(based on the source/destination address of packets\) to control traffic to and from some prefixes\. If you're using a prefix filter \(route map\), ensure that it accepts prefixes with an exact match or longer\. Prefixes advertised from AWS Direct Connect may be aggregated and may differ from the prefixes defined in your prefix filter\.

## Hosted virtual interfaces<a name="hosted-vif"></a>

To use your AWS Direct Connect connection with another AWS account, you can create a hosted virtual interface for that account\. The owner of the other account must accept the hosted virtual interface to begin using it\. A hosted virtual interface works the same as a standard virtual interface and can connect to public resources or a VPC\.

A connection of less than 1 Gbps supports only one virtual interface\.

To create a virtual interface, you need the following information:


| Resource | Required information | 
| --- | --- | 
| Connection | The AWS Direct Connect connection or link aggregation group \(LAG\) for which you are creating the virtual interface\. | 
| Virtual interface name | A name for the virtual interface\. | 
| Virtual interface owner | If you're creating the virtual interface for another account, you need the AWS account ID of the other account\. | 
| \(Private virtual interface only\) Connection | For connecting to a VPC in the same AWS Region, you need the virtual private gateway for your VPC\. The ASN for the Amazon side of the BGP session is inherited from the virtual private gateway\. When you create a virtual private gateway, you can specify your own private ASN\. Otherwise, Amazon provides a default ASN\. For more information, see [Create a Virtual Private Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/SetUpVPNConnections.html#vpn-create-vpg) in the Amazon VPC User Guide\. For connecting to a VPC through a Direct Connect gateway, you need the Direct Connect gateway\. For more information, see [Direct Connect Gateways](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways.html)\. | 
| VLAN | A unique virtual local area network \(VLAN\) tag that's not already in use on your connection\. The value must be between 1 and 4094 and must comply with the Ethernet 802\.1Q standard\. This tag is required for any traffic traversing the AWS Direct Connect connection\. If you have a hosted connection, your AWS Direct Connect Partner provides this value\. You can’t modify the value after you have created the virtual interface\. | 
| Peer IP addresses |  A virtual interface can support a BGP peering session for IPv4, IPv6, or one of each \(dual\-stack\)\. You cannot create multiple BGP sessions for the same IP addressing family on the same virtual interface\. The IP address ranges are assigned to each end of the virtual interface for the BGP peering session\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html)  | 
| Address family | Whether the BGP peering session will be over IPv4 or IPv6\. | 
| BGP information | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html) | 
| \(Public virtual interface only\) Prefixes you want to advertise |   Public IPv4 routes or IPv6 routes to advertise over BGP\. You must advertise at least one prefix using BGP, up to a maximum of 1,000 prefixes\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html) | 
| \(Private virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames apply only to propagated routes from AWS Direct Connect\. If you add static routes to a route table that point to your virtual private gateway, then traffic routed through the static routes is sent using 1500 MTU\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo Frame Capable on the Summary tab\. | 
| \(Transit virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames apply only to propagated routes from AWS Direct Connect\. If you add static routes to a route table that point to your virtual private gateway, then traffic routed through the static routes is sent using 1500 MTU\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo Frame Capable on the Summary tab\. | 

You can create a virtual interface for accounts within your AWS Organizations, or AWS Organizations that are different from yours\. You must accept the virtual interface before you can use it\. For information about how to create and accept a virtual interface, see [Creating a hosted virtual interface](createhostedvirtualinterface.md) and [Accepting a hosted virtual interface](accepthostedvirtualinterface.md)\.

## Prerequisites for virtual interfaces<a name="vif-prerequisites"></a>

Before you create a virtual interface, do the following:
+ Create a connection\. For more information, see [Creating a connection](create-connection.md)\.
+ Create a link aggregation group \(LAG\) when you have multiple connections that you want to treat as a single one\. For information, see [Associating a connection with a LAG](associate-connection-with-lag.md)\.

To create a virtual interface, you need the following information:


| Resource | Required information | 
| --- | --- | 
| Connection | The AWS Direct Connect connection or link aggregation group \(LAG\) for which you are creating the virtual interface\. | 
| Virtual interface name | A name for the virtual interface\. | 
| Virtual interface owner | If you're creating the virtual interface for another account, you need the AWS account ID of the other account\. | 
| \(Private virtual interface only\) Connection | For connecting to a VPC in the same AWS Region, you need the virtual private gateway for your VPC\. The ASN for the Amazon side of the BGP session is inherited from the virtual private gateway\. When you create a virtual private gateway, you can specify your own private ASN\. Otherwise, Amazon provides a default ASN\. For more information, see [Create a Virtual Private Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/SetUpVPNConnections.html#vpn-create-vpg) in the Amazon VPC User Guide\. For connecting to a VPC through a Direct Connect gateway, you need the Direct Connect gateway\. For more information, see [Direct Connect Gateways](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways.html)\. | 
| VLAN | A unique virtual local area network \(VLAN\) tag that's not already in use on your connection\. The value must be between 1 and 4094 and must comply with the Ethernet 802\.1Q standard\. This tag is required for any traffic traversing the AWS Direct Connect connection\. If you have a hosted connection, your AWS Direct Connect Partner provides this value\. You can’t modify the value after you have created the virtual interface\. | 
| Peer IP addresses |  A virtual interface can support a BGP peering session for IPv4, IPv6, or one of each \(dual\-stack\)\. You cannot create multiple BGP sessions for the same IP addressing family on the same virtual interface\. The IP address ranges are assigned to each end of the virtual interface for the BGP peering session\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html)  | 
| Address family | Whether the BGP peering session will be over IPv4 or IPv6\. | 
| BGP information | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html) | 
| \(Public virtual interface only\) Prefixes you want to advertise |   Public IPv4 routes or IPv6 routes to advertise over BGP\. You must advertise at least one prefix using BGP, up to a maximum of 1,000 prefixes\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html) | 
| \(Private virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames apply only to propagated routes from AWS Direct Connect\. If you add static routes to a route table that point to your virtual private gateway, then traffic routed through the static routes is sent using 1500 MTU\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo Frame Capable on the Summary tab\. | 
| \(Transit virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames apply only to propagated routes from AWS Direct Connect\. If you add static routes to a route table that point to your virtual private gateway, then traffic routed through the static routes is sent using 1500 MTU\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo Frame Capable on the Summary tab\. | 

When you create a virtual interface, you can specify the account that owns the virtual interface\. When you choose an AWS account that is not your account, the following rules apply:
+ For private VIFs and transit VIFs, the account applies to the virtual interface and the virtual private gateway/Direct Connect gateway destination\.
+ For public VIFs, the account is used for virtual interface billing\. The Data Transfer Out \(DTO\) usage is metered toward the resource owner at AWS Direct Connect data transfer rate\.