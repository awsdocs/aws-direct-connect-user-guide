# Creating a LAG<a name="create-lag"></a>

You can create a LAG by provisioning new connections, or aggregating existing connections\.

You cannot create a LAG with new connections if this results in you exceeding the overall connections limit for the region\.

**To create a LAG with new connections**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **LAGs**\.

1. Choose **Create LAG**\.

1. Choose **Request new Connections**, and provide the following information:
   + **Location**: The location for the LAG\.
   + **LAG Name**: A name for the LAG\.
   + **Connection Bandwidth**: The port speed for the connections\.
   + **Number of new Connections**: The number of connections that must be provisioned in the LAG\.

1. Choose **Create**\.

To create a LAG from existing connections, the connections must be on the same AWS device \(terminate at the same AWS Direct Connect endpoint\), and they must use the same bandwidth\. You cannot migrate a connection from an existing LAG if removing the connection causes the original LAG to fall below its setting for minimum number of operational connections\.

**Important**  
For existing connections, connectivity to AWS is interrupted during the creation of the LAG\.

**To create a LAG from existing connections**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **LAGs**\.

1. Choose **Create LAG**\.

1. Choose **Use existing Connections**, and select the required connections\.

1. For **LAG Name**, specify a name for the LAG\. For **Set Minimum Links**, specify the minimum number of connections that must be operational for the LAG itself to be operational\. If you do not specify a value, we assign a default value of 0\.  
![\[Create a LAG screen\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/create_lag_existing_connections.png)

1. Select the confirmation check box and choose **Create**\.

After you've created a LAG, you can view its details in the AWS Direct Connect console\.

**To view information about your LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG\.

1. You can view information about the LAG, including its ID, the AWS Direct Connect endpoint on which the connections terminate \(**AWS Device**\), and the number of connections in the LAG \(**Port Count**\)\.  
![\[LAG details screen\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/view_lag.png)

After you've created a LAG, you can associate or disassociate connections from it\. For more information, see [Associating a Connection with a LAG](associate-connection-with-lag.md) and [Disassociating a Connection From a LAG](disassociate-connection-from-lag.md)\.

**To create a LAG using the command line or API**
+ [create\-lag](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-lag.html) \(AWS CLI\)
+ [CreateLag](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateLag.html) \(AWS Direct Connect API\)

**To describe your LAGs using the command line or API**
+ [describe\-lags](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-lags.html) \(AWS CLI\)
+ [DescribeLags](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeLags.html) \(AWS Direct Connect API\)

**To download the LOA\-CFA using the command line or API**
+ [describe\-loa](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-loa.html) \(AWS CLI\)
+ [DescribeLoa](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeLoa.html) \(AWS Direct Connect API\)