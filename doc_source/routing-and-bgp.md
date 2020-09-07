# Routing policies and BGP communities<a name="routing-and-bgp"></a>

AWS Direct Connect applies inbound \(from your on\-premises data center\) and outbound \(from your AWS Region\) routing policies for a public AWS Direct Connect connection\. You can also use Border Gateway Protocol \(BGP\) community tags on routes advertised by Amazon and apply BGP community tags on the routes you advertise to Amazon\.

## Public virtual interface routing policies<a name="routing-policies"></a>

If you're using AWS Direct Connect to access public AWS services, you must specify the public IPv4 prefixes or IPv6 prefixes to advertise over BGP\. 

The following inbound routing policies apply:
+ You must own the public prefixes and they must be registered as such in the appropriate regional internet registry\.
+ Traffic must be destined to Amazon public prefixes\. Transitive routing between connections is not supported\.
+ AWS Direct Connect performs inbound packet filtering to validate that the source of the traffic originated from your advertised prefix\. 

The following outbound routing policies apply:
+ AS\_PATH is used to determine the routing path, and AWS Direct Connect is the preferred path for traffic sourced from Amazon\. Only public ASNs are used internally for route selection\.
+ AWS Direct Connect advertises all local and remote AWS Region prefixes where available and includes on\-net prefixes from other AWS non\-Region points of presence \(PoP\) where available; for example, CloudFront and Route 53\.
+ AWS Direct Connect advertises prefixes with a minimum path length of 3\.
+ AWS Direct Connect advertises all public prefixes with the well\-known `NO_EXPORT` BGP community\.
+ If you have multiple AWS Direct Connect connections, you can adjust the load\-sharing of inbound traffic by advertising prefixes with similar path attributes\.
+ The prefixes advertised by AWS Direct Connect must not be advertised beyond the network boundaries of your connection\. For example, these prefixes must not be included in any public internet routing table\.

## Private virtual interface and transit virtual interface routing policies<a name="private-routing-policies"></a>

### All Private virtual interfaces or transit virtual interfaces terminate on a Direct Connect gateway<a name="direct-connect-gateway"></a>

Consider the configuration where the AWS Direct Connect location 1 home Region is the same as the VPC 1 home Region\. The AWS Direct Connect location 2 and AWS Direct Connect location 3 are homed to Regions that are different from the VPC 1 home Region\. In this case, there are no community tags on the routes that are advertised from the on\-premises location to location 1\.

### All Private virtual interfaces or transit virtual interfaces terminate on a virtual private gateway<a name="virtual-private-gateway"></a>

Consider the configuration where the AWS Direct Connect location (east) home Region is the same as the VPC home Region (us-east-1). There is a redundant AWS Direct Connect location in a different Region (west). There are two private VIFs from AWS Direct Connect location (east) to the Direct Connect gateway. There is one private VIF from the AWS Direct Connect location (west) to the Direct Connect gateway. The VIFs have the following configurations:

    Private VIF A (in us-east-1) advertises 172.16.0.0/16 and has an AS_PATH of 65001, 65001, 65001
    Private VIF B (in us-east-1) advertises 172.16.0.0/16 and has an AS_PATH of 65001, 65001
    Private VIF C (in us-west-1) advertises 172.16.0.0/16 and has an AS_PATH of 65001\.

In this scenario, even though Private VIF C has the shortest AS_PATH, traffic is routed over Private VIF B because it is in the same Region as the VPC, and therefore has the least cost.

If you change the configuration of Private VIF C to the following configuration, routes that fall in to the VIF C CIDR range use VIF C because it has the longest prefix match.

    Private VIF C (in west) advertises 172.16.0.0/24 and has an AS_PATH of 65001\.

## Public virtual interface BGP communities<a name="bgp-communities"></a>

AWS Direct Connect supports scope BGP community tags and the `NO_EXPORT` BGP community tag to help control the scope \(Regional or global\) and route preference of traffic on public virtual interfaces\.

### Scope BGP communities<a name="scope-bgp-communities"></a>

You can apply BGP community tags on the public prefixes that you advertise to Amazon to indicate how far to propagate your prefixes in the Amazon network, for the local AWS Region only, all Regions within a continent, or all public Regions\.

You can use the following BGP communities for your prefixes:
+ `7224:9100`—Local AWS Region
+ `7224:9200`—All AWS Regions for a continent
  + North America–wide
  + Asia Pacific
  + Europe, the Middle East and Africa
+ `7224:9300`—Global \(all public AWS Regions\)

**Note**  
If you do not apply any community tags, prefixes are advertised to all public AWS Regions \(global\) by default\.  
Prefixes that are marked with the same communities, and have identical AS\_PATH attributes are candidates for multi\-pathing\.

The communities `7224:1` – `7224:65535` are reserved by AWS Direct Connect\.

AWS Direct Connect applies the following BGP communities to its advertised routes:
+ `7224:8100`—Routes that originate from the same AWS Region in which the AWS Direct Connect point of presence is associated\.
+ `7224:8200`—Routes that originate from the same continent with which the AWS Direct Connect point of presence is associated\.
+ No tag—Global \(all public AWS Regions\)\.

Communities that are not supported for an AWS Direct Connect public connection are removed\.

### `NO_EXPORT` BGP community<a name="no-export-bgp-communities"></a>

The `NO_EXPORT` BGP community tag is supported for public virtual interfaces, private virtual interfaces, and transit virtual interfaces\.

AWS Direct Connect also provides BGP community tags on advertised Amazon routes\. If you use AWS Direct Connect to access public AWS services, you can create filters based on these community tags\. 

## Private virtual interface and transit virtual interface BGP communities<a name="bgp-communities-private-transit"></a>

AWS Direct Connect supports local preference BGP community tags to help control the route preference of traffic on private virtual interfaces and transit virtual interfaces\.

### Local preference BGP communities<a name="local-pref-bgp-communities"></a>

You can use local preference BGP community tags to achieve load balancing and route preference for incoming traffic to your network\. For each prefix that you advertise over a BGP session, you can apply a community tag to indicate the priority of the associated path for returning traffic\. 

The following local preference BGP community tags are supported:
+ `7224:7100`—Low preference
+ `7224:7200`—Medium preference
+ `7224:7300`—High preference

Local preference BGP community tags are mutually exclusive\. To load balance traffic across multiple AWS Direct Connect connections, apply the same community tag across the prefixes for the connections\. To support failover across multiple AWS Direct Connect connections, apply a community tag with a higher preference to the prefixes for the primary or active virtual interface\. For example set the BGP community tags for your primary or active virtual interfaces to 7224:7300 \(high preference\)\.

Local preference BGP community tags are evaluated before any AS\_PATH attribute, and are evaluated in order from lowest to highest preference \(where highest preference is preferred\)\.

If you do not specify local preference community tags, the default local preference is based on the distance to the AWS Direct Connect location\.

## Virtual interface BGP community tags<a name="bgp-communities-interfaces"></a>

You can use this traffic engineering technique for private and transit virtual interface BGP advertisements to achieve an active/passive load distribution over redundant virtual interfaces\. An active virtual interface has 7224:7300 \(High preference\) as the tag and a Passive has 7224:7100 \(Low preference\) as the tag\.
