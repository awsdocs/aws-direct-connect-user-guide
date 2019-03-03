# Adding or Deleting a BGP Peer<a name="add-peer-to-vif"></a>

 In some locations, a virtual interface can support up to two IPv4 BGP peering sessions and up to two IPv6 BGP peering sessions\. In other locations, a virtual interface can support a single IPv4 BGP peering session and a single IPv6 BGP peering session\. For information about the Regions that support logical redundancy, see [AWS Direct Connect Locations](https://aws.amazon.com/directconnect/features/#AWS_Direct_Connect_Locations)\.

You cannot specify your own peer IPv6 addresses for an IPv6 BGP peering session\. Amazon automatically allocates you a /125 IPv6 CIDR\. 

Multiprotocol BGP is not supported\. IPv4 and IPv6 operate in dual\-stack mode for the virtual interface\.

## Adding a BGP Peer<a name="add-bgp-peer-vif"></a>

Use the following procedure to add a BGP peer\.

**To add a BGP peer**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and choose **Actions**, **Add Peering**\.

1. \(Private virtual interface\) To add IPv4 BGP peers, do the following:
   + To have AWS generate your router IP address and Amazon IP address, select **Auto\-generate peer IPs**\.
   + To specify these IP addresses yourself, clear **Auto\-generate peer IPs**\. For **Your router peer IP**, type the destination IPv4 CIDR address to which Amazon should send traffic\. In the **Amazon router peer IP** field, type the IPv4 CIDR address to use to send traffic to AWS\.  
![\[Add BGP peering for IPv4\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/add_bgp_peering.png)

1. \(Public virtual interface\) To add IPv4 BGP peers, do the following:
   + For **Your router peer IP**, type the IPv4 CIDR destination address where traffic should be sent\.
   + For **Amazon router peer IP**, type the IPv4 CIDR address to use to send traffic to AWS\.

1. \(Private or public virtual interface\) To add IPv6 BGP peers, the **Auto\-generate peer IPs** is selected by default\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses; you cannot specify custom IPv6 addresses\.  
![\[Add BGP peering for IPv6\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/add_bgp_peering_ipv6.png)

1. In the **BGP ASN** field, type the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway; for example, a number between 1 and 65534\. For a public virtual interface, the ASN must be private or already whitelisted for the virtual interface\.

1. Select **Auto\-generate BGP key** to have AWS to generate one for you\.

   To provide your own BGP key, clear **Auto\-generate BGP key**\. For **BGP Authentication Key**, type your BGP MD5 key\.

1. Choose **Continue**\.

**To create a BGP peer using the command line or API**
+ [https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-bgp-peer.html](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-bgp-peer.html) \(AWS CLI\)
+ [https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateBGPPeer.html](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateBGPPeer.html) \(AWS Direct Connect API\)

## Deleting a BGP Peer<a name="delete-bgp-peer-vif"></a>

If your virtual interface has both an IPv4 and IPv6 BGP peering session, you can delete one of the BGP peering sessions \(but not both\)\.

**To delete a BGP peer**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and choose **Actions**, **Delete Peering**\.

1. To delete the IPv4 BGP peer, choose **IPv4**\. To delete the IPv6 BGP peer, choose **IPv6**\.

1. Choose **Delete**\.

**To delete a BGP peer using the command line or API**
+ [https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-bgp-peer.html](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-bgp-peer.html) \(AWS CLI\)
+ [https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteBGPPeer.html](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteBGPPeer.html) \(AWS Direct Connect API\)