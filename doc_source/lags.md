# Link aggregation groups<a name="lags"></a>

You can use multiple connections for redundancy\. A link aggregation group \(LAG\) is a logical interface that uses the Link Aggregation Control Protocol \(LACP\) to aggregate multiple connections at a single AWS Direct Connect endpoint, allowing you to treat them as a single, managed connection\. LAGs streamline configuration because the LAG configuration applies to all connections in the group\.

In the following diagram, you have four connections, with two connections to each location\. You can create a LAG for the connections that terminate in the same location, and then use the two LAGs instead of the four connections for configuration and management\.

![\[Link Aggregation Group\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/LAG_description.png)

You can create a LAG from existing connections, or you can provision new connections\. After you've created the LAG, you can associate existing connections \(whether standalone or part of another LAG\) with the LAG\.

The following rules apply:
+ All connections must be dedicated connections and have a port speed of 1 Gbps, 10 Gbps, or 100 Gbps\. 
+ All connections in the LAG must use the same bandwidth\.
+ You can have a maximum of two 100G connections, or four connections with a port speed less than 100G in a LAG\. Each connection in the LAG counts towards your overall connection limit for the Region\. 
+ All connections in the LAG must terminate at the same AWS Direct Connect endpoint\. 

When you create a LAG, you can download the Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\) for each new physical connection individually from the AWS Direct Connect console\. For more information, see [Download the LOA\-CFA](create-connection.md#create-connection-loa-cfa)\.

All LAGs have an attribute that determines the minimum number of connections in the LAG that must be operational for the LAG itself to be operational\. By default, new LAGs have this attribute set to 0\. You can update your LAG to specify a different value—doing so means that your entire LAG becomes non\-operational if the number of operational connections falls below this threshold\. This attribute can be used to prevent over\-utilization of the remaining connections\. 

All connections in a LAG operate in Active/Active mode\. 

**Note**  
When you create a LAG or associate more connections with the LAG, we may not be able to guarantee enough available ports on a given AWS Direct Connect endpoint\. 

## MACsec considerations<a name="lag-macsec-considerations"></a>

Take the following into consideration when you want to configure MACsec on LAGs:
+ When you create a LAG from existing connections, we disassociate all of the MACsec keys from the connections\. Then we add the connections to the LAG, and associate the LAG MACsec key with the connections\.
+ When you associate an existing connection to a LAG, the MACsec keys that are currently associated with the LAG are associated with the connection\. Therefore, we disassociate the MACsec keys from the connection, add the connection to the LAG, and then associate the LAG MACsec key with the connection\.