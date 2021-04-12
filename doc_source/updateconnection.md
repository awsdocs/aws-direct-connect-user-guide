# Update a connection<a name="updateconnection"></a>

You can update the following connection attributes:
+ The name of the connection\.
+ The connection's MACsec encryption mode\.

  MACsec is only available on dedicated connections\.

  The valid values are:
  + `should_encrypt`
  + `must_encrypt`

    When you set the encryption mode to this value, the connection goes down when the encryption is down\.
  + `no_encrypt`

------
#### [ Console ]

**To update a connection**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Connections**\.

1. Select the connection, and then choose **Edit**\.

1. Modify the connection:

   \[Change the name\] For **Name**, enter a new connection name\.

   \[Add a tag\] Choose **Add tag** and do the following:
   + For **Key**, enter the key name\.
   + For **Value**, enter the key value\.

   \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Edit connection**\.

------
#### [ Command line ]

**To add a tag or remove a tag using the command line**
+ [tag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/tag-resource.html) \(AWS CLI\) 
+ [untag\-resource](https://docs.aws.amazon.com/cli/latest/reference/directconnect/untag-resource.html) \(AWS CLI\) 

**To update a connection using the command line or API**
+ [update\-connection](https://docs.aws.amazon.com/cli/latest/reference/directconnect/update-connection.html) \(AWS CLI\)
+ [UpdateConnection](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_UpdateConnection.html) \(AWS Direct Connect API\)

------