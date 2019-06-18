# AWS Direct Connect Limits<a name="limits"></a>

The following table lists the limits related to AWS Direct Connect\. Unless indicated otherwise, you can request an increase for any of these limits using the [AWS Direct Connect Limits form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-direct-connect)\.


| Component | Limit | Comments | 
| --- | --- | --- | 
|  Private or public virtual interfaces per AWS Direct Connect dedicated connection  |  50  |  This limit cannot be increased\.  | 
| Transit virtual interfaces per AWS Direct Connect dedicated connection |  1  | This limit cannot be increased\. | 
| Private, public, or transit virtual interfaces per AWS Direct Connect hosted connection1 | 1 | This limit cannot be increased\. | 
|  Active AWS Direct Connect dedicated connections per Region per account  | 10 |  | 
|  Routes per Border Gateway Protocol \(BGP\) session on a private virtual interface  |  100  |  This limit cannot be increased\.  | 
|  Routes per Border Gateway Protocol \(BGP\) session on a public virtual interface  |  1,000  |  This limit cannot be increased\.  | 
|  Dedicated connections per link aggregation group \(LAG\)  | 4 |  | 
|  Link aggregation groups \(LAGs\) per Region  |  10  |  | 
|  AWS Direct Connect gateways per account  |  200  |  | 
|  Virtual private gateways per AWS Direct Connect gateway  |  10  |  This limit cannot be increased\.  | 
| Transit gateways per AWS Direct Connect gateway | 3 | This limit cannot be increased\. | 
|  Virtual interfaces per AWS Direct Connect gateway  |  30  |  | 
| Number of prefixes from on\-premises to AWS on a transit virtual interface | 100 | This limit cannot be increased\. | 
| Number of prefixes per AWS Transit Gateway from AWS to on\-premises on a transit virtual interface | 20 | This limit cannot be increased\. | 

AWS Direct Connect supports these port speeds over single\-mode fiber: 1 Gbps: 1000BASE\-LX \(1310nm\) and 10 Gbps: 10GBASE\-LR \(1310nm\)\.

1: You cannot create a transit virtual interface on a hosted connection with a capacity less than 1Gbps\.
