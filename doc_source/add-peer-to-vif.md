# Adding or Removing a BGP Peer<a name="add-peer-to-vif"></a>

A virtual interface can support a single IPv4 BGP peering session and a single IPv6 BGP peering session\. You can add an IPv6 BGP peering session to a virtual interface that has an existing IPv4 BGP peering session\. Alternately, you can add an IPv4 BGP peering session to a virtual interface that has an existing IPv6 BGP peering session\. 

You cannot specify your own peer IPv6 addresses for an IPv6 BGP peering session\. Amazon automatically allocates you a /125 IPv6 CIDR\. 

Multiprotocol BGP is not supported\. IPv4 and IPv6 operate in dual\-stack mode for the virtual interface\.

**To add a BGP peer**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and choose **Actions**, **Add Peering**\.

1. \(Private virtual interface\) To add an IPv4 BGP peer, do the following:
   + To have AWS generate your router IP address and Amazon IP address, select **Auto\-generate peer IPs**\.
   + To specify these IP addresses yourself, clear **Auto\-generate peer IPs**\. For **Your router peer IP**, type the destination IPv4 CIDR address to which Amazon should send traffic\. In the **Amazon router peer IP** field, type the IPv4 CIDR address to use to send traffic to AWS\.  
![\[Add BGP peering for IPv4\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/add_bgp_peering.png)

1. \(Public virtual interface\) To add an IPv4 BGP peer, do the following:
   + For **Your router peer IP**, type the IPv4 CIDR destination address where traffic should be sent\.
   + For **Amazon router peer IP**, type the IPv4 CIDR address to use to send traffic to AWS\.

1. \(Private or public virtual interface\) To add an IPv6 BGP peer, the **Auto\-generate peer IPs** is selected by default\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses; you cannot specify custom IPv6 addresses\.  
![\[Add BGP peering for IPv6\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/add_bgp_peering_ipv6.png)

1. In the **BGP ASN** field, type the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway; for example, a number between 1 and 65534\. For a public virtual interface, the ASN must be private or already whitelisted for the virtual interface\.

1. Select **Auto\-generate BGP key** to have AWS to generate one for you\.

   To provide your own BGP key, clear **Auto\-generate BGP key**\. For **BGP Authentication Key**, type your BGP MD5 key\.

1. Choose **Continue**\.

If your virtual interface has both an IPv4 and IPv6 BGP peering session, you can delete one of the BGP peering sessions \(but not both\)\.

**To delete a BGP peer**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and choose **Actions**, **Delete Peering**\.

1. To delete the IPv4 BGP peer, choose **IPv4**\. To delete the IPv6 BGP peer, choose **IPv6**\.

1. Choose **Delete**\.

**To create a BGP peer using the command line or API**
+ [create\-bgp\-peer](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-bgp-peer.html) \(AWS CLI\)
+ [CreateBGPPeer](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateBGPPeer.html) \(AWS Direct Connect API\)

**To delete a BGP peer using the command line or API**
+ [delete\-bgp\-peer](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-bgp-peer.html) \(AWS CLI\)
+ [DeleteBGPPeer](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteBGPPeer.html) \(AWS Direct Connect API\)