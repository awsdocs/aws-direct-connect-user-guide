# Direct Connect Gateways<a name="direct-connect-gateways"></a>

You can use an *AWS Direct Connect gateway* to connect your AWS Direct Connect connection over a private virtual interface to one or more VPCs in your account that are located in the same or different Regions\. You associate a Direct Connect gateway with the virtual private gateway for the VPC\. Then, create a private virtual interface for your AWS Direct Connect connection to the Direct Connect gateway\. You can attach multiple private virtual interfaces to your Direct Connect gateway\.

A Direct Connect gateway is a globally available resource\. You can create the Direct Connect gateway in any public Region and access it from all other public Regions\.

In the following diagram, the Direct Connect gateway enables you to use your AWS Direct Connect connection in the US East \(N\. Virginia\) Region to access VPCs in your account in both the US East \(N\. Virginia\) and US West \(N\. California\) Regions\.

![\[Direct connect gateway\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/dx-gateway.png)

Complete the following steps for this configuration\.

1.  Create a Direct Connect gateway\.

1. Associate each private virtual gateway with the Direct Connect gateway\.

1. Create a private virtual interface between the Direct Connect gateway and the Direct Connect location\.

The following rules apply:
+ You cannot use a Direct Connect gateway to connect to a VPC in the China Regions\.
+ You cannot use a Direct Connect gateway that's in your account to connect to a VPC that's in a different AWS account\. To associate a Direct Connect gateway with a virtual private gateway, it must be in the same account as the virtual private gateway\.
+ There are limits for creating and using Direct Connect gateways\. For more information, see [AWS Direct Connect Limits](limits.md)
+ The VPCs to which you connect through a Direct Connect gateway cannot have overlapping CIDR blocks\. If you add an IPv4 CIDR block to a VPC that's associated with a Direct Connect gateway, ensure that the CIDR block does not overlap with an existing CIDR block for any other associated VPC\. For more information, see [Adding IPv4 CIDR Blocks to a VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#vpc-resize) in the *Amazon VPC User Guide*\.
+ You cannot create a public virtual interface to a Direct Connect gateway\.
+ A Direct Connect gateway supports communication between attached private virtual interfaces and associated virtual private gateways only\. The following traffic flows are not supported:
  + Direct communication between the VPCs that are associated with the Direct Connect gateway\.
  + Direct communication between the virtual interfaces that are attached to the Direct Connect gateway\.
  + Direct communication between a virtual interface attached to a Direct Connect gateway and a VPN connection on a virtual private gateway that's associated with the same Direct Connect gateway\.
+ You cannot associate a virtual private gateway with more than one Direct Connect gateway and you cannot attach a private virtual interface to more than one Direct Connect gateway\.
+ A virtual private gateway that you associate with a Direct Connect gateway must be attached to a VPC\.

To connect your AWS Direct Connect connection to a VPC in the same Region only, you can create a Direct Connect gateway\. Or, you can create a private virtual interface and attach it to the virtual private gateway for the VPC\. For more information, see [Creating a Private Virtual Interface](create-vif.md#create-private-vif) and [VPN CloudHub](https://docs.aws.amazon.com/vpc/latest/userguide/VPN_CloudHub.html)\.

To use your AWS Direct Connect connection with a VPC in another account, you can create a hosted private virtual interface for that account\. When the owner of the other account accepts the hosted virtual interface, they can choose to attach it to either a virtual private gateway or a Direct Connect gateway in their account\. For more information, see [AWS Direct Connect Virtual Interfaces](WorkingWithVirtualInterfaces.md)\.

**Topics**
+ [Creating a Direct Connect Gateway](create-direct-connect-gateway.md)
+ [Associating and Disassociating Virtual Private Gateways](associate-vgw-with-direct-connect-gateway.md)
+ [Creating a Private Virtual Interface to the Direct Connect Gateway](create-private-vif-for-gateway.md)
+ [Adding or Removing Direct Connect Gateway Tags](modify-tags-gateway.md)
+ [Deleting Direct Connect Gateways](delete-direct-connect-gateway.md)