# Troubleshooting AWS Direct Connect<a name="Troubleshooting"></a>

The following troubleshooting information can help you diagnose and fix issues with your AWS Direct Connect connection\.

**Contents**
+ [Layer 1 \(physical\) issues](#ts_layer_1)
+ [Layer 2 \(data link\) issues](#ts-layer-2)
+ [Layer 3/4 \(Network/Transport\) issues](#ts-layer-3)
+ [Routing issues](#ts-routing)

## Troubleshooting layer 1 \(physical\) issues<a name="ts_layer_1"></a>

If you or your network provider are having difficulty establishing physical connectivity to an AWS Direct Connect device, use the following steps to troubleshoot the issue\.

1. Verify with the colocation provider that the cross connect is complete\. Ask them or your network provider to provide you with a cross connect completion notice and compare the ports with those listed on your LOA\-CFA\.

1. Verify that your router or your provider's router is powered on and that the ports are activated\.

1. Ensure that the routers are using the correct optical transceiver\. Auto\-negotiation for the port must be disabled if you have a connection with a port speed more than 1 Gbps\. However, depending on the AWS Direct Connect endpoint serving your connection, auto\-negotiation might need to be enabled or disabled for 1 Gbps connections\. If auto\-negotation needs to be disabled for your connections, port speed and full\-duplex mode must be configured manually\. If your virtual interface remains down, see [Troubleshooting layer 2 \(data link\) issues](#ts-layer-2)\.

1. Verify that the router is receiving an acceptable optical signal over the cross connect\.

1. Try flipping \(also known as rolling\) the Tx/Rx fiber strands\.

1. Check the Amazon CloudWatch metrics for AWS Direct Connect\. You can verify the AWS Direct Connect device's Tx/Rx optical readings \(10\-Gbps port speeds only\), physical error count, and operational status\. For more information, see [Monitoring with Amazon CloudWatch](https://docs.aws.amazon.com/directconnect/latest/UserGuide/monitoring-cloudwatch.html)\.

1. Contact the colocation provider and request a written report for the Tx/Rx optical signal across the cross connect\.

1. If the above steps do not resolve physical connectivity issues, [contact AWS Support](https://aws.amazon.com/support/createCase) and provide the cross connect completion notice and optical signal report from the colocation provider\.

The following flow chart contains the steps to diagnose issues with the physical connection\.

![\[Troubleshoot AWS Direct Connect\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/layer1-ts.png)

## Troubleshooting layer 2 \(data link\) issues<a name="ts-layer-2"></a>

If your AWS Direct Connect physical connection is up but your virtual interface is down, use the following steps to troubleshoot the issue\.

1. If you cannot ping the Amazon peer IP address, verify that your peer IP address is configured correctly and in the correct VLAN\. Ensure that the IP address is configured in the VLAN subinterface and not the physical interface \(for example, GigabitEthernet0/0\.123 instead of GigabitEthernet0/0\)\. 

1. Verify if the router has a MAC address entry from the AWS endpoint in your address resolution protocol \(ARP\) table\.

1. Ensure that any intermediate devices between endpoints have VLAN trunking enabled for your 802\.1Q VLAN tag\. ARP cannot be established on the AWS side until AWS receives tagged traffic\.

1. Clear your or your provider's ARP table cache\.

1. If the above steps do not establish ARP or you still cannot ping the Amazon peer IP, [contact AWS Support](https://aws.amazon.com/support/createCase)\.

The following flow chart contains the steps to diagnose issues with the data link\.

![\[Troubleshoot AWS Direct Connect\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/troubleshooting-chart-layer-2.png)

If the BGP session is still not established after verifying these steps, see [Troubleshooting layer 3/4 \(Network/Transport\) issues](#ts-layer-3)\. If the BGP session is established but you are experiencing routing issues, see [Troubleshooting routing issues](#ts-routing)\.

## Troubleshooting layer 3/4 \(Network/Transport\) issues<a name="ts-layer-3"></a>

Consider a situation where your AWS Direct Connect physical connection is up and you can ping the Amazon peer IP address\. If your virtual interface is down and the BGP peering session cannot be established, use the following steps to troubleshoot the issue:

1. Ensure that your BGP local Autonomous System Number \(ASN\) and Amazon's ASN are configured correctly\.

1. Ensure that the peer IPs for both sides of the BGP peering session are configured correctly\.

1. Ensure that your MD5 authentication key is configured and exactly matches the key in the downloaded router configuration file\. Check that there are no extra spaces or characters\.

1. Verify that you or your provider are not advertising more than 100 prefixes for private virtual interfaces or 1,000 prefixes for public virtual interfaces\. These are hard limits and cannot be exceeded\.

1. Ensure that there are no firewall or ACL rules that are blocking TCP port 179 or any high\-numbered ephemeral TCP ports\. These ports are necessary for BGP to establish a TCP connection between the peers\.

1. Check your BGP logs for any errors or warning messages\.

1. If the above steps do not establish the BGP peering session, [contact AWS Support](https://aws.amazon.com/support/createCase)\.

The following flow chart contains the steps to diagnose issues with the BGP peering session\.

![\[Troubleshoot AWS Direct Connect\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/troubleshooting-chart-layer-3-4.png)

If the BGP peering session is established but you are experiencing routing issues, see [Troubleshooting routing issues](#ts-routing)\.

## Troubleshooting routing issues<a name="ts-routing"></a>

Consider a situation where your virtual interface is up and you've established a BGP peering session\. If you cannot route traffic over the virtual interface, use the following steps to troubleshoot the issue:

1. Ensure that you are advertising a route for your on\-premises network prefix over the BGP session\. For a private virtual interface, this can be a private or public network prefix\. For a public virtual interface, this must be your publicly routable network prefix\.

1. For a private virtual interface, ensure that your VPC security groups and network ACLs allow inbound and outbound traffic for your on\-premises network prefix\. For more information, see [Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) and [Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_ACLs.html) in the *Amazon VPC User Guide*\.

1. For a private virtual interface, ensure that your VPC route tables have prefixes pointing to the virtual private gateway to which your private virtual interface is connected\. For example, if you prefer to have all your traffic routed towards your on\-premises network by default, you can add the default route \(0\.0\.0\.0/0 or ::/0\) with the virtual private gateway as the target in your VPC route tables\.
   + Alternatively, enable route propagation to automatically update routes in your route tables based on your dynamic BGP route advertisement\. You can have up to 100 propagated routes per route table\. This limit cannot be increased\. For more information, see [Enabling and Disabling Route Propagation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html#EnableDisableRouteProp) in the *Amazon VPC User Guide*\.

1. If the above steps do not resolve your routing issues, [contact AWS Support](https://aws.amazon.com/support/createCase)\.

The following flow chart contains the steps to diagnose routing issues\.

![\[Troubleshoot AWS Direct Connect\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/troubleshooting-chart-routing.png)