# Logging AWS Direct Connect API Calls in AWS CloudTrail<a name="logging_dc_api_calls"></a>

AWS Direct Connect is integrated with AWS CloudTrail, a service that captures API calls made by or on behalf of your AWS account\. This information is collected and written to log files that are stored in an Amazon Simple Storage Service \(S3\) bucket that you specify\. API calls are logged when you use the AWS Direct Connect API, the AWS Direct Connect console, a back\-end console, or the AWS CLI\. Using the information collected by CloudTrail, you can determine what request was made to AWS Direct Connect, the source IP address the request was made from, who made the request, when it was made, and so on\. 

To learn more about CloudTrail, including how to configure and enable it, see the [AWS CloudTrail User Guide](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\. 


+ [AWS Direct Connect Information in CloudTrail](#dc_info_in_ct)
+ [Understanding AWS Direct Connect Log File Entries](#understanding_dc_log_file_entries)

## AWS Direct Connect Information in CloudTrail<a name="dc_info_in_ct"></a>

If CloudTrail logging is turned on, calls made to all AWS Direct Connect actions are captured in log files\. All of the AWS Direct Connect actions are documented in the [AWS Direct Connect API Reference](http://docs.aws.amazon.com/directconnect/latest/APIReference/)\. For example, calls to the **CreateConnection**, **CreatePrivateVirtualInterface**, and **DescribeConnections** actions generate entries in CloudTrail log files\.

Every log entry contains information about who generated the request\. For example, if a request is made to create a new connection to AWS Direct Connect \(**CreateConnection**\), CloudTrail logs the user identity of the person or service that made the request\. The user identity information helps you determine whether the request was made with root credentials or AWS Identity and Access Management \(IAM\) user credentials, with temporary security credentials for a role or federated user, or by another service in AWS\. For more information about CloudTrail fields, see [CloudTrail Event Reference](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/eventreference.html) in the AWS CloudTrail User Guide\. 

You can store your log files in your bucket for as long as you want, but you can also define Amazon S3 lifecycle rules to archive or delete log files automatically\. By default, your log files are encrypted by using Amazon S3 server\-side encryption \(SSE\)\. 

## Understanding AWS Direct Connect Log File Entries<a name="understanding_dc_log_file_entries"></a>

CloudTrail log files can contain one or more log entries composed of multiple JSON\-formatted events\. A log entry represents a single request from any source and includes information about the requested action, any input parameters, the date and time of the action, and so on\. The log entries do not appear in any particular order\. That is, they do not represent an ordered stack trace of the public API calls\. 

The following log file record shows that a user called the **CreateConnection** action\.

```
{
    "Records": [{
        "eventVersion": "1.0",
        "userIdentity": {
            "type": "IAMUser",
            "principalId": "EX_PRINCIPAL_ID",
            "arn": "arn:aws:iam::123456789012:user/Alice",
            "accountId": "123456789012",
            "accessKeyId": "EXAMPLE_KEY_ID",
            "userName": "Alice",
            "sessionContext": {
                "attributes": {
                    "mfaAuthenticated": "false",
                    "creationDate": "2014-04-04T12:23:05Z"
                }
            }
        },
        "eventTime": "2014-04-04T17:28:16Z",
        "eventSource": "directconnect.amazonaws.com",
        "eventName": "CreateConnection",
        "awsRegion": "us-west-2",
        "sourceIPAddress": "127.0.0.1",
        "userAgent": "Coral/Jakarta",
        "requestParameters": {
            "location": "EqSE2",
            "connectionName": "MyExampleConnection",
            "bandwidth": "1Gbps"
        },
        "responseElements": {
            "location": "EqSE2",
            "region": "us-west-2",
            "connectionState": "requested",
            "bandwidth": "1Gbps",
            "ownerAccount": "123456789012",
            "connectionId": "dxcon-fhajolyy",
            "connectionName": "MyExampleConnection"
        }
    },
    ...additional entries
  ]
}
```

The following log file record shows that a user called the **CreatePrivateVirtualInterface** action\.

```
{
    "Records": [
    {
        "eventVersion": "1.0",
        "userIdentity": {
            "type": "IAMUser",
            "principalId": "EX_PRINCIPAL_ID",
            "arn": "arn:aws:iam::123456789012:user/Alice",
            "accountId": "123456789012",
            "accessKeyId": "EXAMPLE_KEY_ID",
            "userName": "Alice",
            "sessionContext": {
                "attributes": {
                    "mfaAuthenticated": "false",
                    "creationDate": "2014-04-04T12:23:05Z"
                }
            }
        },
        "eventTime": "2014-04-04T17:39:55Z",
        "eventSource": "directconnect.amazonaws.com",
        "eventName": "CreatePrivateVirtualInterface",
        "awsRegion": "us-west-2",
        "sourceIPAddress": "127.0.0.1",
        "userAgent": "Coral/Jakarta",
        "requestParameters": {
            "connectionId": "dxcon-fhajolyy",
            "newPrivateVirtualInterface": {
                "virtualInterfaceName": "MyVirtualInterface",
                "customerAddress": "[PROTECTED]",
                "authKey": "[PROTECTED]",
                "asn": -1,
                "virtualGatewayId": "vgw-bb09d4a5",
                "amazonAddress": "[PROTECTED]",
                "vlan": 123
            }
        },
        "responseElements": {
            "virtualInterfaceId": "dxvif-fgq61m6w",
            "authKey": "[PROTECTED]",
            "virtualGatewayId": "vgw-bb09d4a5",
            "customerRouterConfig": "[PROTECTED]",
            "virtualInterfaceType": "private",
            "asn": -1,
            "routeFilterPrefixes": [],
            "virtualInterfaceName": "MyVirtualInterface",
            "virtualInterfaceState": "pending",
            "customerAddress": "[PROTECTED]",
            "vlan": 123,
            "ownerAccount": "123456789012",
            "amazonAddress": "[PROTECTED]",
            "connectionId": "dxcon-fhajolyy",
            "location": "EqSE2"
        }
    },
    ...additional entries
  ]
}
```

The following log file record shows that a user called the **DescribeConnections** action\.

```
{
    "Records": [
    {
        "eventVersion": "1.0",
        "userIdentity": {
            "type": "IAMUser",
            "principalId": "EX_PRINCIPAL_ID",
            "arn": "arn:aws:iam::123456789012:user/Alice",
            "accountId": "123456789012",
            "accessKeyId": "EXAMPLE_KEY_ID",
            "userName": "Alice",
            "sessionContext": {
                "attributes": {
                    "mfaAuthenticated": "false",
                    "creationDate": "2014-04-04T12:23:05Z"
                }
            }
        },
        "eventTime": "2014-04-04T17:27:28Z",
        "eventSource": "directconnect.amazonaws.com",
        "eventName": "DescribeConnections",
        "awsRegion": "us-west-2",
        "sourceIPAddress": "127.0.0.1",
        "userAgent": "Coral/Jakarta",
        "requestParameters": null,
        "responseElements": null
    },
    ...additional entries
  ]
}
```

The following log file record shows that a user called the **DescribeVirtualInterfaces** action\.

```
{
    "Records": [
    {
        "eventVersion": "1.0",
        "userIdentity": {
            "type": "IAMUser",
            "principalId": "EX_PRINCIPAL_ID",
            "arn": "arn:aws:iam::123456789012:user/Alice",
            "accountId": "123456789012",
            "accessKeyId": "EXAMPLE_KEY_ID",
            "userName": "Alice",
            "sessionContext": {
                "attributes": {
                    "mfaAuthenticated": "false",
                    "creationDate": "2014-04-04T12:23:05Z"
                }
            }
        },
        "eventTime": "2014-04-04T17:37:53Z",
        "eventSource": "directconnect.amazonaws.com",
        "eventName": "DescribeVirtualInterfaces",
        "awsRegion": "us-west-2",
        "sourceIPAddress": "127.0.0.1",
        "userAgent": "Coral/Jakarta",
        "requestParameters": {
            "connectionId": "dxcon-fhajolyy"
        },
        "responseElements": null
    },
    ...additional entries
  ]
}
```