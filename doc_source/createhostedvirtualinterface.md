# Creating a Hosted Virtual Interface<a name="createhostedvirtualinterface"></a>

You can create a public or private hosted virtual interface\. Before you begin, ensure that you have read the information in [Prerequisites for Virtual Interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

## Creating a Hosted Private Virtual Interface<a name="create-hosted-private-vif"></a>

**To create a hosted private virtual interface**

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

1. After the hosted virtual interface is accepted by the owner of the other AWS account, you can [download the router configuration file](create-vif.md#vif-router-config)\.

**To create a hosted private virtual interface using the command line or API**
+ [allocate\-private\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-private-virtual-interface.html) \(AWS CLI\)
+ [AllocatePrivateVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePrivateVirtualInterface.html) \(AWS Direct Connect API\)

## Creating a Hosted Public Virtual Interface<a name="create-hosted-public-vif"></a>

**To create a hosted public virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Choose **Create virtual interface**\.

1. Under **Virtual interface type**, for **Type**, choose **Public**\.

1. Under **Private virtual interface settings**, for **Virtual interface name**, enter a name for the virtual interface\.

1. Under **Additional Settings**, for **Virtual interface owner**, enter the ID of the AWS account to own this virtual interface\.

1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\.

1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your AWS endpoint\.

1. To configure an IPv4 BGP or an IPv6 peer, do the following:

   \[IPv4\] To configure an IPv4 BGP peer, under **Additional Settings**, choose **IPv4** and do one of the following:
   + To specify these IP addresses yourself, for **Your router peer IP**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to AWS\.

   \[IPv6\] To configure an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

1. To provide your own BGP key, under **Additional Settings**, enter your BGP MD5 key\.

   If you do not enter a value, then AWS generates a BGP key\.

1. To advertise prefixes to Amazon, under **Additional Settings**, for **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\. 

1. Choose **Create virtual interface**\.

1. After the hosted virtual interface is accepted by the owner of the other AWS account, you can [download the router configuration file](create-vif.md#vif-router-config)\.

**To create a hosted public virtual interface using the command line or API**
+ [allocate\-public\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-public-virtual-interface.html) \(AWS CLI\)
+ [AllocatePublicVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePublicVirtualInterface.html) \(AWS Direct Connect API\)