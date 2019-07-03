# Control Access to AWS Direct Connect<a name="control-options"></a>

You can use features of AWS Identity and Access Management to specify which AWS Direct Connect actions, and resources a user under your AWS account can perform\. 

When you create an IAM policy, you can use tag condition keys to control access to do any of the following:
+  [Resource](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html#access_tags_control-resources) – Control access to AWS service resources based on the tags on those resources\. 
+ [Request](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html#access_tags_control-requests) – Control what tags can be passed in an IAM request\. 
+ [Tag Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html#access_tags_control-tag-keys) – Use the** aws:TagKeys** condition key to control whether specific tag keys can be used on a resource or in a request\. 