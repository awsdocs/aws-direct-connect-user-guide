# Disassociating a Connection From a LAG<a name="disassociate-connection-from-lag"></a>

Convert a connection to standalone by disassociating it from a LAG\. You can't disassociate a connection if it causes the LAG to fall below its threshold for the minimum number of operational connections\.

Disassociating a connection from a LAG does not automatically disassociate any virtual interfaces\.

**Important**  
Your connection to AWS is broken off during disassociation\.

**To disassociate a connection from a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the left pane, choose **LAGs**\.

1. Select the LAG and choose **View details**\.

1. Under **Connections**, select the connection from the list of available connections and choose **Disassociate**\.

1. In the confirmation dialog box choose **Disassociate**\.

**To disassociate a connection using the command line or API**
+ [disassociate\-connection\-from\-lag](https://docs.aws.amazon.com/cli/latest/reference/directconnect/disassociate-connection-from-lag.html) \(AWS CLI\)
+ [DisassociateConnectionFromLag](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DisassociateConnectionFromLag.html) \(AWS Direct Connect API\)