# Adding or removing virtual interface tags<a name="modify-tags-vif"></a>

Tags provide a way to identify the virtual interface\. You can add or remove a tag if you are the account owner for the virtual interface\.

**To add or remove a virtual interface tag**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1.  Select the virtual interface and then choose **Edit**\.

1. Add or remove a tag\.

   \[Add a tag\] Choose **Add tag** and do the following:
   + For **Key**, enter the key name\.
   + For **Value**, enter the key value\.

   \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Edit virtual interface**\.

**To add a tag or remove a tag using the command line**
+ [tag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/tag-resource.html) \(AWS CLI\) 
+ [untag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/untag-resource.html) \(AWS CLI\) 