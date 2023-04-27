# Hosted connections<a name="hosted_connection"></a>

To create an AWS Direct Connect hosted connection, you need the following information:

**AWS Direct Connect location**  
Work with an AWS Direct Connect Partner in the AWS Direct Connect Partner Program to help you establish network circuits between an AWS Direct Connect location and your data center, office, or colocation environment\. They can also help provide colocation space within the same facility as the location\. For more information, see [AWS Direct Connect Delivery Partners](https://aws.amazon.com/directconnect/partners)\.  
You can't request a hosted connection through the AWS Direct Connect console\. However, an AWS Direct Connect Partner can create and configure a hosted connection for you\. Once configured, the connection appears in the **Connections** pane in the console\.   
You must accept the hosted connection before you can use it\. For more information, see [Accept a hosted connection](#accept-hosted-connection)\.

**Port speed**  
For hosted connections, the possible values are 50 Mbps, 100 Mbps, 200 Mbps, 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, and 10 Gbps\. Note that only those AWS Direct Connect partners who have met specific requirements may create a 1 Gbps, 2 Gbps, 5 Gbps or 10 Gbps hosted connection\.

You cannot change the port speed after you create the connection request\. To change the port speed, you must create and configure a new connection\.

AWS uses traffic policing on hosted connections, which means that when the traffic rate reaches the configured maximum rate, excess traffic is dropped\. This might result in bursty traffic having a lower throughput than non\-bursty traffic\.

The following console operations are available after you've requested a hosted connection and accepted it:
+ [View your connection details](viewdetails.md)
+ [Update a connection](updateconnection.md)
+ [Delete connections](deleteconnection.md)

 After you accept a connection, create a virtual interface to connect to public and private AWS resources\. For more information, see [AWS Direct Connect virtual interfaces](WorkingWithVirtualInterfaces.md)\.

## Accept a hosted connection<a name="accept-hosted-connection"></a>

If you are interested in purchasing a hosted connection, you must contact an AWS Direct Connect Partner in the AWS Direct Connect Partner Program\. The partner provisions the connection for you\. After the connection is configured, it appears in the **Connections** pane in the AWS Direct Connect console\.

Before you can begin using a hosted connection, you must accept the connection\.

------
#### [ Console ]

1. Open the **AWS Direct Connect** console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Connections**\.

1. Select the hosted connection and choose **View details**\.

1. Select the confirmation check box and choose **Accept**\.

------
#### [ Command line ]

**To accept a hosted connection using the command line or API**
+ [confirm\-connection](https://docs.aws.amazon.com/cli/latest/reference/directconnect/confirm-connection.html) \(AWS CLI\)
+ [ConfirmConnection](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_ConfirmConnection.html) \(AWS Direct Connect API\)

------