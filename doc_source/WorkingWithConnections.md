# AWS Direct Connect Connections<a name="WorkingWithConnections"></a>

AWS Direct Connect enables you to establish a dedicated network connection between your network and one of the AWS Direct Connect locations\.

To create an AWS Direct Connect connection, you need the following information:

**AWS Direct Connect location**  
Work with a partner in the AWS Partner Network \(APN\) to help you establish network circuits between an AWS Direct Connect location and your data center, office, or colocation environment\. They can also help provide colocation space within the same facility as the location\. For more information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com/directconnect/partners)\.

**Port speed**  
AWS Direct Connect supports these port speeds over single\-mode fiber: 1 Gbps: 1000BASE\-LX \(1310nm\) and 10 Gbps: 10GBASE\-LR \(1310nm\)\.

You cannot change the port speed after you've created the connection request\. To change the port speed, you must create and configure a new connection\.

For port speeds less than 1 Gbps, you cannot request a connection using the console\. Instead, you can contact an APN partner who supports AWS Direct Connect and who can provision a hosted connection for you\.

After you've requested the connection, AWS makes a Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\) available to you to download, or emails you with a request for more information\. If you receive a request for more information, you must respond within 7 days or the connection is deleted\. The LOA\-CFA is the authorization to connect to AWS, and is required by your network provider to order a cross connect for you\. If you do not have equipment in the AWS Direct Connect location, you cannot order a cross connect for yourself there\. Your network provider does this for you\. 

For information about associating a connection with a link aggregation group \(LAG\), see [Associating a Connection with a LAG](associate-connection-with-lag.md)\.

After you've created a connection, create a virtual interface to connect to public and private AWS resources\. For more information, see [AWS Direct Connect Virtual Interfaces](WorkingWithVirtualInterfaces.md)\.

**Topics**
+ [Creating a Connection](create-connection.md)
+ [Viewing Connection Details](viewdetails.md)
+ [Updating a Connection](updateconnection.md)
+ [Deleting Connections](deleteconnection.md)
+ [Accepting a Hosted Connection](acceptSub1Gconnection.md)