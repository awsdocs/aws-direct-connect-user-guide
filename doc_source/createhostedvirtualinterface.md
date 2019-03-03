# Creating a Hosted Virtual Interface<a name="createhostedvirtualinterface"></a>

You can create a public or private hosted virtual interface\. Before you begin, ensure that you have read the information in [Prerequisites for Virtual Interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

## Creating a Hosted Private Virtual Interface<a name="create-hosted-private-vif"></a>

**To create a hosted private virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Connections**\.

1. Select the connection and choose **Actions**, **Create Virtual Interface**\.

1. Choose **Private**\.

1. For **Virtual Interface Name**, type a name for the virtual interface\.

1. For **Virtual Interface Owner**, choose **Another AWS Account**\. For **Account ID**, type the ID of the AWS account to own this virtual interface\.

1. For **VLAN**, type the ID number for your virtual local area network \(VLAN\)\.

1. \[IPv4\] To configure an IPv4 BGP peer, choose **IPv4** and do one of the following:
   + To have AWS generate your router IP address and Amazon IP address, select **Auto\-generate peer IPs**\.
   + To specify these IP addresses yourself, clear **Auto\-generate peer IPs**\. For **Your router peer IP**, type the destination IPv4 CIDR address to which Amazon should send traffic\. For **Amazon router peer IP**, type the IPv4 CIDR address to use to send traffic to AWS\.

   \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

1. For **BGP ASN**, type the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

   To have AWS generate a BGP key, select **Auto\-generate BGP key**\.

   To provide your own BGP key, clear **Auto\-generate BGP key**\. For **BGP Authentication Key**, type your BGP MD5 key\.

1. To change the maximum transmission unit \(MTU\) from 1500 \(default\) to 9001 \(jumbo frames\), select **Jumbo MTU \(MTU size 9001\)**\.

1. Choose **Continue**\.

1. After the hosted virtual interface is accepted by the owner of the other AWS account, you can [download the router configuration file](create-vif.md#vif-router-config)\.

**To create a hosted private virtual interface using the command line or API**
+ [https://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-private-virtual-interface.html](https://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-private-virtual-interface.html) \(AWS CLI\)
+ [https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePrivateVirtualInterface.html](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePrivateVirtualInterface.html) \(AWS Direct Connect API\)

## Creating a Hosted Public Virtual Interface<a name="create-hosted-public-vif"></a>

**To create a hosted public virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Connections**\.

1. Select the connection and choose **Actions**, **Create Virtual Interface**\.

1. Choose **Public**\.

1. For **Virtual Interface Name**, type a name for the virtual interface\.

1. For **Virtual Interface Owner**, choose **Another AWS Account**\. For **Account ID**, type the ID of the AWS account to own this virtual interface\.

1. For **VLAN**, type the ID number for your virtual local area network \(VLAN\)\.

1. \[IPv4\] To configure an IPv4 BGP peer, do the following:

   1. Choose **IPv4**\.

   1. For **Your router peer IP**, type the IPv4 CIDR destination address to which Amazon should send traffic\.

   1. For **Amazon router peer IP**, type the IPv4 CIDR address to use to send traffic to AWS\.

   \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

1. For **BGP ASN**, type the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

   To have AWS generate a BGP key, select **Auto\-generate BGP key**\.

   To provide your own BGP key, clear **Auto\-generate BGP key**\. For **BGP Authentication Key**, type your BGP MD5 key\.

1. For **Prefixes you want to advertise**, type the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\.

1. Choose **Continue**\.

1. After the hosted virtual interface is accepted by the owner of the other AWS account, you can [download the router configuration file](create-vif.md#vif-router-config)\.

**To create a hosted public virtual interface using the command line or API**
+ [https://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-public-virtual-interface.html](https://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-public-virtual-interface.html) \(AWS CLI\)
+ [https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePublicVirtualInterface.html](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePublicVirtualInterface.html) \(AWS Direct Connect API\)