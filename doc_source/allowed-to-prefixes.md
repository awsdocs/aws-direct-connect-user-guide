# Allowed Prefixes Interactions<a name="allowed-to-prefixes"></a>

## Transit Gateway Associations<a name="allowed-to-prefixes-transit-gateway"></a>

For a transit gateway, association, you provision the allowed prefixes list on the Direct Connect gateway\. The list is used to route traffic from on\-premises to AWS into the transit gateway even if the VPCs attached to the transit gateway do not have assigned CIDRs\. Prefixes in the Direct Connect gateway allowed prefix list originate on the Direct Connect gateway and are advertised to the on\-premises network\.

For example, consider the scenario where you have a VPC with CIDR 10\.0\.0\.0/16 is attached to a transit gateway\.
+ When the allowed prefixes list is set to 22\.0\.0\.0/24, you receive 22\.0\.0\.0/24 via BGP on your transit virtual interface\. You do not receive 10\.0\.0\.0/16 because we directly provision the prefixes that are in the allowed prefix list\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/24, you receive 10\.0\.0\.0/24 via BGP on your transit virtual interface\. You do not receive 10\.0\.0\.0/16 because we directly provision the prefixes that are in the allowed prefix list\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/8, you receive 10\.0\.0\.0/8 via BGP on your transit virtual interface\. You do not receive 10\.0\.0\.0/16 because we directly provision the prefixes that are in the allowed prefix list\.

## Virtual Private Gateway Associations<a name="allowed-to-prefixes-virtual-private-gateway"></a>

For example, consider the scenario where you have a VPC with CIDR 10\.0\.0\.0/16 is attached to a virtual private gateway\.
+ When the allowed prefixes list is set to 22\.0\.0\.0/24, you do not receive any route because 22\.0\.0\.0/24 is not the same or wider than 10\.0\.0\.0/16\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/24, you do not receive any route because 10\.0\.0\.0/24 is not the same or wider than 10\.0\.0\.0/16\.
+ When the allowed prefixes list is set to 10\.0\.0\.0/15, you do receive 10\.0\.0\.0/16, because the IP address is wider than 10\.0\.0\.0/16\.