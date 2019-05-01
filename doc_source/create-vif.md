# Creating a Virtual Interface<a name="create-vif"></a>

You can create a transit virtual interface to connect to a transit gateway, a public virtual interface to connect to public resources \(non\-VPC services\), or a private virtual interface to connect to a VPC\.

**Prerequisites**  
Before you begin, ensure that you have read the information in [Prerequisites for Virtual Interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

## Creating a Public Virtual Interface<a name="create-public-vif"></a>

When you create a public virtual interface, it can take up to 72 hours for AWS to review and approve your request\.

**To provision a public virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Public**\.

1. Under **Public virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

1. Under **Additional settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to AWS\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To provide your own BGP key, enter your BGP MD5 key\.

      If you do not enter a value, AWS generates a BGP key\.

   1. To advertise prefixes to Amazon, for **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\. 

1. Choose **Create virtual interface**\.

1. Download the router configuration for your device\. For more information, see [Downloading the Router Configuration File](#vif-router-config)\.

**To create a public virtual interface using the command line or API**
+ [create\-public\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-public-virtual-interface.html) \(AWS CLI\)
+ [CreatePublicVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreatePublicVirtualInterface.html) \(AWS Direct Connect API\)

## Creating a Private Virtual Interface<a name="create-private-vif"></a>

You can provision a private virtual interface to a virtual private gateway in the same Region as your AWS Direct Connect connection\. For more information about provisioning a private virtual interface to an AWS Direct Connect gateway, see [Working with Direct Connect Gateways](direct-connect-gateways.md)\.

If you use the VPC wizard to create a VPC, route propagation is automatically enabled for you\. With route propagation, routes are automatically populated to the route tables in your VPC\. If you choose, you can disable route propagation\. For more information, see [Enable Route Propagation in Your Route Table](https://docs.aws.amazon.com/vpc/latest/userguide/SetUpVPNConnections.html#vpn-configure-routing) in the *Amazon VPC User Guide*\.

**To provision a private virtual interface to a VPC**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Private**\.

1. Under **Private virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **Gateway type**, choose **Virtual private gateway**\. 

   1. For **Virtual interface owner**, choose **Another AWS account**, and then enter the AWS account\. 

   1. For **Virtual private gateway**, choose the virtual private gateway to use for this interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

1. Under **Additional Settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To advertise prefixes to Amazon, for **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\. 

   1. To change the maximum transmission unit \(MTU\) from 1500 \(default\) to 9001 \(jumbo frames\), select **Jumbo MTU \(MTU size 9001\)**\.

1. Choose **Create virtual interface**\.

1. Download the router configuration for your device\. For more information, see [Downloading the Router Configuration File](#vif-router-config)\.

**To create a private virtual interface using the command line or API**
+ [create\-private\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-private-virtual-interface.html) \(AWS CLI\)
+ [CreatePrivateVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreatePrivateVirtualInterface.html) \(AWS Direct Connect API\)

## Creating a Transit Virtual Interface to the Direct Connect Gateway<a name="create-transit-vif"></a>

To connect your AWS Direct Connect connection to the transit gateway, you must create a transit interface for your connection\. Specify the Direct Connect gateway to which to connect\.

**Important**  
If you associate your transit gateway with one or more Direct Connect gateways, the Autonomous System Number \(ASN\) used by the transit gateway and the Direct Connect gateway must be different\. For example, if you use the default ASN 64512 for both the transit gateway and the Direct Connect gateway, the association request fails\.

**To provision a transit virtual interface to a Direct Connect gateway**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Transit**\.

1. Under **Transit virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **Virtual interface owner**, choose **My AWS account** if the virtual interface is for your AWS account\. 

   1. For **Gateway type**, choose **Direct Connect gateway**\.

   1.  For **Direct Connect gateway**, select the Direct Connect gateway\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

1. Under **Additional Settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To change the maximum transmission unit \(MTU\) from 1500 \(default\) to 8500 \(jumbo frames\), select **Jumbo MTU \(MTU size 8500\)**\.

1. Choose **Create virtual interface**\.

After you create the virtual interface, you can download the router configuration for your device\. For more information, see [Downloading the Router Configuration File](#vif-router-config)\.

**To create a transit virtual interface using the command line or API**
+ [create\-transit\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-transit-virtual-interface.html) \(AWS CLI\)
+ [CreateTransitVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateTransitVirtualInterface.html) \(AWS Direct Connect API\)

**To view the virtual interfaces that are attached to a Direct Connect gateway using the command line or API**
+ [describe\-direct\-connect\-gateway\-attachments](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-attachments.html) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAttachments](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAttachments.html) \(AWS Direct Connect API\)

## Downloading the Router Configuration File<a name="vif-router-config"></a>

After you create the virtual interface, you can download the router configuration file for your router\.

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and then choose **View details**\.

1. Choose **Download router configuration**\.

1. For **Download router configuration**, do the following:

   1. For **Vendor**, select the manufacturer of your router\.

   1. For **Platform**, select the model of your router\.

   1. For **Software**, select the software version for your router\.

1. Choose **Download**, and then use the appropriate configuration for your router to ensure that you can connect to AWS Direct Connect\.

### Example Router Configuration Files<a name="vif-example-router-files"></a>

The following are example extracts of router configuration files\.

**Cisco IOS**

```
interface GigabitEthernet0/1
no ip address

interface GigabitEthernet0/1.VLAN_NUMBER
description "Direct Connect to your Amazon VPC or AWS Cloud"
encapsulation dot1Q VLAN_NUMBER
ip address YOUR_PEER_IP

router bgp CUSTOMER_BGP_ASN
neighbor AWS_PEER_IP remote-as AWS_ASN
neighbor AWS_PEER_IP password MD5_key
network 0.0.0.0 
exit

! Optionally configure Bidirectional Forwarding Detection (BFD).

interface GigabitEthernet0/1.VLAN_NUMBER 
bfd interval 300 min_rx 300 multiplier 3 
router bgp CUSTOMER_BGP_ASN 
neighbor AWS_PEER_IP fall-over bfd 

! NAT Configuration for Public Virtual Interfaces (Optional)

ip access-list standard NAT-ACL
permit (internal subnet IP address for NAT)
exit

ip nat inside source list NAT-ACL interface GigabitEthernet0/1.VLAN_NUMBER overload

interface GigabitEthernet0/1.VLAN_NUMBER
 ip nat outside
exit

interface interface-towards-customer-local-network
 ip nat inside
exit
```

**Cisco NX\-OS**

```
feature interface-vlan
vlan VLAN_NUMBER
name "Direct Connect to your Amazon VPC or AWS Cloud"

interface VlanVLAN_NUMBER
  ip address YOUR_PEER_IP/30
  no shutdown

interface Ethernet0/1
  switchport
  switchport mode trunk
  switchport trunk allowed vlan VLAN_NUMBER
  no shutdown

router bgp CUSTOMER_BGP_ASN
  address-family ipv4 unicast
    network 0.0.0.0
  neighbor AWS_PEER_IP remote-as AWS_ASN
    password 0 MD5_key
    address-family ipv4 unicast

! Optionally configure Bidirectional Forwarding Detection (BFD).

feature bfd
interface VlanVLAN_NUMBER
no ip redirects
bfd interval 300 min_rx 300 multiplier 3
router bgp CUSTOMER_BGP_ASN
neighbor AWS_PEER_IP remote-as AWS_ASN
bfd

! NAT Configuration for Public Virtual Interfaces (Optional)

ip access-list standard NAT-ACL
 permit any any
exit

ip nat inside source list NAT-ACL VlanVLAN_NUMBER overload

interface VlanVLAN_NUMBER
 ip nat outside
exit

interface interface-towards-customer-local-network
 ip nat inside
exit
```

**Juniper JunOS**

```
configure exclusive
edit interfaces ge-0/0/1
set description "Direct Connect to your Amazon VPC or AWS Cloud"
set flexible-vlan-tagging
set mtu 1522
edit unit 0
set vlan-id VLAN_NUMBER
set family inet mtu 1500
set family inet address YOUR_PEER_IP
top

edit policy-options policy-statement EXPORT-DEFAULT
edit term DEFAULT
set from route-filter 0.0.0.0/0 exact
set then accept
up
edit term REJECT
set then reject
top

set routing-options autonomous-system CUSTOMER_BGP_ASN

edit protocols bgp group EBGP
set type external
set peer-as AWS_ASN

edit neighbor AWS_PEER_IP
set local-address YOUR_PEER_IP
set export EXPORT-DEFAULT
set authentication-key "MD5_key"
top
commit check
commit and-quit

# Optionally configure Bidirectional Forwarding Detection (BFD).

set protocols bgp group EBGP neighbor AWS_PEER_IP bfd-liveness-detection minimum-interval 300 
set protocols bgp group EBGP neighbor AWS_PEER_IP bfd-liveness-detection multiplier 3

# NAT Configuration for Public Virtual Interfaces (Optional)

set security policies from-zone trust to-zone untrust policy PolicyName match source-address any
set security policies from-zone trust to-zone untrust policy PolicyName match destination-address any
set security policies from-zone trust to-zone untrust policy PolicyName match application any
set security policies from-zone trust to-zone untrust policy PolicyName then permit

set security nat source rule-set SNAT-RS from zone trust
set security nat source rule-set SNAT-RS to zone untrust
set security nat source rule-set SNAT-RS rule SNAT-Rule match source-address 0.0.0.0/0
set security nat source rule-set SNAT-RS rule SNAT-Rule then source-nat interface

commit check
commit and-quit
```