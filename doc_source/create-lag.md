# Creating a LAG<a name="create-lag"></a>

You can create a LAG by provisioning new connections, or aggregating existing connections\.

You cannot create a LAG with new connections if this results in you exceeding the overall connections limit for the Region\.

To create a LAG from existing connections, the connections must be on the same AWS device \(terminate at the same AWS Direct Connect endpoint\)\. They must also use the same bandwidth\. You cannot migrate a connection from an existing LAG if removing the connection causes the original LAG to fall below its setting for the minimum number of operational connections\.

**Important**  
For existing connections, connectivity to AWS is interrupted during the creation of the LAG\.

**To create a LAG with new connections**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **LAGs**\.

1. Choose **Create LAG**\.

1. Under** Lag creation type**, choose **Request new connections**, and provide the following information:
   + **LAG name**: A name for the LAG\.
   + **Location**: The location for the LAG\.
   + **Port speed**: The port speed for the connections\.
   + **Number of new connections**: The number of new connections to create\.

1. \(Optional\) Add or remove a tag\.

   \[Add a tag\] Choose **Add tag** and do the following:
   + For **Key**, enter the key name\.
   + For **Value**, enter the key value\.

   \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create LAG**\.

**To create a LAG from existing connections**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **LAGs**\.

1. Choose **Create LAG**\.

1. Under** Lag creation type**, choose **Use existing connections**, and provide the following information:
   + **LAG name**: A name for the LAG\.
   + **Connection**: The Direct Connect connection to use for the LAG\.
   + **Minimum links**: The minimum number of connections that must be operational for the LAG itself to be operational\. If you do not specify a value, we assign a default value of 0\.

1. \(Optional\) Add or remove a tag\.

   \[Add a tag\] Choose **Add tag** and do the following:
   + For **Key**, enter the key name\.
   + For **Value**, enter the key value\.

   \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create LAG**\.

After you've created a LAG, you can view its details in the AWS Direct Connect console\.

**To view information about your LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG and choose **View details**\.

1. You can view information about the LAG, including its ID, the AWS Direct Connect endpoint on which the connections terminate\.

After you've created a LAG, you can associate or disassociate connections from it\. For more information, see [Associating a connection with a LAG](associate-connection-with-lag.md) and [Disassociating a connection from a LAG](disassociate-connection-from-lag.md)\.

**To create a LAG using the command line or API**
+ [create\-lag](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-lag.html) \(AWS CLI\)
+ [CreateLag](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateLag.html) \(AWS Direct Connect API\)

**To describe your LAGs using the command line or API**
+ [describe\-lags](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-lags.html) \(AWS CLI\)
+ [DescribeLags](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeLags.html) \(AWS Direct Connect API\)

**To download the LOA\-CFA using the command line or API**
+ [describe\-loa](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-loa.html) \(AWS CLI\)
+ [DescribeLoa](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeLoa.html) \(AWS Direct Connect API\)