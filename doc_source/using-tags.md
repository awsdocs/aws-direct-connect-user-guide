# Using Tags with AWS Direct Connect<a name="using-tags"></a>

You can optionally assign tags to your AWS Direct Connect resources to categorize or manage them\. A tag consists of a key and an optional value, both of which you define\. 

You can tag the following AWS Direct Connect resources\. 


| Resource | Amazon Resource Name \(ARN\) | 
| --- | --- | 
| Connections |  arn:aws:directconnect:region:account\-id:dxcon/connection\-id  | 
| Virtual interfaces |  arn:aws:directconnect:region:account\-id:dxvif/virtual\-interface\-id  | 
| Link aggregation group \(LAG\) |  arn:aws:directconnect:region:account\-id:dxlag/lag\-id  | 

For example, you have two AWS Direct Connect connections in a region, each in different locations\. Connection `dxcon-11aa22bb` is a connection serving production traffic, and is associated with virtual interface `dxvif-33cc44dd`\. Connection `dxcon-abcabcab` is a redundant \(backup\) connection, and is associated with virtual interface `dxvif-12312312`\. You might choose to tag your connections and virtual interfaces as follows, to help distinguish them:

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/using-tags.html)

## Tag Restrictions<a name="using-tags-restrictions"></a>

The following rules and restrictions apply to tags:

+ Maximum number of tags per resource: 50

+ Maximum key length: 128 Unicode characters

+ Maximum value length: 265 Unicode characters

+ Tag keys and values are case sensitive\.

+ The `aws:` prefix is reserved for AWS use — you can't create or delete tag keys or values with this prefix\. Tags with this prefix do not count against your tags per resource limit\.

+ Allowed characters are letters, spaces, and numbers representable in UTF\-8, plus the following special characters: \+ \- = \. \_ : / @

+ Cost allocation tags are not supported; therefore, tags that you apply to AWS Direct Connect resources cannot be used for cost allocation tracking\.

## Working with Tags<a name="working-with-tags"></a>

Currently, you can work with tags using the AWS Direct Connect API, the AWS CLI, the AWS Tools for Windows PowerShell, or an AWS SDK only\. To apply or remove tags, you must specify the Amazon Resource Name \(ARN\) for the resource\. For more information, see [Amazon Resource Names \(ARNs\) and AWS Service Namespaces](http://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) in the *Amazon Web Services General Reference*\.

**To add a tag using the AWS CLI**

Use the [tag\-resource](http://docs.aws.amazon.com/cli/latest/reference/directconnect/tag-resource.html) command:

```
aws directconnect tag-resource --resource-arn arn:aws:directconnect:region:account-id:resource-type/resource-id --tags "key=key,value=value"
```

**To describe your tags using the AWS CLI**

Use the [describe\-tags](http://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-tags.html) command:

```
aws directconnect describe-tags --resource-arns arn:aws:directconnect:region:account-id:resource-type/resource-id
```

**To delete a tag using the AWS CLI**

Use the [untag\-resource](http://docs.aws.amazon.com/cli/latest/reference/directconnect/untag-resource.html) command:

```
aws directconnect untag-resource --resource-arn arn:aws:directconnect:region:account-id:resource-type/resource-id --tag-keys key
```