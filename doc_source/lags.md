# Link Aggregation Groups<a name="lags"></a>

A link aggregation group \(LAG\) is a logical interface that uses the Link Aggregation Control Protocol \(LACP\) to aggregate multiple 1 gigabit or 10 gigabit connections at a single AWS Direct Connect endpoint, allowing you to treat them as a single, managed connection\. 

You can create a LAG from existing connections, or you can provision new connections\. After you've created the LAG, you can associate existing connections \(whether standalone or part of another LAG\) with the LAG\.

The following rules apply:
+ All connections in the LAG must use the same bandwidth\. The following bandwidths are supported: 1 Gbps and 10 Gbps\.
+ You can have a maximum of 4 connections in a LAG\. Each connection in the LAG counts towards your overall connection limit for the region\.
+ All connections in the LAG must terminate at the same AWS Direct Connect endpoint\. 

When you create a LAG, you can download the Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\) for each new physical connection individually from the AWS Direct Connect console\. For more information, see [Downloading the LOA\-CFA](create-connection.md#create-connection-loa-cfa)\.

All LAGs have an attribute that determines the minimum number of connections in the LAG that must be operational for the LAG itself to be operational\. By default, new LAGs have this attribute set to 0\. You can update your LAG to specify a different value—doing so means that your entire LAG becomes non\-operational if the number of operational connections falls below this threshold\. This attribute can be used to prevent over\-utilization of the remaining connections\. 

All connections in a LAG operate in Active/Active mode\. 

**Note**  
When you create a LAG or associate more connections with the LAG, we may not be able to guarantee enough available ports on a given AWS Direct Connect endpoint\. 

**Topics**
+ [Creating a LAG](create-lag.md)
+ [Updating a LAG](update-lag.md)
+ [Associating a Connection with a LAG](associate-connection-with-lag.md)
+ [Disassociating a Connection From a LAG](disassociate-connection-from-lag.md)
+ [Deleting a LAG](delete-lag.md)