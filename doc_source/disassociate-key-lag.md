# Remove the association between a MACsec secret key and a LAG<a name="disassociate-key-lag"></a>

You can remove the association between the LAG and the MACsec key\.

------
#### [ Console ]

**To remove an association between a LAG and a MACsec key**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG and choose **View details**\.

1. Select the MACsec secret to remove, and then choose **Disassociate key**\.

1. In the confirmation dialog box, enter **disassociate**, and then choose **Disassociate**\.

------
#### [ Command line ]

**To remove an association between a LAG and a MACsec key**
+ [disassociate\-mac\-sec\-key](https://docs.aws.amazon.com/cli/latest/reference/directconnect/disassociate-mac-sec-key.html) \(AWS CLI\)
+ [DisassociateMacSecKey](https://docs.aws.amazon.com/directconnect/latest/APIReference/API__DisassociateMacSecKey.html) \(AWS Direct Connect API\)

------