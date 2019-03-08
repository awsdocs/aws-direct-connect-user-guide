# Deleting Direct Connect Gateways<a name="delete-direct-connect-gateway"></a>

If you no longer require a Direct Connect gateway, you can delete it\. You must first [disassociate](associate-vgw-with-direct-connect-gateway.md) all associated virtual private gateways and [delete](deletevif.md) the attached private virtual interface\.

**To delete a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home/](https://console.aws.amazon.com/directconnect/v2/home/)\.

1. In the navigation pane, choose **Direct Connect Gateways**\.

1. Select the gateways and choose **Delete**\.

**To delete a Direct Connect gateway using the command line or API**
+ [delete\-direct\-connect\-gateway](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway.html) \(AWS CLI\)
+ [DeleteDirectConnectGateway](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGateway.html) \(AWS Direct Connect API\)