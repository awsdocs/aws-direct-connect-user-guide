# Creating a Direct Connect Gateway<a name="create-direct-connect-gateway"></a>

You can create a Direct Connect gateway in any supported public Region\. 

**To create a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect Gateways**\.

1. Choose **Create Direct Connect gateway**\.

1. Specify the following information, and choose **Create Direct Connect gateway**\.
   + **Name**: Enter a name to help you identify the Direct Connect gateway\.
   + **Amazon side ASN**: Specify the ASN for the Amazon side of the BGP session\. The ASN must be in the 64,512 to 65,534 range or 4,200,000,000 to 4,294,967,294 range\.
   + **Virtual private gateway**: To associate a virtual private gateway, choose the virtual private gateway\.

**To create a Direct Connect gateway using the command line or API**
+ [create\-direct\-connect\-gateway](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-direct-connect-gateway.html) \(AWS CLI\)
+ [CreateDirectConnectGateway](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateDirectConnectGateway.html) \(AWS Direct Connect API\)