# AWS Direct Connect quotas<a name="limits"></a>

The following table lists the quotas related to AWS Direct Connect\. Unless indicated otherwise, you can request an increase for any of these limits using the [AWS Direct Connect Limits form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-direct-connect)\.


| Component | Quota | Comments | 
| --- | --- | --- | 
|  Private or public virtual interfaces per AWS Direct Connect dedicated connection  |  50  |  This limit cannot be increased\.  | 
| Transit virtual interfaces per AWS Direct Connect dedicated connection |  4  | This limit cannot be increased\. | 
| Private or public virtual interfaces per AWS Direct Connect dedicated connection and transit virtual interfaces per AWS Direct Connect dedicated connection | 50 and 1 transit virtual interface | This limit cannot be increased\. | 
| Private, public, or transit virtual interfaces per AWS Direct Connect hosted connection | 1 | This limit cannot be increased\. | 
|  Active AWS Direct Connect connections per Direct Connect location per Region per account  | 10 | Contact your Solutions Architect \(SA\) or Technical Account Manager \(TAM\) for further assistance\. | 
| Number of virtual interfaces per Link Aggregation Group \(LAG\) | 50 |  | 
|  Routes per Border Gateway Protocol \(BGP\) session on a private virtual interface or transit virtual interface If you advertise more than 100 routes each for IPv4 and IPv6 over the BGP session, the BGP session will go into an idle state with the BGP session DOWN\.  |  100 each for IPv4 and IPv6  |  This limit cannot be increased\.  | 
|  Routes per Border Gateway Protocol \(BGP\) session on a public virtual interface  |  1,000  |  This limit cannot be increased\.  | 
|  Dedicated connections per link aggregation group \(LAG\)  | 4 when the port speed is less than 100G 2 when the port speed is 100G |  | 
|  Link aggregation groups \(LAGs\) per Region  |  10  |  | 
|  AWS Direct Connect gateways per account  |  200  |  | 
|  Virtual private gateways per AWS Direct Connect gateway  |  20  |  This limit cannot be increased\.  | 
| Transit gateways per AWS Direct Connect gateway  | 6 | This limit cannot be increased\. | 
|  Virtual interfaces \(private or transit\) per AWS Direct Connect gateway  |  30  |  | 
| Number of prefixes from on\-premises to AWS on a transit virtual interface | 100 | This limit cannot be increased\. | 
| Number of prefixes per AWS Transit Gateway from AWS to on\-premise on a transit virtual interface | 200 combined total for IPv4 and IPv6 | This limit cannot be increased\. | 
| Number of virtual interfaces per virtual private gateway | There is no limit\. |  | 
| Number of Direct Connect gateways associated to a transit gateway | 20 | This limit cannot be increased\. | 

AWS Direct Connect supports these port speeds over single\-mode fiber: 1 Gbps: 1000BASE\-LX \(1310 nm\), 10 Gbps: 10GBASE\-LR \(1310 nm\) and 100Gbps: 100GBASE\-LR4\.

## BGP quotas<a name="bgp-quotas"></a>

The following are BGP quotas\. The BGP timers negotiate down to the lowest value between the routers\. The BFD intervals are defined by the slowest device\.
+ Default hold timer: 90 seconds
+ Minimum hold timer: 3 seconds

  A hold value of 0 is not supported\.
+ Default keepalive timer: 30 seconds
+ Minimum keepalive timer: 1 second
+ Graceful restart timer: 120 seconds

  We recommend that you do not configure graceful restart and BFD at the same time\.
+ BFD liveness detection minimum interval: 300 ms
+ BFD minimum multiplier: 3

## Load balance considerations<a name="load-balance-considerations"></a>

If you want to use load balancing with multiple public VIFs, all the VIFs must be in the same Region\.