# Create a hosted virtual interface<a name="createhostedvirtualinterface"></a>

You can create a public, transit, or private hosted virtual interface\. Before you begin, ensure that you have read the information in [Prerequisites for virtual interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

## Create a hosted private virtual interface<a name="create-hosted-private-vif"></a>

**To create a hosted private virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Private**\.

1. Under **Private virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **Virtual interface owner**, choose **Another AWS account**, and then for **Virtual interface owner**, enter the ID of the account to own this virtual interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol Autonomous System Number of your on\-premises peer router for the new virtual interface\.

      The valid values are 1\-2147483647\.

1. Under **Additional Settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.
**Important**  
If you let AWS auto\-assign IP addresses, a /30 CIDR will be allocated from 169\.254\.0\.0/16\. AWS does not recommend this option if you intend to use the customer router peer IP address as the source and destination for traffic\. Instead you should use RFC 1918 or other addressing, and specify the address yourself\. For more information about RFC 1918 see [ Address Allocation for Private Internets](https://datatracker.ietf.org/doc/html/rfc1918)\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To change the maximum transmission unit \(MTU\) from 1500 \(default\) to 9001 \(jumbo frames\), select **Jumbo MTU \(MTU size 9001\)**\.

   1. \(Optional\) Add or remove a tag\.

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. After the hosted virtual interface is accepted by the owner of the other AWS account, you can [download the router configuration file](create-vif.md#vif-router-config)\.

**To create a hosted private virtual interface using the command line or API**
+ [allocate\-private\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-private-virtual-interface.html) \(AWS CLI\)
+ [AllocatePrivateVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePrivateVirtualInterface.html) \(AWS Direct Connect API\)

## Create a hosted public virtual interface<a name="create-hosted-public-vif"></a>

**To create a hosted public virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Public**\.

1. Under **Public Virtual Interface Settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **Virtual interface owner**, choose **Another AWS account**, and then for **Virtual interface owner**, enter the ID of the account to own this virtual interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol Autonomous System Number of your on\-premises peer router for the new virtual interface\.

      The valid values are 1\-2147483647\.

1. To configure an IPv4 BGP or an IPv6 peer, do the following:

   \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
   + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
   + For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.
**Important**  
If you let AWS auto\-assign IP addresses, a /30 CIDR will be allocated from 169\.254\.0\.0/16\. AWS does not recommend this option if you intend to use the customer router peer IP address as the source and destination for traffic\. Instead you should use RFC 1918 or other addressing, and specify the address yourself\. For more information about RFC 1918 see [ Address Allocation for Private Internets](https://datatracker.ietf.org/doc/html/rfc1918)\.

   \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

1. To advertise prefixes to Amazon, for **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\. 

1. To provide your own key to authenticate the BGP session, under **Additional Settings**, for **BGP authentication key**, enter the key\.

   If you do not enter a value, then we generate a BGP key\.

1. \(Optional\) Add or remove a tag\.

   \[Add a tag\] Choose **Add tag** and do the following:
   + For **Key**, enter the key name\.
   + For **Value**, enter the key value\.

   \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create virtual interface**\.

1. After the hosted virtual interface is accepted by the owner of the other AWS account, you can [download the router configuration file](create-vif.md#vif-router-config)\.

**To create a hosted public virtual interface using the command line or API**
+ [allocate\-public\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-public-virtual-interface.html) \(AWS CLI\)
+ [AllocatePublicVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePublicVirtualInterface.html) \(AWS Direct Connect API\)

## Create a hosted transit virtual interface<a name="create-hosted-transit-vif"></a>

**To create a hosted transit virtual interface**
**Important**  
If you associate your transit gateway with one or more Direct Connect gateways, the Autonomous System Number \(ASN\) used by the transit gateway and the Direct Connect gateway must be different\. For example, if you use the default ASN 64512 for both the transit gateway and the Direct Connect gateway, the association request fails\.

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Transit**\.

1. Under **Transit virtual interface settings**, do the following:

   1. For **Virtual interface name**, enter a name for the virtual interface\.

   1. For **Connection**, choose the Direct Connect connection that you want to use for this interface\.

   1. For **Virtual interface owner**, choose **Another AWS account**, and then for **Virtual interface owner**, enter the ID of the account to own this virtual interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\. 

   1. For **BGP ASN**, enter the Border Gateway Protocol Autonomous System Number of your on\-premises peer router for the new virtual interface\.

      The valid values are 1\-2147483647\.

1. Under **Additional Settings**, do the following:

   1. To configure an IPv4 BGP or an IPv6 peer, do the following:

      \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
      + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. 
      + For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.
**Important**  
If you let AWS auto\-assign IP addresses, a /30 CIDR will be allocated from 169\.254\.0\.0/16\. AWS does not recommend this option if you intend to use the customer router peer IP address as the source and destination for traffic\. Instead you should use RFC 1918 or other addressing, and specify the address yourself\. For more information about RFC 1918 see [ Address Allocation for Private Internets](https://datatracker.ietf.org/doc/html/rfc1918)\.

      \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. To change the maximum transmission unit \(MTU\) from 1500 \(default\) to 8500 \(jumbo frames\), select **Jumbo MTU \(MTU size 8500\)**\.

   1. \[Optional\] Add a tag\. Do the following:

      \[Add a tag\] Choose **Add tag** and do the following:
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create virtual interface**\.

1. After the hosted virtual interface is accepted by the owner of the other AWS account, you can [download the router configuration file](create-vif.md#vif-router-config)\.

**To create a hosted transit virtual interface using the command line or API**
+ [allocate\-transit\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-public-transit-interface.html) \(AWS CLI\)
+ [AllocateTransitVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocateTransitVirtualInterface.html) \(AWS Direct Connect API\)