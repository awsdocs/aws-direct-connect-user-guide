# AWS Direct Connect Failover Test<a name="resiliency_failover"></a>

The AWS Direct Connect Resiliency Toolkit resiliency models are designed to ensure that you have the appropriate number of virtual interface connections in multiple locations\. After you complete the wizard, use the AWS Direct Connect Resiliency Toolkit failover test to bring down the BGP peering session in order to verify that traffic routes to one of your redundant virtual interfaces, and meets your resiliency requirements\.

Use the test to make sure that traffic routes over redundant virtual interfaces when a virtual interface is out of service\. You start the test by selecting a virtual interface, BGP peering session, and how long to run the test\. AWS places the selected virtual interface BGP peering session in the down state\. When the interface is in this state, traffic should go over a redundant virtual interface\. If your configuration does not contain the appropriate redundant connections, the BGP peering session fails, and traffic does not get routed\. When the test completes, or you manually stop the test, AWS restores the BGP session\. After the test is complete, you can use the AWS Direct Connect Resiliency Toolkit to adjust your configuration\.

## Test History<a name="test_history"></a>

AWS deletes the test history after 365 days\. The test history includes the status for tests that were run on all BGP peers\. The history includes which BGP peering sessions were tested, the start and end times, and the test status, which can be any of the following values:
+ **In progress** \- The test is currently running\.
+ **Completed** \- The test ran for the time that you specified\.
+ **Cancelled** \- The test was cancelled before the specified time\.
+ **Failed** \- The test did not run for the time that you specified\. This can happen when there is an issue with the router\.

For more information, see [Viewing the virtual interface failover test history](#view_failover_test)\.

## Validation Permissions<a name="permissions"></a>

The only account that has permission to run the failover test is the account that owns the virtual interface\. The account owner receives an indication through AWS CloudTrail that a test ran on a virtual interface\.

## Starting the virtual interface failover test<a name="start_failover_test"></a>

You can start the virtual interface failover test using the AWS Direct Connect console, or the AWS CLI\.

**To start the virtual interface failover test from the AWS Direct Connect console**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. Choose **Virtual interfaces**\.

1. Select the virtual interfaces and then choose **Actions**, **Bring down BGP**\.

   You can run the test on a public, private, or transit virtual interface\.

1. In the **Start failure test** dialog box, do the following:

   1. For **Peerings to bring down to test**, choose which peering sessions to test, for example IPv4\.

   1. For **Test maximum time**, enter the number of minutes that the test will last\.

      The maximum value is 180 minutes \(3 hours\)\.

      The default value is 180 minutes \(3 hours\)\.

   1. For **To confirm test**, enter **Confirm**\.

   1. Choose **Confirm**\.

   The BGP peering session is placed in the DOWN state\. You can send traffic to verify that there are no outages\. If needed, you can stop the test immediately\.

**To start the virtual interface failover test using the AWS CLI**  
Use [StartBgpFailoverTest](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_StartBgpFailoverTest.html)\.

## Viewing the virtual interface failover test history<a name="view_failover_test"></a>

You can view the virtual interface failover test history using the AWS Direct Connect console, or the AWS CLI\.

**To view the virtual interface failover test history from the AWS Direct Connect console**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. Choose **Virtual interfaces**\.

1. Select the virtual interface and then choose **View details**\.

1. Choose **Test history**\.

   The console displays the virtual interface tests that you performed for the virtual interface\.

1. To view the details for a specific test, select the test id\.

**To view the virtual interface failover test history using the AWS CLI**  
Use [ListVirtualInterfaceTestHistory](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_ListVirtualInterfaceTestHistory.html)\.

## Stopping the virtual interface failover test<a name="stop_failover_test"></a>

You can stop the virtual interface failover test using the AWS Direct Connect console, or the AWS CLI\.

**To stop the virtual interface failover test from the AWS Direct Connect console**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. Choose **Virtual interfaces**\.

1. Select the virtual interface, and then choose **Actions**, **Cancel test**\.

1. Choose **Confirm**\.

AWS restores the BGP peering session\. The testing history displays "cancelled" for the test\. 

**To stop the virtual interface failover test using the AWS CLI**  
Use [StopBgpFailoverTest](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_StopBgpFailoverTest.html)\.