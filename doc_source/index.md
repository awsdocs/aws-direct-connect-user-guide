# AWS Direct Connect User Guide

-----
*****Copyright &copy; 2019 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What is AWS Direct Connect?](Welcome.md)
   + [Accessing a Remote AWS Region](remote_regions.md)
   + [Routing Policies and BGP Communities](routing-and-bgp.md)
+ [Using the Direct Connect Resiliency Toolkit to Get Started](resilency_toolkit.md)
   + [Maximum Resiliency](maximum_resiliency.md)
   + [High Resiliency](high_resiliency.md)
   + [Development and Test](dev-test-resiliency.md)
   + [Classic](getting_started.md)
+ [AWS Direct Connect Connections](WorkingWithConnections.md)
   + [Creating a Connection](create-connection.md)
   + [Viewing Connection Details](viewdetails.md)
   + [Updating a Connection](updateconnection.md)
   + [Deleting Connections](deleteconnection.md)
   + [Accepting a Hosted Connection](accept-hosted-connection.md)
+ [Requesting Cross Connects at AWS Direct Connect Locations](Colocation.md)
+ [AWS Direct Connect Virtual Interfaces](WorkingWithVirtualInterfaces.md)
   + [Creating a Virtual Interface](create-vif.md)
   + [Viewing Virtual Interface Details](viewvifdetails.md)
   + [Adding or Deleting a BGP Peer](add-peer-to-vif.md)
   + [Setting Network MTU for Private Virtual Interfaces or Transit Virtual Interfaces](set-jumbo-frames-vif.md)
   + [Adding or Removing Virtual Interface Tags](modify-tags-vif.md)
   + [Deleting Virtual Interfaces](deletevif.md)
   + [Creating a Hosted Virtual Interface](createhostedvirtualinterface.md)
   + [Accepting a Hosted Virtual Interface](accepthostedvirtualinterface.md)
+ [Link Aggregation Groups](lags.md)
   + [Creating a LAG](create-lag.md)
   + [Updating a LAG](update-lag.md)
   + [Associating a Connection with a LAG](associate-connection-with-lag.md)
   + [Disassociating a Connection From a LAG](disassociate-connection-from-lag.md)
   + [Deleting LAGs](delete-lag.md)
+ [Working with Direct Connect Gateways](direct-connect-gateways.md)
   + [Direct Connect Gateways](direct-connect-gateways-intro.md)
   + [Virtual Private Gateway Associations](virtualgateways.md)
      + [Associating a Virtual Private Gateway Across Accounts](multi-account-associate-vgw.md)
   + [Transit Gateway Associations](direct-connect-transit-gateways.md)
      + [Associating a Transit Gateway Across Accounts](multi-account-associate-tgw.md)
   + [Allowed Prefixes Interactions](allowed-to-prefixes.md)
+ [Tagging AWS Direct Connect Resources](using-tags.md)
+ [Security in AWS Direct Connect](security.md)
   + [Data Protection in AWS Direct Connect](data-protection.md)
      + [Internetwork Traffic Privacy in AWS Direct Connect](encryption-at-rest.md)
      + [Encryption in AWS Direct Connect](encryption-in-transit.md)
   + [Identity and Access Management for AWS Direct Connect](security-iam.md)
      + [How AWS Direct Connect Works with IAM](security_iam_service-with-iam.md)
      + [AWS Direct Connect Identity-Based Policy Examples](security_iam_id-based-policy-examples.md)
         + [AWS Direct Connect Resource-Based Policy Examples](security_iam_resource-based-policy-examples.md)
      + [Troubleshooting AWS Direct Connect Identity and Access](security_iam_troubleshoot.md)
   + [Logging and Monitoring in AWS Direct Connect](dc-incident-response.md)
   + [Compliance Validation for AWS Direct Connect](DirectConnect-compliance.md)
   + [Resilience in AWS Direct Connect](disaster-recovery-resiliency.md)
   + [Infrastructure Security in AWS Direct Connect](infrastructure-security.md)
+ [Using the AWS CLI](using-cli.md)
+ [Logging AWS Direct Connect API Calls Using AWS CloudTrail](logging_dc_api_calls.md)
+ [Monitoring AWS Direct Connect](monitoring-overview.md)
   + [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)
+ [AWS Direct Connect Limits](limits.md)
+ [Troubleshooting AWS Direct Connect](Troubleshooting.md)
+ [Document History](AboutThisGuide.md)