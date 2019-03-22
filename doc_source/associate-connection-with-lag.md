# Associating a Connection with a LAG<a name="associate-connection-with-lag"></a>

You can associate an existing connection with a LAG\. The connection can be standalone, or it can be part of another LAG\. The connection must be on the same AWS device and must use the same bandwidth as the LAG\. If the connection is already associated with another LAG, you cannot re\-associate it if removing the connection causes the original LAG to fall below its threshold for the minimum number of operational connections\.

Associating a connection to a LAG automatically re\-associates its virtual interfaces to the LAG\.

**Important**  
Connectivity to AWS over the connection is interrupted during association\.

**To associate a connection with a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG and choose **View details**\.

1. Under **Connections**, choose **Associate connection**\.

1. For **Connection**, choose the Direct Connect connection to use for the LAG\.

1. Choose **Associate Connection**\.

**To associate a connection using the command line or API**
+ [associate\-connection\-with\-lag](https://docs.aws.amazon.com/cli/latest/reference/directconnect/associate-connection-with-lag.html) \(AWS CLI\)
+ [AssociateConnectionWithLag](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AssociateConnectionWithLag.html) \(AWS Direct Connect API\)