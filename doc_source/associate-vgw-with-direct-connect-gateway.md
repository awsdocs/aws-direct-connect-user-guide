# Associating and Disassociating Virtual Private Gateways<a name="associate-vgw-with-direct-connect-gateway"></a>

To associate a virtual private gateway with a Direct Connect gateway, you must be in the Region in which the virtual private gateway is located\. The virtual private gateway must be attached to the VPC to which you want to connect\. For more information, see [Create a Virtual Private Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_VPN.html#vpn-create-vpg) in the *Amazon VPC User Guide*\.

**Note**  
If you are planning to use the virtual private gateway for a Direct Connect gateway and a dynamic VPN connection, set the ASN on the virtual private gateway to the value you require for the VPN connection\. Otherwise, the ASN on the virtual private gateway can be set to any permitted value\. The Direct Connect gateway advertises all connected VPCs over the ASN assigned to it\.

**To associate a virtual private gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home/](https://console.aws.amazon.com/directconnect/v2/home/)\.

1. In the navigation pane, choose **Direct Connect Gateways** and select the Direct Connect gateway\.

1. Choose **View details**\.

1. Choose **Virtual gateways associations** and choose **Associate virtual private gateway**\.

1. For **Virtual private gateway**, choose the virtual private gateways to associate, and choose **Associate virtual private gateway**\.

You can view all of the virtual private gateways in all Regions that are associated with the Direct Connect gateway by choosing **Virtual Gateway Associations**\. To disassociate a virtual private gateway from a Direct Connect gateway, you must be in the Region in which the virtual private gateway is located\.

**To disassociate a virtual private gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home/](https://console.aws.amazon.com/directconnect/v2/home/)\.

1. Use the Region selector to switch to the Region in which your virtual private gateway is located\.

1. In the navigation pane, choose **Direct Connect Gateways** and select the Direct Connect gateway\.

1. Choose **View details**\.

1. Choose **Virtual gateways associations** and select the virtual private gateway\.

1. Choose **Disassociate**\.

**To associate a virtual private gateway using the command line or API**
+ [create\-direct\-connect\-gateway\-association](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-direct-connect-gateway-association.html) \(AWS CLI\)
+ [CreateDirectConnectGatewayAssociation](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)

**To view the virtual private gateways associated with a Direct Connect gateway using the command line or API**
+ [describe\-direct\-connect\-gateway\-associations](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-associations.html) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAssociations](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAssociations.html) \(AWS Direct Connect API\)

**To disassociate a virtual private gateway using the command line or API**
+ [delete\-direct\-connect\-gateway\-association](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway-association.html) \(AWS CLI\)
+ [DeleteDirectConnectGatewayAssociation](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)