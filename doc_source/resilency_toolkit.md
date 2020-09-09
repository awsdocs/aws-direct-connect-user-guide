# Using the AWS Direct Connect Resiliency Toolkit to get started<a name="resilency_toolkit"></a>

AWS offers customers the ability to achieve highly resilient network connections between Amazon Virtual Private Cloud \(Amazon VPC\) and their on\-premises infrastructure\. The AWS Direct Connect Resiliency Toolkit provides a connection wizard with multiple resiliency models\. These models help you to determine, and then place an order for the number of dedicated connections to achieve your SLA objective\. You select a resiliency model, and then the AWS Direct Connect Resiliency Toolkit guides you through the dedicated connection ordering process\. The resiliency models are designed to ensure that you have the appropriate number of dedicated connections in multiple locations\. 

The AWS Direct Connect Resiliency Toolkit has the following benefits:
+ Provides guidance on how you determine and then order the appropriate redundant AWS Direct Connect dedicated connections\.
+ Ensures that the redundant dedicated connections have the same speed\.
+ Automatically configures the dedicated connection names\.
+ Automatically approves your dedicated connections when you have an existing AWS account and you select a known AWS Direct Connect Partner\. The Letter of Authority \(LOA\) is available for immediate download\.
+ Automatically creates a support ticket for the dedicated connection approval when you are a new AWS customer, or you select an unknown \(**Other**\) partner\.
+ Provides an order summary for your dedicated connections, with the SLA that you can achieve and the port\-hour cost for the ordered dedicated connections\.
+ Creates link aggregation groups \(LAGs\), and adds the appropriate number of dedicated connections to the LAGs when you choose a speed other than 1 Gbps or 10 Gbps\.
+ Provides a LAG summary with the dedicated connection SLA that you can achieve, and the total port\-hour cost for each ordered dedicated connection as part of the LAG\.
+ Prevents you from terminating the dedicated connections on the same AWS Direct Connect device\.
+ Provides a way for you to test your configuration for resiliency\. You work with AWS to bring down the BGP peering session in order to verify that traffic routes to one of your redundant virtual interfaces\. For more information, see [AWS Direct Connect Failover Test](resilency_failover.md)\.
+ Provides Amazon CloudWatch metrics for connections and virtual interfaces\. For more information, see [Monitoring AWS Direct Connect resources](monitoring-overview.md)\.

The following resiliency models are available in the AWS Direct Connect Resiliency Toolkit:
+ **Maximum Resiliency**: This model provides you a way to order dedicated connections to achieve an SLA of 99\.99%\. It requires you to meet all of the requirements for achieving the SLA that are specified in the [AWS Direct Connect Service Level Agreement](https://aws.amazon.com/directconnect/sla/)\. 
+ **High Resiliency**: This model provides you a way to order dedicated connections to achieve an SLA of 99\.9%\. It requires you to meet all of the requirements for achieving the SLA that are specified in the [AWS Direct Connect Service Level Agreement](https://aws.amazon.com/directconnect/sla/)\. 
+ **Development and Test**: This model provides you a way to achieve development and test resiliency for non\-critical workloads, by using separate connections that terminate on separate devices in one location\.
+ **Classic**\. This model is intended for users that have existing connections and want to add additional connections\. This model does not provide an SLA\.

The best practice is to use the **Connection wizard** in the AWS Direct Connect Resiliency Toolkit to order the dedicated connections to achieve your SLA objective\.

After you select the resiliency model, the AWS Direct Connect Resiliency Toolkit steps you through the following procedures:
+ Selecting the number of dedicated connections
+ Selecting the connection capacity, and the dedicated connection location
+ Ordering the dedicated connections
+ Verifying that the dedicated connections are ready to use
+ Downloading your Letter of Authority \(LOA\-CFA\) for each dedicated connection
+ Verifying that your configuration meets your resiliency requirements

## Prerequisites<a name="prerequisites"></a>

AWS Direct Connect supports the following port speeds over single\-mode fiber: 1 Gbps: 1000BASE\-LX \(1310 nm\) and 10 Gbps: 10GBASE\-LR \(1310 nm\)\.

You can set up an AWS Direct Connect connection in one of the following ways:


| Model | Bandwidth | Method | 
| --- | --- | --- | 
| Dedicated connection | 1 Gbps, 10 Gbps |  Work with an AWS Direct Connect Partner or a network provider to connect a router from your data center, office, or colocation environment to an AWS Direct Connect location\. The network provider does not have to be an [AWS Direct Connect Partner](https://aws.amazon.com/directconnect/partners) to connect you to a dedicated connection\. AWS Direct Connect dedicated connections support these port speeds over single\-mode fiber: 1 Gbps: 1000BASE\-LX \(1310 nm\) and 10 Gbps: 10GBASE\-LR \(1310 nm\)  | 
| Hosted connection | 50 Mbps, 100 Mbps, 200 Mbps, 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, and 10 Gbps |  Work with a partner in the [AWS Direct Connect Partner Program](https://aws.amazon.com/directconnect/partners) to connect a router from your data center, office, or colocation environment to an AWS Direct Connect location\. Only certain partners provide higher capacity connections\.   | 

For connections to AWS Direct Connect with bandwidths of 1 Gbps or higher, ensure that your network meets the following requirements:
+ Your network must use single\-mode fiber with a 1000BASE\-LX \(1310 nm\) transceiver for 1 gigabit Ethernet or a 10GBASE\-LR \(1310 nm\) transceiver for 10 gigabit Ethernet\.
+ Auto\-negotiation for the port must be disabled\. Port speed and full\-duplex mode must be configured manually\.
+ 802\.1Q VLAN encapsulation must be supported across the entire connection, including intermediate devices\.
+ Your device must support Border Gateway Protocol \(BGP\) and BGP MD5 authentication\.
+ \(Optional\) You can configure Bidirectional Forwarding Detection \(BFD\) on your network\. Asynchronous BFD is automatically enabled for AWS Direct Connect virtual interfaces, but does not take effect until you configure it on your router\. Refer to [How do I enable BFD for my DX connection?](https://aws.amazon.com/premiumsupport/knowledge-center/enable-bfd-direct-connect/) to learn more.

Make sure you have the following information before you begin your configuration:
+ The resiliency model that you want to use\.
+ The speed, location, and partner for all of your connections\.

  You only need the speed for one connection\. 
