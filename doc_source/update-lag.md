# Updating a LAG<a name="update-lag"></a>

You can update a LAG to change its name, or to change the value for the minimum number of operational connections\., or to add a tag, or remove a tag\.

**Note**  
If you adjust the threshold value for the minimum number if operational connections, ensure that the new value does not cause the LAG to fall below the threshold and become non\-operational\.

**To update a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG and choose **Edit**\.

1. Modify the LAG

   \[Change the name\] For **LAG Name**, enter a new LAG name\.

   \[Adjust the minimum number of connections\] For Minimum Links, enter minimum number of operational connections\.

   \[Add a tag\] Choose **Add tag** and do the following:
   + For **Key**, enter the key name\.
   + For **Value**, enter the key value\.

   \[Remove a tag\] Beside the tag, choose **Remove tag**\.

1. Choose **Edit LAG**\.

**To update a LAG using the command line or API**
+ [update\-lag](https://docs.aws.amazon.com/cli/latest/reference/directconnect/update-lag.html) \(AWS CLI\)
+ [UpdateLag](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_UpdateLag.html) \(AWS Direct Connect API\)

**To add a tag or remove a tag using the command line**
+ [tag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/tag-resource.html) \(AWS CLI\) 
+ [untag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/untag-resource.html) \(AWS CLI\) 