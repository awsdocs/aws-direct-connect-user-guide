# AWS Direct Connect connections<a name="WorkingWithConnections"></a>

AWS Direct Connect enables you to establish a dedicated network connection between your network and one of the AWS Direct Connect locations\.

There are two types of connections:
+ Dedicated Connection: A physical Ethernet connection associated with a single customer\. Customers can request a dedicated connection through the AWS Direct Connect console, the CLI, or the API\.
+ Hosted Connection: A physical Ethernet connection that an AWS Direct Connect Partner provisions on behalf of a customer\. Customers request a hosted connection by contacting a partner in the AWS Direct Connect Partner Program, who provisions the connection\. 

## Dedicated connections<a name="dedicated_connection"></a>

To create an AWS Direct Connect dedicated connection, you need the following information:

**AWS Direct Connect location**  
Work with a partner in the AWS Direct Connect Partner Program to help you establish network circuits between an AWS Direct Connect location and your data center, office, or colocation environment\. They can also help provide colocation space within the same facility as the location\. For more information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com/directconnect/partners)\.

**Port speed**  
The possible values are 1 Gbps, 10 Gbps, and 100 Gbps\. 

You cannot change the port speed after you create the connection request\. To change the port speed, you must create and configure a new connection\.

After you request the connection, we make a Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\) available to you to download, or emails you with a request for more information\. If you receive a request for more information, you must respond within 7 days or the connection is deleted\. The LOA\-CFA is the authorization to connect to AWS, and is required by your network provider to order a cross connect for you\. If you do not have equipment in the AWS Direct Connect location, you cannot order a cross connect for yourself there\. 

The following operations are available for dedicated connections:
+ [Create a connection](create-connection.md)
+ [View your connection details](viewdetails.md)
+ [Update a connection](updateconnection.md)
+ [Associate a MACsec CKN/CAK with a connection](associate-key-connection.md)
+ [Remove the association between a MACsec secret key and a connection](disassociate-key-connection.md)
+ [Delete connections](deleteconnection.md)

You can add a dedicated connection to a link aggregation group \(LAG\) allowing you to treat multiple connections as a single one\. For information, see [Associate a connection with a LAG](associate-connection-with-lag.md)\.

After you create a connection, create a virtual interface to connect to public and private AWS resources\. For more information, see [AWS Direct Connect virtual interfaces](WorkingWithVirtualInterfaces.md)\.

## Hosted connections<a name="hosted_connection"></a>

To create an AWS Direct Connect hosted connection, you need the following information:

**AWS Direct Connect location**  
Work with an AWS Direct Connect Partner in the AWS Direct Connect Partner Program to help you establish network circuits between an AWS Direct Connect location and your data center, office, or colocation environment\. They can also help provide colocation space within the same facility as the location\. For more information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com/directconnect/partners)\.

**Port speed**  
For hosted connections, the possible values are 50 Mbps, 100 Mbps, 200 Mbps, 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, and 10 Gbps\. Note that only those AWS Direct Connect partners who have met specific requirements may create a 1 Gbps, 2 Gbps, 5 Gbps or 10 Gbps hosted connection\.

You cannot change the port speed after you create the connection request\. To change the port speed, you must create and configure a new connection\.

AWS uses traffic policing on hosted connections, which means that when the traffic rate reaches the configured maximum rate, excess traffic is dropped\. This might result in bursty traffic having a lower throughput than non\-bursty traffic\.

The following operations are available for hosted connections:
+ [Create a connection](create-connection.md)

  After the AWS Direct Connect Partner configures the connection, it appears in the **Connections** pane in the AWS Direct Connect console\. You must accept the hosted connection before you can use it\. For more information, see [Accept a hosted connection](accept-hosted-connection.md)\.
+ [View your connection details](viewdetails.md)
+ [Update a connection](updateconnection.md)
+ [Delete connections](deleteconnection.md)

 After you accept a connection, create a virtual interface to connect to public and private AWS resources\. For more information, see [AWS Direct Connect virtual interfaces](WorkingWithVirtualInterfaces.md)\.