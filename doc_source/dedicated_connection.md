# Dedicated connections<a name="dedicated_connection"></a>

To create an AWS Direct Connect dedicated connection, you need the following information:

**AWS Direct Connect location**  
Work with a partner in the AWS Direct Connect Partner Program to help you establish network circuits between an AWS Direct Connect location and your data center, office, or colocation environment\. They can also help provide colocation space within the same facility as the location\. For more information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com/directconnect/partners)\.

**Port speed**  
The possible values are 1 Gbps, 10 Gbps, and 100 Gbps\. 

You cannot change the port speed after you create the connection request\. To change the port speed, you must create and configure a new connection\.

You can create a connection using either the Connection wizard or create a Classic connection\. Using the Connection wizard you can set up connections using resiliency recommendations\. The wizard is recommended if you're setting up connections for the first time\. If you prefer, you can use Class to create connections one\-at\-a\-time\. Classic is recommended if you've already got an existing setup that you want to add connections to\. You can create a standalone connection, or you can create a connection to associate with a LAG in your account\. If you associate a connection with a LAG, it's created with the same port speed and location that is specified in the LAG\.

After you request the connection, we make a Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\) available to you to download, or emails you with a request for more information\. If you receive a request for more information, you must respond within 7 days or the connection is deleted\. The LOA\-CFA is the authorization to connect to AWS, and is required by your network provider to order a cross connect for you\. If you do not have equipment in the AWS Direct Connect location, you cannot order a cross connect for yourself there\. 

