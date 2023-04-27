# Add or delete a BGP peer<a name="add-peer-to-vif"></a>

Add or delete an IPv4 or IPv6 BGP peering session to your virtual interface\.

A virtual interface can support a single IPv4 BGP peering session and a single IPv6 BGP peering session\.

You cannot specify your own peer IPv6 addresses for an IPv6 BGP peering session\. Amazon automatically allocates you a /125 IPv6 CIDR\. 

Multi\-protocol BGP is not supported\. IPv4 and IPv6 operate in dual\-stack mode for the virtual interface\.

AWS enables MD5 by default\. You cannot modify this option\.

## Add a BGP peer<a name="add-bgp-peer-vif"></a>

Use the following procedure to add a BGP peer\.

**To add a BGP peer**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and then choose **View details**\.

1. Choose **Add peering**\.

1. \(Private virtual interface\) To add IPv4 BGP peers, do the following:
   + Choose **IPv4**\.
   + To specify these IP addresses yourself, for **Your router peer ip**, enter the destination IPv4 CIDR address to which Amazon should send traffic\. For **Amazon router peer ip**, enter the IPv4 CIDR address to use to send traffic to AWS\.

1. \(Public virtual interface\) To add IPv4 BGP peers, do the following:
   + For **Your router peer ip**, enter the IPv4 CIDR destination address where traffic should be sent\.
   + For **Amazon router peer IP**, enter the IPv4 CIDR address to use to send traffic to AWS\.
**Important**  
If you let AWS auto\-assign IP addresses, a /30 CIDR will be allocated from 169\.254\.0\.0/16\. AWS does not recommend this option if you intend to use the customer router peer IP address as the source and destination for traffic\. Instead you should use RFC 1918 or other addressing, and specify the address yourself\. For more information about RFC 1918 see [ Address Allocation for Private Internets](https://datatracker.ietf.org/doc/html/rfc1918)\.

1. \(Private or public virtual interface\) To add IPv6 BGP peers, choose **IPv6**\. The peer IPv6 addresses are automatically assigned from Amazon's pool of IPv6 addresses; you cannot specify custom IPv6 addresses\.

1. For **BGP ASN**, enter the Border Gateway Protocol Autonomous System Number of your on\-premises peer router for the new virtual interface\.

   For a public virtual interface, the ASN must be private or already on the allow list for the virtual interface\.

   The valid values are 1\-2147483647\.

   Note that if you do not enter a value, we automatically assign one\.

1. To provide your own BGP key, for **BGP Authentication Key**, enter your BGP MD5 key\.

1. Choose **Add peering**\.

**To create a BGP peer using the command line or API**
+ [create\-bgp\-peer](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-bgp-peer.html) \(AWS CLI\)
+ [CreateBGPPeer](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateBGPPeer.html) \(AWS Direct Connect API\)

## Delete a BGP peer<a name="delete-bgp-peer-vif"></a>

If your virtual interface has both an IPv4 and IPv6 BGP peering session, you can delete one of the BGP peering sessions \(but not both\)\.

**To delete a BGP peer**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and then choose **View details**\.

1. Under **Peerings,** select the peering that you want to delete and then choose **Delete**\.

1. In the **Remove peering from virtual interface** dialog box, choose **Delete**\.

**To delete a BGP peer using the command line or API**
+ [delete\-bgp\-peer](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-bgp-peer.html) \(AWS CLI\)
+ [DeleteBGPPeer](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteBGPPeer.html) \(AWS Direct Connect API\)