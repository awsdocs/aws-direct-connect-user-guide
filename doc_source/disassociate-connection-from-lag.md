# Disassociating a Connection From a LAG<a name="disassociate-connection-from-lag"></a>

You can disassociate a connection from a LAG to convert it to a standalone connection\. You cannot disassociate a connection if this will cause the LAG to fall below its threshold for minimum number of operational connections\.

Disassociating a connection from a LAG does not automatically disassociate any virtual interfaces\. You must associate the virtual interface with the connection separately\. For more information, see [Associating a Virtual Interface with a Connection or LAG](associate-vif.md)\.

**Important**  
Connectivity to AWS over the connection is interrupted during disassociation\.

**To disassociate a connection from a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **LAGs**, and select the LAG\.

1. Choose **Actions**, **Disassociate Connection**\.

1. Select the connection from the list of available connections\. 

1. Select the confirmation check box, and choose **Continue**\.

**To disassociate a connection using the command line or API**

+ [disassociate\-connection\-from\-lag](http://docs.aws.amazon.com/cli/latest/reference/directconnect/disassociate-connection-from-lag.html) \(AWS CLI\)

+ [DisassociateConnectionFromLag](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_DisassociateConnectionFromLag.html) \(AWS Direct Connect API\)