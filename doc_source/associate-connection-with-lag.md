# Associating a Connection with a LAG<a name="associate-connection-with-lag"></a>

You can associate an existing connection with a LAG\. The connection can be standalone, or it can be part of another LAG\. The connection must be on the same AWS device and must use the same bandwidth as the LAG\. If the connection is already associated with another LAG, you cannot re\-associate it if removing the connection causes the original LAG to fall below its threshold for minimum number of operational connections\.

Associating a connection to a LAG automatically re\-associates its virtual interfaces to the LAG\.

**Important**  
Connectivity to AWS over the connection is interrupted during association\.

**To associate a connection with a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG and choose **Actions**, **Associate Connection**\.

1. Select the connection from the list of available connections\.

1. Select the confirmation check box and choose **Continue**\.

**To associate a connection using the command line or API**
+ [associate\-connection\-with\-lag](https://docs.aws.amazon.com/cli/latest/reference/directconnect/associate-connection-with-lag.html) \(AWS CLI\)
+ [AssociateConnectionWithLag](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AssociateConnectionWithLag.html) \(AWS Direct Connect API\)