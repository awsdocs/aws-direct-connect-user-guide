# Deleting LAGs<a name="delete-lag"></a>

If you no longer need LAGs, you can delete them\. You cannot delete a LAG if it has virtual interfaces associated with it\. You must first delete the virtual interfaces, or associate them with a different LAG or connection\. Deleting a LAG does not delete the connections in the LAG; you must delete the connections yourself\. For more information, see [Deleting Connections](deleteconnection.md)\.

**To delete a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home/](https://console.aws.amazon.com/directconnect/v2/home/)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAGs and choose **Delete**\.

1. In the confirmation dialog box choose **Delete**\.

**To delete a LAG using the command line or API**
+ [delete\-lag](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-lag.html) \(AWS CLI\)
+ [DeleteLag](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteLag.html) \(AWS Direct Connect API\)