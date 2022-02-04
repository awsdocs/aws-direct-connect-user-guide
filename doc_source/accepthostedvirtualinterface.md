# Accept a hosted virtual interface<a name="accepthostedvirtualinterface"></a>

Before you can begin using a hosted virtual interface, you must accept the virtual interface\. For a private virtual interface, you must also have an existing virtual private gateway or Direct Connect gateway\. For a transit virtual interface, you must have an existing transit gateway or Direct Connect gateway\.

**To accept a hosted virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and then choose **View details**\.

1. Choose **Accept**\.

1. This applies to private virtual interfaces and transit virtual interfaces\.

   \(Transit virtual interface\) In the **Accept virtual interface** dialog box, select a Direct Connect gateway, and then choose **Accept virtual interface**\.

   \(Private virtual interface\) In the **Accept virtual interface** dialog box, select a virtual private gateway or Direct Connect gateway, and then choose **Accept virtual interface**\.

1. After you accept the hosted virtual interface, the owner of the AWS Direct Connect connection can download the router configuration file\. The **Download router configuration** option is not available for the account that accepts the hosted virtual interface\.

**To accept a hosted private virtual interface using the command line or API**
+ [confirm\-private\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/confirm-private-virtual-interface.html) \(AWS CLI\)
+ [ConfirmPrivateVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_ConfirmPrivateVirtualInterface.html) \(AWS Direct Connect API\)

**To accept a hosted public virtual interface using the command line or API**
+ [confirm\-public\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/confirm-public-virtual-interface.html) \(AWS CLI\)
+ [ConfirmPublicVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_ConfirmPublicVirtualInterface.html) \(AWS Direct Connect API\)

**To accept a hosted transit virtual interface using the command line or API**
+ [confirm\-transit\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/confirm-transit-virtual-interface.html) \(AWS CLI\)
+ [ConfirmTransitVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_ConfirTransitVirtualInterface.html) \(AWS Direct Connect API\)