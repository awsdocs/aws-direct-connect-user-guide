# Accessing a Remote AWS Region<a name="remote_regions"></a>

AWS Direct Connect locations in public regions or AWS GovCloud \(US\) can access public services in any other public region \(excluding China \(Beijing\)\)\. In addition, AWS Direct Connect connections in public regions or AWS GovCloud \(US\) can be configured to access a VPC in your account in any other public region \(excluding China \(Beijing\)\)\. You can therefore use a single AWS Direct Connect connection to build multi\-region services\. All networking traffic remains on the AWS global network backbone, regardless of whether you access public AWS services or a VPC in another region\.

Any data transfer out of a remote region is billed at the remote region data transfer rate\. For more information about data transfer pricing, see the [Pricing](http://aws.amazon.com/directconnect/pricing/) section on the AWS Direct Connect detail page\.

For more information about the routing polices and supported BGP communities for an AWS Direct Connect connection, see [Routing Policies and BGP Communities](routing-and-bgp.md)\.

## Accessing Public Services in a Remote Region<a name="inter-region-public"></a>

To access public resources in a remote region, you must set up a public virtual interface and establish a Border Gateway Protocol \(BGP\) session\. For more information, see [Virtual Interfaces](WorkingWithVirtualInterfaces.md)\.

After you have created a public virtual interface and established a BGP session to it, your router learns the routes of the other public AWS regions\. For more information about prefixes currently advertised by AWS, see [AWS IP Address Ranges](http://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the *Amazon Web Services General Reference*\.

## Accessing VPCs in a Remote Region<a name="inter-region-private"></a>

You can create a *Direct Connect gateway* in any public region and use it to connect your AWS Direct Connect connection over a private virtual interface to VPCs in your account that are located in different regions\. For more information, see [Direct Connect Gateways](direct-connect-gateways.md)\.

Alternatively, you can create a public virtual interface for your AWS Direct Connect connection and then establish a VPN connection to your VPC in the remote region\. For more information about configuring VPN connectivity to a VPC, see [Scenarios for Using Amazon Virtual Private Cloud](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Scenarios.html) in the *Amazon VPC User Guide*\. 