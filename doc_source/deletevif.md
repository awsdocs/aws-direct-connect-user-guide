# Deleting a Virtual Interface<a name="deletevif"></a>

Before you can delete a connection, you must delete its virtual interface\. The number of virtual interfaces configured on a connection is listed in the **\# VIs** column in the **Connection** pane\. Deleting a virtual interface stops AWS Direct Connect data transfer charges associated with the virtual interface\.

**To delete a virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface, and then choose **Actions**, **Delete Virtual Interface**\.

1. In the **Delete Virtual Interface** dialog box, choose **Delete**\.

**To delete a virtual interface using the command line or API**
+ [delete\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-virtual-interface.html) \(AWS CLI\)
+ [DeleteVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteVirtualInterface.html) \(AWS Direct Connect API\)