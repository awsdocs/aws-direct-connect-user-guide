# AWS Direct Connect User Guide

-----
*****Copyright &copy; 2020 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

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
   + [Accessing a remote AWS Region](remote_regions.md)
   + [Routing policies and BGP communities](routing-and-bgp.md)
+ [Using the Direct Connect Resiliency Toolkit to get started](resilency_toolkit.md)
   + [Maximum resiliency](maximum_resiliency.md)
   + [High resiliency](high_resiliency.md)
   + [Development and test](dev-test-resiliency.md)
   + [Classic](getting_started.md)
+ [AWS Direct Connect connections](WorkingWithConnections.md)
   + [Creating a connection](create-connection.md)
   + [Viewing connection details](viewdetails.md)
   + [Updating a connection](updateconnection.md)
   + [Deleting connections](deleteconnection.md)
   + [Accepting a hosted connection](accept-hosted-connection.md)
+ [Requesting cross connects at AWS Direct Connect locations](Colocation.md)
+ [AWS Direct Connect virtual interfaces](WorkingWithVirtualInterfaces.md)
   + [Creating a virtual interface](create-vif.md)
   + [Viewing virtual interface details](viewvifdetails.md)
   + [Adding or deleting a BGP peer](add-peer-to-vif.md)
   + [Setting network MTU for private virtual interfaces or transit virtual interfaces](set-jumbo-frames-vif.md)
   + [Adding or removing virtual interface tags](modify-tags-vif.md)
   + [Deleting virtual interfaces](deletevif.md)
   + [Creating a hosted virtual interface](createhostedvirtualinterface.md)
   + [Accepting a hosted virtual interface](accepthostedvirtualinterface.md)
   + [Migrating a virtual interface](migratevirtualinterface.md)
+ [Link aggregation groups](lags.md)
   + [Creating a LAG](create-lag.md)
   + [Updating a LAG](update-lag.md)
   + [Associating a connection with a LAG](associate-connection-with-lag.md)
   + [Disassociating a connection from a LAG](disassociate-connection-from-lag.md)
   + [Deleting LAGs](delete-lag.md)
+ [Working with Direct Connect gateways](direct-connect-gateways.md)
   + [Direct Connect gateways](direct-connect-gateways-intro.md)
   + [Virtual private gateway associations](virtualgateways.md)
      + [Associating a virtual private gateway across accounts](multi-account-associate-vgw.md)
   + [Transit gateway associations](direct-connect-transit-gateways.md)
      + [Associating a transit gateway across accounts](multi-account-associate-tgw.md)
   + [Allowed prefixes interactions](allowed-to-prefixes.md)
+ [Tagging AWS Direct Connect resources](using-tags.md)
+ [Security in AWS Direct Connect](security.md)
   + [Data protection in AWS Direct Connect](data-protection.md)
      + [Internetwork traffic privacy in AWS Direct Connect](encryption-at-rest.md)
      + [Encryption in AWS Direct Connect](encryption-in-transit.md)
   + [Identity and access management for AWS Direct Connect](security-iam.md)
      + [How AWS Direct Connect works with IAM](security_iam_service-with-iam.md)
      + [AWS Direct Connect identity-based policy examples](security_iam_id-based-policy-examples.md)
         + [AWS Direct Connect resource-based policy examples](security_iam_resource-based-policy-examples.md)
      + [Troubleshooting AWS Direct Connect identity and access](security_iam_troubleshoot.md)
   + [Logging and monitoring in AWS Direct Connect](dc-incident-response.md)
   + [Compliance validation for AWS Direct Connect](DirectConnect-compliance.md)
   + [Resilience in AWS Direct Connect](disaster-recovery-resiliency.md)
   + [Infrastructure security in AWS Direct Connect](infrastructure-security.md)
+ [Using the AWS CLI](using-cli.md)
+ [Logging AWS Direct Connect API calls using AWS CloudTrail](logging_dc_api_calls.md)
+ [Monitoring AWS Direct Connect resources](monitoring-overview.md)
   + [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)
+ [AWS Direct Connect quotas](limits.md)
+ [Troubleshooting AWS Direct Connect](Troubleshooting.md)
+ [Document history](AboutThisGuide.md)