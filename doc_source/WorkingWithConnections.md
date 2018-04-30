# Connections<a name="WorkingWithConnections"></a>

To create an AWS Direct Connect connection, you need the following information:

+ **AWS Direct Connect location**

  Work with a partner in the AWS Partner Network \(APN\) to help you establish network circuits between an AWS Direct Connect location and your data center, office, or colocation environment, or to provide colocation space within the same facility as the AWS Direct Connect location\. For the list of AWS Direct Connect partners who belong to the APN, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com/directconnect/partners)\.

+ **Port speed**

  AWS Direct Connect supports two port speeds: 1 Gbps: 1000BASE\-LX \(1310nm\) over single\-mode fiber and 10 Gbps: 10GBASE\-LR \(1310nm\) over single\-mode fiber\. You cannot change the port speed after you've created the connection request\. If you need to change the port speed, you must create and configure a new connection\. 

  For port speeds less than 1 Gbps, you cannot request a connection using the console\. Instead, you can contact an APN partner who supports AWS Direct Connect and who can provision a hosted connection for you\.

After you've requested the connection, AWS makes a Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\) available to you to download, or emails you with a request for more information\. If you receive a request for more information, you must respond within 7 days or the connection is deleted\. The LOA\-CFA is the authorization to connect to AWS, and is required by your network provider to order a cross connect for you\. You cannot order a cross connect for yourself in the AWS Direct Connect location if you do not have equipment there; your network provider does this for you\. 

For information about associating a connection with a link aggregation group \(LAG\), see [Associating a Connection with a LAG](associate-connection-with-lag.md)\.

After you've created a connection, create a virtual interface to connect to public and private AWS resources\. For more information, see [Virtual Interfaces](WorkingWithVirtualInterfaces.md)\.


+ [Creating a Connection](create-connection.md)
+ [Viewing Connection Details](viewdetails.md)
+ [Deleting a Connection](deleteconnection.md)
+ [Accepting a Hosted Connection](acceptSub1Gconnection.md)