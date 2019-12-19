# Adding or Deleting a BGP Peer<a name="add-peer-to-vif"></a>

 In some locations, a virtual interface can support up to two IPv4 BGP peering sessions and up to two IPv6 BGP peering sessions\. In other locations, a virtual interface can support a single IPv4 BGP peering session and a single IPv6 BGP peering session\. For information about the Regions that support logical redundancy, see [AWS Direct Connect Locations](https://aws.amazon.com/directconnect/features/#AWS_Direct_Connect_Locations)\.

You cannot specify your own peer IPv6 addresses for an IPv6 BGP peering session\. Amazon automatically allocates you a /125 IPv6 CIDR\. 

Multiprotocol BGP is not supported\. IPv4 and IPv6 operate in dual\-stack mode for the virtual interface\.

## Adding a BGP Peer<a name="add-bgp-peer-vif"></a>

Use the following procedure to add a BGP peer\.

**To add a BGP peer**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and then choose **View details**\.

1. Choose **Add peering**\.

1. \(Private virtual interface\) To add IPv4 BGP peers, do the following:
   + Choose **IPv4**\.
   + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.  
![\[Add BGP peering for IPv4\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/add_bgp_peering.png)

1. \(Public virtual interface\) To add IPv4 BGP peers, do the following:
   + For **Your router peer ip**, enter the IPv4 CIDR destination address where traffic should be sent\.
   + For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to AWS\.

1. \(Private or public virtual interface\) To add IPv6 BGP peers, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses; you cannot specify custom IPv6 addresses\.

1. For **BGP ASN**, enter the Border Gateway Protocol \(BGP\) Autonomous System Number \(ASN\) of your gateway, for example, a number between 1 and 65534\. For a public virtual interface, the ASN must be private or already whitelisted for the virtual interface\.

   The valid values are 1\-2147483647\.

1. To provide your own BGP key, for **BGP Authentication Key**, enter your BGP MD5 key\.

1. Choose **Add peering**\.

**To create a BGP peer using the command line or API**
+ [create\-bgp\-peer](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-bgp-peer.html) \(AWS CLI\)
+ [CreateBGPPeer](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateBGPPeer.html) \(AWS Direct Connect API\)

## Deleting a BGP Peer<a name="delete-bgp-peer-vif"></a>

If your virtual interface has both an IPv4 and IPv6 BGP peering session, you can delete one of the BGP peering sessions \(but not both\)\.

**To delete a BGP peer**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and then choose **View details**\.

1. Under **Peerings,** select the peering that you want to delete and then choose **Delete**\.

1. In the **Remove peering from virtual interface** dialog box, choose **Delete**\.

**To delete a BGP peer using the command line or API**
+ [delete\-bgp\-peer](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-bgp-peer.html) \(AWS CLI\)
+ [DeleteBGPPeer](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteBGPPeer.html) \(AWS Direct Connect API\)