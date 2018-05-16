# Creating a Hosted Virtual Interface<a name="createhostedvirtualinterface"></a>

You can create a public or private hosted virtual interface\. Before you begin, ensure that you have read the information in [Prerequisites for Virtual Interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\.

**To create a hosted private virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. If necessary, change the region in the navigation bar\. For more information, see [AWS Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html)\.

1. In the navigation pane, choose **Connections**\.

1. In the **Connections** pane, select the connection to which to add a virtual interface and choose **Actions**, **Create Virtual Interface**\.

1. Select the **Private** option\.

1. Under **Define Your New Private Virtual Interface**, do the following:

   1. For **Virtual Interface Name**, enter a name for the virtual interface\.

   1. For **Virtual Interface Owner**, choose **Another AWS Account**\. For **Account ID**, enter the AWS account ID number to associate as the owner of this virtual interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\.

   1. If you're configuring an IPv4 BGP peer, choose **IPv4**, and do the following:
      + To have AWS generate your router IP address and Amazon IP address, select **Auto\-generate peer IPs**\.
      + To specify these IP addresses yourself, clear the **Auto\-generate peer IPs** check box\. For **Your router peer IP**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to AWS\. 

   1. If you're configuring an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

   1. Select the **Auto\-generate BGP key** check box if you would like AWS to generate one for you\.

      To provide your own BGP key, clear the **Auto\-generate BGP key** check box\. For **BGP Authentication Key**, enter your BGP MD5 key\.

1. Choose **Continue**\. The new interface is added to the list of virtual interfaces on the **Virtual Interfaces** pane\.

1. After the hosted virtual interface is accepted by the owner of the other AWS account, you can [download the router configuration file](create-vif.md#vif-router-config)\.

**To create a hosted public virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. If necessary, change the region in the navigation bar\. For more information, see [AWS Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html)\.

1. In the navigation pane, choose **Connections**\.

1. In the **Connections** pane, select the connection to which to add a virtual interface and choose **Actions**, **Create Virtual Interface**\.

1. Select the **Public** option\.

1. In the **Define Your New Public Virtual Interface** dialog box, do the following:

   1. For **Virtual Interface Name**, enter a name for the virtual interface\.

   1. For **Virtual Interface Owner**, choose **Another AWS Account**\. For **Account ID**, enter the AWS account ID number to associate as the owner of this virtual interface\.

   1. For **VLAN**, enter the ID number for your virtual local area network \(VLAN\)\.

   1. If you're configuring an IPv4 BGP peer, choose **IPv4**, and do the following:
      + For **Your router peer IP**, enter the IPv4 CIDR destination address to which Amazon should send traffic\.
      + For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to Amazon\.

   1. If you're configuring an IPv6 BGP peer, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses\. You cannot specify custom IPv6 addresses\.

   1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway\.

   1. To have AWS generate a BGP key, select the **Auto\-generate BGP key** check box\.

      To provide your own BGP key, clear the **Auto\-generate BGP key** check box\. For **BGP Authentication Key**, enter your BGP MD5 key\.

   1. For **Prefixes you want to advertise**, enter the IPv4 CIDR destination addresses \(separated by commas\) to which traffic should be routed over the virtual interface\.

1. Choose **Continue**\. The new interface is added to the list of virtual interfaces on the **Virtual Interfaces** pane\.

1. After the hosted virtual interface is accepted by the owner of the other AWS account, you can [download the router configuration file](create-vif.md#vif-router-config)\.

**To create a hosted private virtual interface using the command line or API**
+ [allocate\-private\-virtual\-interface](http://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-private-virtual-interface.html) \(AWS CLI\)
+ [AllocatePrivateVirtualInterface](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePrivateVirtualInterface.html) \(AWS Direct Connect API\)

**To create a hosted public virtual interface using the command line or API**
+ [allocate\-public\-virtual\-interface](http://docs.aws.amazon.com/cli/latest/reference/directconnect/allocate-public-virtual-interface.html) \(AWS CLI\)
+ [AllocatePublicVirtualInterface](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_AllocatePublicVirtualInterface.html) \(AWS Direct Connect API\)