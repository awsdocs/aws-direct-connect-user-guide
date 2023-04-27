# Disassociate a connection from a LAG<a name="disassociate-connection-from-lag"></a>

Convert a connection to standalone by disassociating it from a LAG\. You can't disassociate a connection if it causes the LAG to fall below its threshold for the minimum number of operational connections\.

Disassociating a connection from a LAG does not automatically disassociate any virtual interfaces\.

**Important**  
Your connection to AWS is broken off during disassociation\.

------
#### [ Console ]

**To disassociate a connection from a LAG**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the left pane, choose **LAGs**\.

1. Select the LAG, and then choose **View details**\.

1. Under **Connections**, select the connection from the list of available connections and choose **Disassociate**\.

1. In the confirmation dialog box, choose **Disassociate**\.

------
#### [ Command line ]

**To disassociate a connection using the command line or API**
+ [disassociate\-connection\-from\-lag](https://docs.aws.amazon.com/cli/latest/reference/directconnect/disassociate-connection-from-lag.html) \(AWS CLI\)
+ [DisassociateConnectionFromLag](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DisassociateConnectionFromLag.html) \(AWS Direct Connect API\)

------