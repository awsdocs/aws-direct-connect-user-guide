# AWS Direct Connect virtual interfaces<a name="WorkingWithVirtualInterfaces"></a>

You must create one of the following virtual interfaces to begin using your AWS Direct Connect connection\. 
+ Private virtual interface: A private virtual interface should be used to access an Amazon VPC using private IP addresses\.
+ Public virtual interface: A public virtual interface can access all AWS public services using public IP addresses\.
+ Transit virtual interface: A transit virtual interface should be used to access one or more Amazon VPC Transit Gateways associated with Direct Connect gateways\. You can use transit virtual interfaces with any AWS Direct Connect dedicated or hosted connection\. For information about Direct Connect gateway configurations, see [Direct Connect gateways](direct-connect-gateways-intro.md)\.

To connect to other AWS services using IPv6 addresses, check the service documentation to verify that IPv6 addressing is supported\.

## Public virtual interface prefix advertisement rules<a name="advertise-prefixes"></a>

We advertise appropriate Amazon prefixes to you so that you can reach either your VPCs or other AWS services\. You can access all AWS prefixes through this connection; for example, Amazon EC2, Amazon S3, and Amazon\.com\. You do not have access to non\-Amazon prefixes\. For a current list of prefixes advertised by AWS, see [AWS IP Address Ranges](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the *Amazon Web Services General Reference*\. AWS does not re\-advertise customer prefixes that were received over AWS Direct Connect public virtual interfaces to other customers\. For more information about public virtual interfaces and routing policies, see [Public virtual interface routing policies](routing-and-bgp.md#routing-policies)\.

**Note**  
We recommend that you use a firewall filter \(based on the source/destination address of packets\) to control traffic to and from some prefixes\. If you're using a prefix filter \(route map\), ensure that it accepts prefixes with an exact match or longer\. Prefixes advertised from AWS Direct Connect may be aggregated and may differ from the prefixes defined in your prefix filter\.

## Hosted virtual interfaces<a name="hosted-vif"></a>

To use your AWS Direct Connect connection with another account, you can create a hosted virtual interface for that account\. The owner of the other account must accept the hosted virtual interface to begin using it\. A hosted virtual interface works the same as a standard virtual interface and can connect to public resources or a VPC\.

You can use transit virtual interfaces with 1/2/5/10/100 Gbps, and at speeds of 500 megabits per second \(Mbps\) and lower, Direct Connect dedicated or hosted connections\. A connection of less than 1 Gbps supports only one virtual interface\.

To create a virtual interface, you need the following information:


| Resource | Required information | 
| --- | --- | 
| Connection | The AWS Direct Connect connection or link aggregation group \(LAG\) for which you are creating the virtual interface\. | 
| Virtual interface name | A name for the virtual interface\. | 
| Virtual interface owner | If you're creating the virtual interface for another account, you need the AWS account ID of the other account\. | 
| \(Private virtual interface only\) Connection | For connecting to a VPC in the same AWS Region, you need the virtual private gateway for your VPC\. The ASN for the Amazon side of the BGP session is inherited from the virtual private gateway\. When you create a virtual private gateway, you can specify your own private ASN\. Otherwise, Amazon provides a default ASN\. For more information, see [Create a Virtual Private Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/SetUpVPNConnections.html#vpn-create-vpg) in the Amazon VPC User Guide\. For connecting to a VPC through a Direct Connect gateway, you need the Direct Connect gateway\. For more information, see [Direct Connect Gateways](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways.html)\. | 
| VLAN | A unique virtual local area network \(VLAN\) tag that's not already in use on your connection\. The value must be between 1 and 4094 and must comply with the Ethernet 802\.1Q standard\. This tag is required for any traffic traversing the AWS Direct Connect connection\. If you have a hosted connection, your AWS Direct Connect Partner provides this value\. You can’t modify the value after you have created the virtual interface\. | 
| Peer IP addresses |  A virtual interface can support a BGP peering session for IPv4, IPv6, or one of each \(dual\-stack\)\. Do not use Elastic IPs \(EIPs\) from the Amazon Pool to create a public virtual interface\. You cannot create multiple BGP sessions for the same IP addressing family on the same virtual interface\. The IP address ranges are assigned to each end of the virtual interface for the BGP peering session\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html)  | 
| Address family | Whether the BGP peering session will be over IPv4 or IPv6\. | 
| BGP information | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html) | 
| \(Public virtual interface only\) Prefixes you want to advertise |   Public IPv4 routes or IPv6 routes to advertise over BGP\. You must advertise at least one prefix using BGP, up to a maximum of 1,000 prefixes\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html) | 
| \(Private virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames apply only to propagated routes from AWS Direct Connect\. If you add static routes to a route table that point to your virtual private gateway, then traffic routed through the static routes is sent using 1500 MTU\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo frame capable on the virtual interface General configuration page\. | 
| \(Transit virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames are supported up to 8500 MTU for Direct Connect\. Static routes and propagated routes configured in the Transit Gateway Route Table will support Jumbo Frames, including from EC2 instances with VPC static route table entries to the Transit Gateway Attachment\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo frame capable on the virtual interface General configuration page\. | 

## SiteLink<a name="dx-sitelink"></a>

If you're creating a private or transit virtual interface, you can use SiteLink\.

SiteLink is an optional Direct Connect feature for virtual private interfaces that enables connectivity between any two Direct Connect points of presence \(PoPs\) in the same AWS partition using the shortest available path over the AWS network\. This allows you to connect your on\-premises network through the AWS global network without needing to route your traffic through a Region\. For more information about SiteLink see [Introducing AWS Direct Connect SiteLink](https://aws.amazon.com/blogs/networking-and-content-delivery/introducing-aws-direct-connect-sitelink/)\.

**Note**  
SiteLink is not available in AWS GovCloud \(US\) and the China Regions\.

There's a separate pricing fee for using SiteLink\. For more information, see [AWS Direct Connect Pricing](https://aws.amazon.com/directconnect/pricing/)\.

SiteLink doesn't support all virtual interface types\. The following table shows the interface type and whether it's supported\. 


| Virtual interface type | Supported/Not supported | 
| --- | --- | 
|  Transit virtual interface  |  Supported  | 
|  Private virtual interface attached to a Direct Connect gateway with a virtual gateway  |  Supported  | 
|  Private virtual interface attached to a Direct Connect gateway not associated with a virtual gateway or transit gateway  |  Supported  | 
|  Private virtual interface attached to a virtual gateway  |  Not supported  | 
|  Public virtual interface  |  Not supported  | 

## Prerequisites for virtual interfaces<a name="vif-prerequisites"></a>

Before you create a virtual interface, do the following:
+ Create a connection\. For more information, see [Create a connection](create-connection.md)\.
+ Create a link aggregation group \(LAG\) when you have multiple connections that you want to treat as a single one\. For information, see [Associate a connection with a LAG](associate-connection-with-lag.md)\.

To create a virtual interface, you need the following information:


| Resource | Required information | 
| --- | --- | 
| Connection | The AWS Direct Connect connection or link aggregation group \(LAG\) for which you are creating the virtual interface\. | 
| Virtual interface name | A name for the virtual interface\. | 
| Virtual interface owner | If you're creating the virtual interface for another account, you need the AWS account ID of the other account\. | 
| \(Private virtual interface only\) Connection | For connecting to a VPC in the same AWS Region, you need the virtual private gateway for your VPC\. The ASN for the Amazon side of the BGP session is inherited from the virtual private gateway\. When you create a virtual private gateway, you can specify your own private ASN\. Otherwise, Amazon provides a default ASN\. For more information, see [Create a Virtual Private Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/SetUpVPNConnections.html#vpn-create-vpg) in the Amazon VPC User Guide\. For connecting to a VPC through a Direct Connect gateway, you need the Direct Connect gateway\. For more information, see [Direct Connect Gateways](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways.html)\. | 
| VLAN | A unique virtual local area network \(VLAN\) tag that's not already in use on your connection\. The value must be between 1 and 4094 and must comply with the Ethernet 802\.1Q standard\. This tag is required for any traffic traversing the AWS Direct Connect connection\. If you have a hosted connection, your AWS Direct Connect Partner provides this value\. You can’t modify the value after you have created the virtual interface\. | 
| Peer IP addresses |  A virtual interface can support a BGP peering session for IPv4, IPv6, or one of each \(dual\-stack\)\. Do not use Elastic IPs \(EIPs\) from the Amazon Pool to create a public virtual interface\. You cannot create multiple BGP sessions for the same IP addressing family on the same virtual interface\. The IP address ranges are assigned to each end of the virtual interface for the BGP peering session\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html)  | 
| Address family | Whether the BGP peering session will be over IPv4 or IPv6\. | 
| BGP information | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html) | 
| \(Public virtual interface only\) Prefixes you want to advertise |   Public IPv4 routes or IPv6 routes to advertise over BGP\. You must advertise at least one prefix using BGP, up to a maximum of 1,000 prefixes\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html) | 
| \(Private virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames apply only to propagated routes from AWS Direct Connect\. If you add static routes to a route table that point to your virtual private gateway, then traffic routed through the static routes is sent using 1500 MTU\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo frame capable on the virtual interface General configuration page\. | 
| \(Transit virtual interface only\) Jumbo frames | The maximum transmission unit \(MTU\) of packets over AWS Direct Connect\. The default is 1500\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. Jumbo frames are supported up to 8500 MTU for Direct Connect\. Static routes and propagated routes configured in the Transit Gateway Route Table will support Jumbo Frames, including from EC2 instances with VPC static route table entries to the Transit Gateway Attachment\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find Jumbo frame capable on the virtual interface General configuration page\. | 

When you create a virtual interface, you can specify the account that owns the virtual interface\. When you choose an AWS account that is not your account, the following rules apply:
+ For private VIFs and transit VIFs, the account applies to the virtual interface and the virtual private gateway/Direct Connect gateway destination\.
+ For public VIFs, the account is used for virtual interface billing\. The Data Transfer Out \(DTO\) usage is metered toward the resource owner at AWS Direct Connect data transfer rate\.

**Note**  
31\-Bit prefixes are supported on all Direct Connect virtual interface types\. See [RFC 3021: Using 31\-Bit Prefixes on IPv4 Point\-to\-Point Links](https://datatracker.ietf.org/doc/html/rfc3021) for more information\.