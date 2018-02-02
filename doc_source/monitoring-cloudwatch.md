# Monitoring with Amazon CloudWatch<a name="monitoring-cloudwatch"></a>

You can monitor physical AWS Direct Connect connections using CloudWatch, which collects and processes raw data from AWS Direct Connect into readable, near real\-time metrics\. By default, CloudWatch provides AWS Direct Connect metric data in 5\-minute intervals\. You can optionally view data in 1\-minute intervals\.

For more information about Amazon CloudWatch, see the *[Amazon CloudWatch User Guide](http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)*\.

**Note**  
If your connection is a hosted connection from an AWS Direct Connect partner, you cannot view CloudWatch metrics for the hosted connection\. 


+ [AWS Direct Connect Metrics and Dimensions](#metrics-dimensions)
+ [Creating CloudWatch Alarms to Monitor AWS Direct Connect Connections](#creating-alarms)

## AWS Direct Connect Metrics and Dimensions<a name="metrics-dimensions"></a>

AWS Direct Connect sends the following metrics about your AWS Direct Connect connections at 30\-second intervals to Amazon CloudWatch\. Amazon CloudWatch then aggregates these data points to 1\-minute or 5\-minute intervals\. You can use the following procedures to view the metrics for AWS Direct Connect connections\.

**To view metrics using the CloudWatch console**

Metrics are grouped first by the service namespace, and then by the various dimension combinations within each namespace\.

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Metrics**\.

1. Under **All metrics**, choose the **DX** metric namespace\.

1. Choose **Connection Metrics**, and select the metric dimension to view the metrics \(for example, for the AWS Direct Connect connection\)\.

1. \(Optional\) To return data for the selected metric in 1\-minute intervals, choose **Graphed metrics**, and select **1 Minute** from the **Period** list\.

**To view metrics using the AWS Direct Connect console**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Connections** and select your connection\.

1. The **Monitoring** tab displays the metrics for your connection\.

**To view metrics using the AWS CLI**

+ At a command prompt, use the following command:

  ```
  aws cloudwatch list-metrics --namespace "AWS/DX"
  ```

The following metrics are available from AWS Direct Connect\. Metrics are currently available for AWS Direct Connect physical connections only\.


| Metric | Description | 
| --- | --- | 
|  ConnectionState  |  The state of the connection\. 0 indicates DOWN and 1 indicates UP\. Units: Boolean  | 
|  ConnectionBpsEgress  |  The bit rate for outbound data from the AWS side of the connection\. The number reported is the aggregate over the specified time period \(5 minutes by default, 1 minute minimum\)\. Units: Bits per second  | 
|  ConnectionBpsIngress  |  The bit rate for inbound data to the AWS side of the connection\. The number reported is the aggregate over the specified time period \(5 minutes by default, 1 minute minimum\)\. Units: Bits per second  | 
|  ConnectionPpsEgress  | The packet rate for outbound data from the AWS side of the connection\. The number reported is the aggregate over the specified time period \(5 minutes by default, 1 minute minimum\)\. Units: Packets per second | 
|  ConnectionPpsIngress  | The packet rate for inbound data to the AWS side of the connection\. The number reported is the aggregate over the specified time period \(5 minutes by default, 1 minute minimum\)\. Units: Packets per second | 
|  ConnectionCRCErrorCount  |  The number of times cyclic redundancy check \(CRC\) errors are observed for the data received at the connection\. Units: Integer  | 
| ConnectionLightLevelTx |  Indicates the health of the fiber connection for egress \(outbound\) traffic from the AWS side of the connection\. This metric is available for connections with 10 Gbps port speeds only\. Units: dBm  | 
|  ConnectionLightLevelRx  |  Indicates the health of the fiber connection for ingress \(inbound\) traffic to the AWS side of the connection\. This metric is available for connections with 10 Gbps port speeds only\. Units: dBm  | 

You can filter the AWS Direct Connect data using the following dimensions\.


| Dimension | Description | 
| --- | --- | 
| `ConnectionId` |  This dimension filters the data by the AWS Direct Connect connection\.  | 

## Creating CloudWatch Alarms to Monitor AWS Direct Connect Connections<a name="creating-alarms"></a>

You can create a CloudWatch alarm that sends an Amazon SNS message when the alarm changes state\. An alarm watches a single metric over a time period that you specify, and sends a notification to an Amazon SNS topic based on the value of the metric relative to a given threshold over a number of time periods\. 

For example, you can create an alarm that monitors the state of an AWS Direct Connect connection and sends a notification when the connection state is DOWN for 5 consecutive 1\-minute periods\.

**To create an alarm for connection state**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Alarms**, **Create Alarm**\.

1. Choose **DX Metrics**\.

1. Select the AWS Direct Connect connection and choose the **ConnectionState** metric\. Choose **Next**\.

1. Configure the alarm as follows, and choose **Create Alarm** when you are done:

   + Under **Alarm Threshold**, enter a name and description for your alarm\. For **Whenever**, choose **<** and enter `1`\. Enter **5** for the consecutive periods\.

   + Under **Actions**, select an existing notification list or choose **New list** to create a new one\. 

   + Under **Alarm Preview**, select a period of 1 minute\.

For more examples of creating alarms, see [Creating Amazon CloudWatch Alarms](http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) in the *Amazon CloudWatch User Guide*\.