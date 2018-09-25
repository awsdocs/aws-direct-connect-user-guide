# Accepting a Hosted Virtual Interface<a name="accepthostedvirtualinterface"></a>

Before you can begin using a hosted virtual interface, you must accept the virtual interface\. For a private virtual interface, you must also have an existing virtual private gateway or Direct Connect Gateway\.

**To accept a hosted virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. If necessary, change the region in the navigation bar\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface\.

1. Select the confirmation check box and choose **Accept Virtual Interface**\.

1. \(Private virtual interface\) In the **Accept Virtual Interface** dialog box, select a virtual private gateway or Direct Connect gateway, and choose **Accept**\.

1. After you've accepted the hosted virtual interface, the owner of the AWS Direct Connect connection can download the router configuration file\. The **Download Router Configuration** option is not available for the account that accepts the hosted virtual interface\.

**To accept a hosted private virtual interface using the command line or API**
+ [confirm\-private\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/confirm-private-virtual-interface.html) \(AWS CLI\)
+ [ConfirmPrivateVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_ConfirmPrivateVirtualInterface.html) \(AWS Direct Connect API\)

**To accept a hosted public virtual interface using the command line or API**
+ [confirm\-public\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/confirm-public-virtual-interface.html) \(AWS CLI\)
+ [ConfirmPublicVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_ConfirmPublicVirtualInterface.html) \(AWS Direct Connect API\)