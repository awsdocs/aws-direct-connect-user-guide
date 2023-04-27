# Associate a MACsec CKN/CAK with a LAG<a name="associate-key-lag"></a>

After you create the LAG that supports MACsec, you can associate a CKN/CAK with the connection\.

**Note**  
You cannot modify a MACsec secret key after you associate it with a LAG\. If you need to modify the key, disassociate the key from the connection, and then associate a new key with the connection\. For information about removing an association, see [Remove the association between a MACsec secret key and a LAG](disassociate-key-lag.md)\.

------
#### [ Console ]

**To associate a MACsec key with a LAG**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG and choose **View details**\.

1. Choose **Associate key**\.

1. Enter the MACsec key\.

   \[Use the CAK/CKN pair\] Choose **Key Pair**, and then do the following:
   + For **Connectivity Association Key \(CAK\)**, enter the CAK\.
   + For **Connectivity Association Key Name \(CKN\)**, enter the CKN\.

   \[Use the secret\] Choose **Existing Secret Manager secret**, and then for **Secret**, select the MACsec secret key\.

1. Choose **Associate key**\.

------
#### [ Command line ]

**To associate a MACsec key with a LAG**
+ [associate\-mac\-sec\-key](https://docs.aws.amazon.com/cli/latest/reference/directconnect/associate-mac-sec-key.html) \(AWS CLI\)
+ [AssociateMacSecKey](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AssociateMacSecKey.html) \(AWS Direct Connect API\)

------