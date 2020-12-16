# Allowed prefixes interactions<a name="allowed-to-prefixes"></a>

Learn how allowed prefixes interact with transit gateways and virtual private gateways\. For more information, see [Routing policies and BGP communities](routing-and-bgp.md)\.

## Transit gateway associations<a name="allowed-to-prefixes-transit-gateway"></a>

When you associate a transit gateway with a Direct Connect gateway, you specify a list of up to twenty Amazon VPC prefixes to advertise to the Direct Connect gateway\. The prefix list acts as a filter that allows the same CIDRs, or a smaller range of CIDRs to be advertised to the Direct Connect gateway\. You must set the prefixes to a range that is the same or wider than the VPC CIDR block\.

Consider the scenario where you have a VPC with CIDR 10\.0\.0\.0/16 attached to a transit gateway\.
+ When the allowed prefixes list is set to 22\.0\.0\.0/24, you receive 22\.0\.0\.0/24 through BGP on your transit virtual interface\. You do not receive 10\.0\.0\.0/16 because we directly provision the prefixes that are in the allowed prefix list\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/24, you receive 10\.0\.0\.0/24 through BGP on your transit virtual interface\. You do not receive 10\.0\.0\.0/16 because we directly provision the prefixes that are in the allowed prefix list\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/8, you receive 10\.0\.0\.0/8 through BGP on your transit virtual interface\. 

## Virtual private gateway associations<a name="allowed-to-prefixes-virtual-private-gateway"></a>

Consider the scenario where you have a VPC with CIDR 10\.0\.0\.0/16 is attached to a virtual private gateway\.
+ When the allowed prefixes list is set to 22\.0\.0\.0/24, you do not receive any route because 22\.0\.0\.0/24 is not the same as, or wider than 10\.0\.0\.0/16\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/24, you do not receive any route because 10\.0\.0\.0/24 is not the same as 10\.0\.0\.0/16\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/15, you do receive 10\.0\.0\.0/16, because the IP address is wider than 10\.0\.0\.0/16\.