# Disassociating a Connection From a LAG<a name="disassociate-connection-from-lag"></a>

Convert a connection to standalone by disassociating it from a LAG\. You can't disassociate a connection if it causes the LAG to fall below its threshold for the minimum number of operational connections\.

Disassociating a connection from a LAG does not automatically disassociate any virtual interfaces\. You must associate the virtual interface with the connection separately\. For more information, see [Associating a Virtual Interface with a Connection or LAG](associate-vif.md)\.

**Important**  
Your connection to AWS is broken off during disassociation\.

**To disassociate a connection from a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the left pane, choose **LAGs**\.

1. Select the LAG and choose **Actions**, **Disassociate Connection**\.

1. Select the connection from the list of available connections\.

1. Confirm and choose **Continue**\.

**To disassociate a connection using the command line or API**
+ [https://docs.aws.amazon.com/cli/latest/reference/directconnect/disassociate-connection-from-lag.html](https://docs.aws.amazon.com/cli/latest/reference/directconnect/disassociate-connection-from-lag.html) \(AWS CLI\)
+ [https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DisassociateConnectionFromLag.html](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DisassociateConnectionFromLag.html) \(AWS Direct Connect API\)