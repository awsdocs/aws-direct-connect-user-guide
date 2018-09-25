# Deleting a LAG<a name="delete-lag"></a>

If you no longer need a LAG, you can delete it\. You cannot delete a LAG if it has virtual interfaces associated with it—you must first delete the virtual interfaces, or associate them with a different LAG or connection\. Deleting a LAG does not delete the connections in the LAG; you must delete the connections yourself\. For more information, see [Deleting a Connection](deleteconnection.md)\.

**To delete a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG and choose **Actions**, **Delete LAG**\.

1. Select the confirmation check box and choose **Continue**\.

**To delete a LAG using the command line or API**
+ [delete\-lag](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-lag.html) \(AWS CLI\)
+ [DeleteLag](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteLag.html) \(AWS Direct Connect API\)