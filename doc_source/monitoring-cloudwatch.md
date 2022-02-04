# Monitoring with Amazon CloudWatch<a name="monitoring-cloudwatch"></a>

You can monitor physical AWS Direct Connect connections, and virtual interfaces, using CloudWatch\. CloudWatch collects raw data from AWS Direct Connect, and processes it into readable metrics\. By default, CloudWatch provides AWS Direct Connect metric data in 5\-minute intervals\.  

For detailed information about CloudWatch, see the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)\. You can also monitor your services CloudWatch to see what ones are using resources\. For more information, see [AWS Services That Publish CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/aws-services-cloudwatch-metrics.html)\.

**Topics**
+ [AWS Direct Connect metrics and dimensions](#metrics-dimensions)
+ [Viewing AWS Direct Connect CloudWatch metrics](#viewing-metrics)
+ [Creating CloudWatch alarms to monitor AWS Direct Connect connections](#creating-alarms)

## AWS Direct Connect metrics and dimensions<a name="metrics-dimensions"></a>

Metrics are available for AWS Direct Connect physical connections, and virtual interfaces\.

### AWS Direct Connect Connection metrics<a name="connection-metrics-dimensions"></a>

The following metrics are available from AWS Direct Connect dedicated connections\. 


| Metric | Description | 
| --- | --- | 
|  `ConnectionState`  |  The state of the connection\.1 indicates **up** and 0 indicates **down**\. This metric is available for dedicated and hosted connections\. Units: Boolean  | 
|  `ConnectionBpsEgress`  |  The bitrate for outbound data from the AWS side of the connection\. The number reported is the aggregate \(average\) over the specified time period \(5 minutes by default, 1 minute minimum\)\. You can change the default aggregate\. This metric might be unavailable for a new connection, or when a device reboots\. The metric starts when the connection is used to send or receive traffic\. Units: Bits per second  | 
|  `ConnectionBpsIngress`  |  The bitrate for inbound data to the AWS side of the connection\. This metric might be unavailable for a new connection, or when a device reboots\. The metric starts when the connection is used to send or receive traffic\. Units: Bits per second  | 
|  `ConnectionPpsEgress`  |  The packet rate for outbound data from the AWS side of the connection\. The number reported is the aggregate \(average\) over the specified time period \(5 minutes by default, 1 minute minimum\)\. You can change the default aggregate\. This metric might be unavailable for a new connection, or when a device reboots\. The metric starts when the connection is used to send or receive traffic\. Units: Packets per second  | 
|  `ConnectionPpsIngress`  |  The packet rate for inbound data to the AWS side of the connection\. The number reported is the aggregate \(average\) over the specified time period \(5 minutes by default, 1 minute minimum\)\. You can change the default aggregate\. This metric might be unavailable for a new connection, or when a device reboots\. The metric starts when the connection is used to send or receive traffic\. Units: Packets per second  | 
|  `ConnectionCRCErrorCount`  |  This count is no longer in use\. Use `ConnectionErrorCount` instead\.  | 
|  `ConnectionErrorCount`  |  The total error count for all types of MAC level errors on the AWS device\. The total includes cyclic redundancy check \(CRC\) errors\.  This metric is the error count that occurred since the last reported datapoint\. When there are errors on the interface, the metric reports non\-zero values\. To get the total count of all errors for the selected interval in CloudWatch, for example, 5 minutes, apply the"sum" statistic\. For more information about getting the sum statistic, see [Getting Statistics for a Metric](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/getting-metric-statistics.html) in the *Amazon CloudWatch User Guide*\.  The metric value is set to 0 when the errors on the interface stop\.  This metric replaces `ConnectionCRCErrorCount`, which is no longer in use\.  Units: Count  | 
| ConnectionLightLevelTx |  Indicates the health of the fiber connection for outbound \(egress\) traffic from the AWS side of the connection\. There are two dimensions for this metric\. For more information, see [AWS Direct Connect available dimensions](#metrics-available-dimensions)\. Units: dBm  | 
|  `ConnectionLightLevelRx`  |  Indicates the health of the fiber connection for inbound \(ingress\) traffic to the AWS side of the connection\. There are two dimensions for this metric\. For more information, see [AWS Direct Connect available dimensions](#metrics-available-dimensions)\. Units: dBm  | 
| ConnectionEncryptionState | Indicates the connection encryption status\. 1 indicates the connection encryption is `up`, and 0 indicates the connection encryption is `down`\. When this metric is applied to a LAG, 1 indicates that all connections in the LAG have encrption `up`\. 0 indicates at least one LAG connection encrption is `down`\.The MAC Security feature is in Beta release for AWS Direct Connect, and is subject to change\. | 

### AWS Direct Connect virtual interface metrics<a name="virtual-interfaces-metrics-dimensions"></a>

The following metrics are available from AWS Direct Connect virtual interfaces\. 


| Metric | Description | 
| --- | --- | 
|  `VirtualInterfaceBpsEgress`  |  The bitrate for outbound data from the AWS side of the virtual interface\. The number reported is the aggregate \(average\) over the specified time period \(5 minutes by default\)\.  Units: Bits per second  | 
|  `VirtualInterfaceBpsIngress`  |  The bitrate for inbound data to the AWS side of the virtual interface\. The number reported is the aggregate \(average\) over the specified time period \(5 minutes by default\)\.  Units: Bits per second  | 
|  `VirtualInterfacePpsEgress`  |  The packet rate for outbound data from the AWS side of the virtual interface\. The number reported is the aggregate \(average\) over the specified time period \(5 minutes by default\)\.  Units: Packets per second  | 
|  `VirtualInterfacePpsIngress`  |  The packet rate for inbound data to the AWS side of the virtual interface\. The number reported is the aggregate \(average\) over the specified time period \(5 minutes by default\)\.  Units: Packets per second  | 

### AWS Direct Connect available dimensions<a name="metrics-available-dimensions"></a>

You can filter the AWS Direct Connect data using the following dimensions\.


| Dimension | Description | 
| --- | --- | 
|  `ConnectionId`  |  This dimension is available on the metrics for AWS Direct Connect connection, and virtual interface\. This dimension filters the data by the connection\.  | 
| OpticalLaneNumber | This dimension filters the ConnectionLightLevelTx data and the ConnectionLightLevelRx data, and filters the data by the optical lane number of the AWS Direct Connect connection\. | 
| VirtualInterfaceId | This dimension is available on the metrics for AWS Direct Connect virtual interface, and filters the data by the virtual interface\. | 

## Viewing AWS Direct Connect CloudWatch metrics<a name="viewing-metrics"></a>

AWS Direct Connect sends the following metrics about your AWS Direct Connect connections at 30\-second intervals to Amazon CloudWatch\. Amazon CloudWatch then aggregates these data points to 1\-minute, or 5\-minute intervals\. You can use the following procedures to view the metrics for AWS Direct Connect connections\.

**To view metrics using the CloudWatch console**

Metrics are grouped first by the service namespace, and then by the various dimension combinations within each namespace\.

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Metrics**\.

1. For **All metrics**, choose the **DX** metric namespace\.

1. Choose **Connection Metrics**, and select the metric dimension to view the metrics \(for example, for the AWS Direct Connect connection\)\.

1. \(Optional for Connection metrics\) To return data for the selected metric in 1\-minute intervals, choose **Graphed metrics**, and select **1 Minute** from the **Period** list\.

**To view metrics using the AWS Direct Connect console**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Connections**\.

1. Select your connection\. The **Monitoring** tab displays the metrics for your connection\.

**To view metrics using the AWS CLI**  
At a command prompt, use the following command\.

```
aws cloudwatch list-metrics --namespace "AWS/DX"
```

## Creating CloudWatch alarms to monitor AWS Direct Connect connections<a name="creating-alarms"></a>

You can create a CloudWatch alarm that sends an Amazon SNS message when the alarm changes state\. An alarm watches a single metric over a time period that you specify\. It sends a notification to an Amazon SNS topic based on the value of the metric relative to a given threshold over a number of time periods\. 

For example, you can create an alarm that monitors the state of an AWS Direct Connect connection\. It sends a notification when the connection state is **down** for five consecutive 1\-minute periods\.

**To create an alarm for the connection state**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Alarms**\.

1. Choose **Create Alarm**\.

1. Choose the **DX Metrics** category\.

1. Select the AWS Direct Connect connection and choose the **ConnectionState** metric\. Choose **Next**\.

1. Configure the alarm as follows, and then choose **Create Alarm**:
   + For **Alarm Threshold**, enter a name and description for your alarm\. For **Whenever**, choose **<** and enter `1`\. Enter **5** for the consecutive periods\.
   + For **Actions**, select an existing notification list or choose **New list** to create a new one\.
   + For **Alarm Preview**, select a period of 1 minute\.

For more examples of creating alarms, see [Creating Amazon CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) in the *Amazon CloudWatch User Guide*\.