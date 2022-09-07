# Allowed prefixes interactions<a name="allowed-to-prefixes"></a>

Learn how allowed prefixes interact with transit gateways and virtual private gateways\. For more information, see [Routing policies and BGP communities](routing-and-bgp.md)\.

## Virtual private gateway associations<a name="allowed-to-prefixes-virtual-private-gateway"></a>

The prefix list \(IPv4 and IPv6\) acts as a filter that allows the same CIDRs, or a smaller range of CIDRs to be advertised to the Direct Connect gateway\. You must set the prefixes to a range that is the same or wider than the VPC CIDR block\.

**Note**  
The allowed list only functions as a filter, and only the associated VPC CIDR will be advertised to the customer gateway\. 

Consider the scenario where you have a VPC with CIDR 10\.0\.0\.0/16 is attached to a virtual private gateway\.
+ When the allowed prefixes list is set to 22\.0\.0\.0/24, you do not receive any route because 22\.0\.0\.0/24 is not the same as, or wider than 10\.0\.0\.0/16\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/24, you do not receive any route because 10\.0\.0\.0/24 is not the same as 10\.0\.0\.0/16\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/15, you do receive 10\.0\.0\.0/16, because the IP address is wider than 10\.0\.0\.0/16\.

When you remove or add an allowed prefix, traffic which doesn't use that prefix is not impacted\. During updates the status changes from `associated` to `updating`\. Modifying an existing prefix can delay only that traffic which uses that prefix\. 

## Transit gateway associations<a name="allowed-to-prefixes-transit-gateway"></a>

For a transit gateway association, you provision the allowed prefixes list on the Direct Connect gateway\. The list routes on\-premises traffic to or from a Direct Connect gateway to the transit gateway, even when the VPCs attached to the transit gateway do not have assigned CIDRs\. Prefixes in the Direct Connect gateway allowed prefix list originate on the Direct Connect gateway and are advertised to the on\-premises network\.

Consider the scenario where you have a VPC with CIDR 10\.0\.0\.0/16 attached to a transit gateway\.
+ When the allowed prefixes list is set to 22\.0\.0\.0/24, you receive 22\.0\.0\.0/24 through BGP on your transit virtual interface\. You do not receive 10\.0\.0\.0/16 because we directly provision the prefixes that are in the allowed prefix list\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/24, you receive 10\.0\.0\.0/24 through BGP on your transit virtual interface\. You do not receive 10\.0\.0\.0/16 because we directly provision the prefixes that are in the allowed prefix list\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/8, you receive 10\.0\.0\.0/8 through BGP on your transit virtual interface\. 