The following operations are available for dedicated connections:
+ [Create a connection using the Connection wizard](#create-connection)
+ [Create a Classic connection](#connection-classic)
+ [View your connection details](viewdetails.md)
+ [Update a connection](updateconnection.md)
+ [Associate a MACsec CKN/CAK with a connection](associate-key-connection.md)
+ [Remove the association between a MACsec secret key and a connection](disassociate-key-connection.md)
+ [Delete connections](deleteconnection.md)

You can add a dedicated connection to a link aggregation group \(LAG\) allowing you to treat multiple connections as a single one\. For information, see [Associate a connection with a LAG](associate-connection-with-lag.md)\.

After you create a connection, create a virtual interface to connect to public and private AWS resources\. For more information, see [AWS Direct Connect virtual interfaces](WorkingWithVirtualInterfaces.md)\.

If you do not have equipment at an AWS Direct Connect location, first contact an AWS Direct Connect Partner at the AWS Direct Connect Partner Program\. For more information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com/directconnect/partners)\.

If you want to create a connection that uses MAC Security \(MACsec\), review the prerequisites before you create the connection\. For more information, see [MACsec prerequisites ](direct-connect-mac-sec-getting-started.md#mac-sec-prerequisites)\.

## Create a connection using the Connection wizard<a name="create-connection"></a>

This section describes creating a connection using the Connection wizard\. If you prefer to create a Classic connection, see the steps at [Step 2: Request an AWS Direct Connect dedicated connection](getting_started.md#ConnectionRequest)\.

**To create a Connection wizard connection**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Connections**, and then choose **Create connection**\.

1. On the **Create Connection** page, under **Connection ordering type**, choose **Connection wizard**\.

1. Choose a **Resiliency Level** for your network connections\. A resiliency level can be one of the following:
   + **Maximum Resiliency**
   + **High Resiliency**
   + **Development and Test**

   For descriptions and more detailed information about these resiliency levels, see [Using the AWS Direct Connect Resiliency Toolkit to get started](resiliency_toolkit.md)\.

1. Choose **Next**\.

1. On the **Configure connections** page, provide the following details\.

   1. From the **Bandwidth** drop\-down list, choose the bandwidth required for the connection\. This can be anywhere from **1Gbps** to **100Gbps**\.

   1. For **Location**, choose the appropriate AWS Direct Connect location, and then choose the **First location service provider**, select the service provider providing connectivity for the connection at this location\.

   1. For **Second location**, choose the appropriate AWS Direct Connect at the second location, and then choose the **Second location service provider**, select the service provider providing connectivity for the connection at this second location\.

   1. \(Optional\) Configure MAC security \(MACsec\) for the connection\. Under **Additional Settings**, select **Request a MACsec capable port**\.

      MACsec is only available on dedicated connections\.

   1. \(Optional\) Choose **Add tag** to add key/value pairs to further help identify this connection\.
      + For **Key**, enter the key name\.
      + For **Value**, enter the key value\.

      To remove an existing tag, choose the tag and then choose **Remove tag**\. You can't have empty tags\.

1. Choose **Next**\.

1. On the **Review and create page**, verify the connection\. This page also displays estimated costs for port usage and additional data transfer charges\. 

1. Choose **Create**\.

1. Download your Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\), For more information, see [Download the LOA\-CFA](#create-connection-loa-cfa)\.

Use one of the following commands\.
+ [create\-connection](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-connection.html) \(AWS CLI\)
+ [CreateConnection](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateConnection.html) \(AWS Direct Connect API\)

## Create a Classic connection<a name="connection-classic"></a>

For dedicated connections, you can submit a connection request using the AWS Direct Connect console\. For hosted connections, work with an AWS Direct Connect Partner to request a hosted connection\. Ensure that you have the following information:
+ The port speed that you require\. You cannot change the port speed after you create the connection request\. 
+ The AWS Direct Connect location at which the connection is to be terminated\.

**Note**  
You cannot use the AWS Direct Connect console to request a hosted connection\. Instead, contact an AWS Direct Connect Partner, who can create a hosted connection for you, which you then accept\. Skip the following procedure and go to [ Accept your hosted connection](getting_started.md#get-started-accept-hosted-connection)\.

**To create a new AWS Direct Connect connection**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. On the **AWS Direct Connect** screen, under **Get started**, choose **Create a connection**\.

1. Choose **Classic**\.

1. For **Name**, enter a name for the connection\.

1. For **Location**, select the appropriate AWS Direct Connect location\.

1.  If applicable, for **Sub Location**, choose the floor closest to you or your network provider\. This option is only available if the location has meet\-me rooms \(MMRs\) in multiple floors of the building\.

1.  For **Port Speed**, choose the connection bandwidth\.

1.  For **On\-premises**, select **Connect through an AWS Direct Connect partner** when you use this connection to connect to your data center\.

1.  For **Service provider**, select the AWS Direct Connect Partner\. If you use a partner that is not in the list, select **Other**\.

1.  If you selected **Other** for **Service provider**, for** Name of other provider**, enter the name of the partner that you use\.

1. \(Optional\) Choose **Add tag** to add key/value pairs to further help identify this connection\.
   +  For **Key**, enter the key name\. 
   + For **Value**, enter the key value\.

   To remove an existing tag, choose the tag and then choose **Remove tag**\. You can't have empty tags\.

1. Choose **Create Connection**\.

It can take up to 72 hours for AWS to review your request and provision a port for your connection\. During this time, you might receive an email with a request for more information about your use case or the specified location\. The email is sent to the email address that you used when you signed up for AWS\. You must respond within 7 days or the connection is deleted\.

For more information, see [AWS Direct Connect connections](WorkingWithConnections.md)\.

## Download the LOA\-CFA<a name="create-connection-loa-cfa"></a>

After we have processed your connection request, you can download the LOA\-CFA\. If the link is enabled, the LOA\-CFA is not yet available for you to download\. Check your email for a request for information\. 

 

Billing automatically starts when the port is active or 90 days after the LOA has been issued, whichever comes first\. You can avoid billing charges by deleting the port prior to activation or within 90 days of the LOA being issued\.

If your connection is not up after 90 days, and the LOA\-CFA has not been issued, we will send you an email alerting you that the port will be deleted in 10 days\. If you fail to activate the port within the additional 10 day period, the port will automatically be deleted and you'll need to restart the port creation process\.

**Note**  
For more information about pricing, see [AWS Direct Connect Pricing](https://aws.amazon.com/directconnect/pricing/)\. If you no longer want the connection after you have reissued the LOA\-CFA, you must delete the connection yourself\. For more information, see [Delete connections](deleteconnection.md)\.

------
#### [ Console ]

**To download the LOA\-CFA**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Connections**\.

1. Select the connection, and then choose **View details**\.

1. Choose **Download LOA\-CFA**\. 
**Note**  
If the link is not enabled, the LOA\-CFA is not yet available for you to download\. A Support case will be created requesting additional information\. Once you've responded to the request, and the request processed, the LOA\-CFA will be available for download\. If it's still unavailable, contact [AWS Support](https://aws.amazon.com/support/createCase)\.

1. Send the LOA\-CFA to your network provider or colocation provider so that they can order a cross connect for you\. The contact process can vary for each colocation provider\. For more information, see [Requesting cross connects at AWS Direct Connect locations](Colocation.md)\.

------
#### [ Command line ]

**To download the LOA\-CFA using the command line or API**
+ [describe\-loa](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-loa.html) \(AWS CLI\)
+ [DescribeLoa](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeLoa.html) \(AWS Direct Connect API\)

------