# Updating a LAG<a name="update-lag"></a>

You can update a LAG to change its name, or to change the value for the minimum number of operational connections\. 

**Note**  
If you adjust the threshold value for the minimum number if operational connections, ensure that the new value does not cause the LAG to fall below the threshold and become non\-operational\.

**To update a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG and choose **Actions**, **Update LAG**\.

1. For **LAG Name**, specify a new name for the LAG\. For **Minimum Links**, adjust the value for the minimum number of operational connections\.

1. Choose **Continue**\.

**To update a LAG using the command line or API**
+ [https://docs.aws.amazon.com/cli/latest/reference/directconnect/update-lag.html](https://docs.aws.amazon.com/cli/latest/reference/directconnect/update-lag.html) \(AWS CLI\)
+ [https://docs.aws.amazon.com/directconnect/latest/APIReference/API_UpdateLag.html](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_UpdateLag.html) \(AWS Direct Connect API\)