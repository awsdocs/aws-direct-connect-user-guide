# Monitoring AWS Direct Connect<a name="monitoring-overview"></a>

Monitoring is an important part of maintaining the reliability, availability, and performance of your AWS Direct Connect resources\. You should collect monitoring data from all of the parts of your AWS solution so that you can more easily debug a multi\-point failure if one occurs\. Before you start monitoring AWS Direct Connect; however, you should create a monitoring plan that includes answers to the following questions:
+ What are your monitoring goals?
+ What resources should be monitored?
+ How often should you monitor these resources?
+ What monitoring tools can you use?
+ Who performs the monitoring tasks?
+ Who should be notified when something goes wrong?

The next step is to establish a baseline for normal AWS Direct Connect performance in your environment, by measuring performance at various times and under different load conditions\. As you monitor AWS Direct Connect, store historical monitoring data\. That way, you can compare it with current performance data, identify normal performance patterns and performance anomalies, and devise methods to address issues\.

To establish a baseline, you should monitor the usage, state, and health of your physical AWS Direct Connect connections\.

**Topics**
+ [Monitoring Tools](#monitoring-automated-manual)
+ [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)

## Monitoring Tools<a name="monitoring-automated-manual"></a>

AWS provides various tools that you can use to monitor an AWS Direct Connect connection\. You can configure some of these tools to do the monitoring for you, while some of the tools require manual intervention\. We recommend that you automate monitoring tasks as much as possible\.

### Automated Monitoring Tools<a name="monitoring-automated_tools"></a>

You can use the following automated monitoring tools to watch AWS Direct Connect and report when something is wrong:
+ **Amazon CloudWatch Alarms** – Watch a single metric over a time period that you specify\. Perform one or more actions based on the value of the metric relative to a given threshold over a number of time periods\. The action is a notification sent to an Amazon SNS topic\. CloudWatch alarms do not invoke actions simply because they are in a particular state; the state must have changed and been maintained for a specified number of periods\. For more information, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\.
+ **AWS CloudTrail Log Monitoring** – Share log files between accounts and monitor CloudTrail log files in real time by sending them to CloudWatch Logs\. You can also write log processing applications in Java and validate that your log files have not changed after delivery by CloudTrail\. For more information, see [Logging AWS Direct Connect API Calls Using AWS CloudTrail](logging_dc_api_calls.md) and [Working with CloudTrail Log Files](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-working-with-log-files.html) in the *AWS CloudTrail User Guide*\.

### Manual Monitoring Tools<a name="monitoring-manual-tools"></a>

Another important part of monitoring an AWS Direct Connect connection involves manually monitoring those items that the CloudWatch alarms don't cover\. The AWS Direct Connect and CloudWatch console dashboards provide an at\-a\-glance view of the state of your AWS environment\. 
+ The AWS Direct Connect console shows:
  + Connection status \(see the **State** column\)
  + Virtual interface status \(see the **State** column\)
+ The CloudWatch home page shows:
  + Current alarms and status
  + Graphs of alarms and resources
  + Service health status

  In addition, you can use CloudWatch to do the following: 
  + Create [customized dashboards](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/CloudWatch_Dashboards.html) to monitor the services you care about\.
  + Graph metric data to troubleshoot issues and discover trends\.
  + Search and browse all your AWS resource metrics\.
  + Create and edit alarms to be notified of problems\.