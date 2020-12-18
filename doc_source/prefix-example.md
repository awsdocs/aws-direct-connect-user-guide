# Example: Allowed to prefixes in a transit gateway configuration<a name="prefix-example"></a>

Consider the configuration where you have instance in two different AWS Regions which need to access the corporate data center\. You can use the following resources for this configuration:
+ A transit gateway in each Region\.
+ A transit gateway peering connection\.
+ A Direct connect gateway\.
+ A transit gateway association between one of the transit gateways \(the one in us\-east\-1\) to the Direct Connect gateway\.
+ A transit virtual interface from the on\-premises location and the AWS Direct Connect location\.

![\[Private VIF Routing no AS_PATH\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/dxg-asn.png)

Configure the following options for the resources\.
+ Direct Connect gateway: Set the ASN for to 65030\. For more information, see [Creating a Direct Connect gateway](direct-connect-gateways-intro.md#create-direct-connect-gateway)\.
+ Transit virtual interface: Set the VLAN to 899, and the ASN to 65020\. For more information, see [Creating a transit virtual interface to the Direct Connect gateway](create-vif.md#create-transit-vif)\.
+ Direct Connect gateway association with the transit gateway: Set the allowed to prefixes to 10\.0\.0\.0/8\. 

  This CIDR block covers both VPC CIDR blocks\. For more information, see [Associating and disassociating transit gateways](direct-connect-transit-gateways.md#associate-tgw-with-direct-connect-gateway)\.
+ VPC route: To route traffic from the 10\.2\.0\.0 VPC, create a route in the VPC route table which has a Destination of 0\.0\.0\.0/0 and the transit gateway ID as the Target\. For more information about routing to a transit gateway, see [Routing for a transit gateway](https://docs.aws.amazon.com/vpc/latest/userguide/route-table-options.html#route-tables-tgw) in the* Amazon VPC User Guide*\.