# Delete connections<a name="deleteconnection"></a>

You can delete a connection as long as there are no virtual interfaces attached to it\. Deleting your connection stops all port hour charges for this connection\. AWS Direct Connect data transfer charges are associated with virtual interfaces\. For more information about how to delete a virtual interface, see [Delete virtual interfaces](deletevif.md)\.

Before deleting a connection, download the LOA for the connection containing the cross account information\. The facilities or circuit provider might need this information to properly disconnect cross connects and circuits from AWS\. Any cross connect or network circuit charges are independent of AWS Direct Connect and must be cancelled with the facilities or circuit provider\. For the steps to download the connection LOA, see [Download the LOA\-CFA](dedicated_connection.md#create-connection-loa-cfa)\.

If the connection is part of a link aggregation group \(LAG\), you cannot delete the connection if doing so causes the LAG to fall below its setting for the minimum number of operational connections\. 

------
#### [ Console ]

**To delete a connection**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Connections**\.

1. Select the connections and choose **Delete**\.

1. In the **Delete confirmation** dialog box, choose **Delete**\.

------
#### [ Command line ]

**To delete a connection using the command line or API**
+ [delete\-connection](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-connection.html) \(AWS CLI\)
+ [DeleteConnection](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteConnection.html) \(AWS Direct Connect API\)

------