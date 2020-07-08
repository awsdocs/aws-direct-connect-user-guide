# Tagging AWS Direct Connect resources<a name="using-tags"></a>

A tag is a label that a resource owner assigns to their AWS Direct Connect resources\. Each tag consists of a key and an optional value, both of which you define\. Tags enable the resource owner to categorize your AWS Direct Connect resources in different ways, for example, by purpose, or environment\. This is useful when you have many resources of the same type—you can quickly identify a specific resource based on the tags you've assigned to it\. 

For example, you have two AWS Direct Connect connections in a Region, each in different locations\. Connection `dxcon-11aa22bb` is a connection serving production traffic, and is associated with virtual interface `dxvif-33cc44dd`\. Connection `dxcon-abcabcab` is a redundant \(backup\) connection, and is associated with virtual interface `dxvif-12312312`\. You might choose to tag your connections and virtual interfaces as follows, to help distinguish them:

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/using-tags.html)

We recommend that you devise a set of tag keys that meets your needs for each resource type\. Using a consistent set of tag keys makes it easier for you to manage your resources\. Tags don't have any semantic meaning to AWS Direct Connect and are interpreted strictly as a string of characters\. Also, tags are not automatically assigned to your resources\. You can edit tag keys and values, and you can remove tags from a resource at any time\. You can set the value of a tag to an empty string, but you can't set the value of a tag to null\. If you add a tag that has the same key as an existing tag on that resource, the new value overwrites the old value\. If you delete a resource, any tags for the resource are also deleted\. 

You can tag the following AWS Direct Connect resources using the AWS Direct Connect console, the AWS Direct Connect API, the AWS CLI, the AWS Tools for Windows PowerShell, or an AWS SDK\. When you use these tools to manage tags, you must specify the Amazon Resource Name \(ARN\) for the resource\. For more information about ARNs, see [Amazon Resource Names \(ARNs\) and AWS Service Namespaces](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) in the *Amazon Web Services General Reference*\.


| Resource | Supports tags | Supports tags on creation | Supports tags controlling access and resource allocation | Supports cost allocation | 
| --- | --- | --- | --- | --- | 
| Connections |  Yes | Yes | Yes | Yes | 
| Virtual interfaces |  Yes | Yes | Yes | No | 
| Link aggregation groups \(LAG\) |  Yes | Yes | Yes | Yes | 
| Interconnects | Yes | Yes | Yes | Yes | 
| Direct Connect gateways | No | No | No | No | 

## Tag restrictions<a name="using-tags-restrictions"></a>

The following rules and restrictions apply to tags:
+ Maximum number of tags per resource: 50
+ Maximum key length: 128 Unicode characters
+ Maximum value length: 265 Unicode characters
+ Tag keys and values are case\-sensitive\.
+ The `aws:` prefix is reserved for AWS use\. You can’t edit or delete a tag’s key or value when the tag has a tag key with the `aws:` prefix\. Tags with a tag key with the `aws:` prefix do not count against your tags per resource limit\.
+ Allowed characters are letters, spaces, and numbers representable in UTF\-8, plus the following special characters: \+ \- = \. \_ : / @
+ Only the resource owner can add or remove tags\. For example, if there is a hosted connection, the partner will not be able to add, remove, or view the tags\. 
+ Cost allocation tags are only supported for connections, interconnects, and LAGs\. For information about how to use tags with cost management, see [Using Cost Allocation Tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the* AWS Billing and Cost Management User Guide*\.

## Working with tags using the CLI or API<a name="working-with-tags"></a>

Use the following to add, update, list, and delete the tags for your resources\.


| Task | API | CLI | 
| --- | --- | --- | 
| Add or overwrite one or more tags\. |  [TagResource](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_TagResource.html) | [tag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/tag-resource.html) | 
| Delete one or more tags\. |  [UntagResource](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_UntagResource.html) | [untag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/untag-resource.html) | 
| Describe one or more tags\. | [DescribeTags](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeTags.html) | [describe\-tags](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-tags.html) | 

### Examples<a name="working-with-tags-examples"></a>

Use the [tag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/tag-resource.html) command to tag the Connection `dxcon-11aa22bb`\.

```
aws directconnect tag-resource --resource-arn arn:aws:directconnect:us-east-1:123456789012:dxcon/dxcon-11aa22bb --tags "key=Purpose,value=Production"
```

Use the [describe\-tags](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-tags.html) command to describe the Connection `dxcon-11aa22bb` tags\.

```
aws directconnect describe-tags --resource-arn arn:aws:directconnect:us-east-1:123456789012:dxcon/dxcon-11aa22bb
```

Use the [untag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/untag-resource.html) command to remove a tag from Connection `dxcon-11aa22bb`\.

```
aws directconnect untag-resource --resource-arn arn:aws:directconnect:us-east-1:123456789012:dxcon/dxcon-11aa22bb --tag-keys Purpose
```
