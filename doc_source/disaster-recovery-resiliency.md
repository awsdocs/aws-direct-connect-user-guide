# Resilience in AWS Direct Connect<a name="disaster-recovery-resiliency"></a>

The AWS global infrastructure is built around AWS Regions and Availability Zones\. AWS Regions provide multiple physically separated and isolated Availability Zones, which are connected with low\-latency, high\-throughput, and highly redundant networking\. With Availability Zones, you can design and operate applications and databases that automatically fail over between Availability Zones without interruption\. Availability Zones are more highly available, fault tolerant, and scalable than traditional single or multiple data center infrastructures\. 

For more information about AWS Regions and Availability Zones, see [AWS Global Infrastructure](http://aws.amazon.com/about-aws/global-infrastructure/)\.

In addition to the AWS global infrastructure, AWS Direct Connect offers several features to help support your data resiliency and backup needs\.

## Failover<a name="failover"></a>

The AWS Direct Connect Resiliency Toolkit provides a connection wizard with multiple resiliency models that helps you order dedicated connections to achieve your SLA objective\. You select a resiliency model, and then the AWS Direct Connect Resiliency Toolkit guides you through the dedicated connection ordering process\. The resiliency models are designed to ensure that you have the appropriate number of dedicated connections in multiple locations\. 
+ **Maximum Resiliency**: You can achieve maximum resiliency for critical workloads by using separate connections that terminate on separate devices in more than one location\. This model provides resiliency against device, connectivity, and complete location failures\.
+ **High Resiliency**: You can achieve high resiliency for critical workloads by using two single connections to multiple locations\. This model provides resiliency against connectivity failures caused by a fiber cut or a device failure\. It also helps prevent a complete location failure\.
+ **Development and Test**: You can achieve development and test resiliency for non\-critical workloads by using separate connections that terminate on separate devices in one location\. This model provides resiliency against device failure, but does not provide resiliency against location failure\.

For more information, see [Using the AWS Direct Connect Resiliency Toolkit to get started](resiliency_toolkit.md)\.

For information about how to use VPN with AWS Direct Connect, see [AWS Direct Connect Plus VPN](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect-plus-vpn-network-to-amazon.html)\.