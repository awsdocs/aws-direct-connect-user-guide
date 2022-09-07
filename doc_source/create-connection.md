# Create a connection<a name="create-connection"></a>

You can create a standalone connection, or you can create a connection to associate with a LAG in your account\. If you associate a connection with a LAG, it's created with the same port speed and location that is specified in the LAG\.

If you do not have equipment at an AWS Direct Connect location, first contact an AWS Direct Connect Partner at the AWS Direct Connect Partner Program\. For more information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com/directconnect/partners)\.

If you want to create a connection that uses MAC Security \(MACsec\), review the prerequisites before you create the connection\. For more information, see [MACsec prerequisites ](direct-connect-mac-sec-getting-started.md#mac-sec-prerequisites)\.

------
#### [ Console ]

**To create a new connection**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. On the **AWS Direct Connect** screen, under **Get started**, choose **Create a connection**\.

1. On the **Create Connection** pane, under **Connection settings,** do the following:

   1. For **Name**, enter a name for the connection\.

   1. For **Location**, select the appropriate AWS Direct Connect location\.

   1. If applicable, for **Sub Location**, choose the floor closest to you or your network provider\. This option is only available if the location has meet\-me rooms \(MMRs\) in multiple floors of the building\.

   1. For **Port Speed**, choose the connection bandwidth\.

   1. For **On\-premises**, select **Connect through an AWS Direct Connect partner** when you use this connection to connect to your data center\.

   1. \(Optional\) Configure MAC security \(MACsec\) for the connection\. Under **Additional Settings**, select **Request a MACsec capable port**\.

      MACsec is only available on dedicated connections\.

   1. 

      1. \(Optional\) Add or remove a tag\.

         \[Add a tag\] Choose **Add tag** and do the following:
         + For **Key**, enter the key name\.
         + For **Value**, enter the key value\.

         \[Remove a tag\] Next to the tag, choose **Remove tag**\.

1. Choose **Create Connection**\.

------
#### [ Command line ]

Use one of the following commands\.
+ [create\-connection](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-connection.html) \(AWS CLI\)
+ [CreateConnection](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateConnection.html) \(AWS Direct Connect API\)

------

## Download the LOA\-CFA<a name="create-connection-loa-cfa"></a>

After we have processed your connection request, you can download the LOA\-CFA\. If the link is enabled, the LOA\-CFA is not yet available for you to download\. Check your email for a request for information\. 

 

Billing automatically starts when the port is active or 90 days after the LOA has been issued, whichever comes first\. You can avoid billing charges by deleting the port prior to activation or within 90 days of the LOA being issued\.

If your connection is not up after 90 days, and the LOA\-CFA has not been issued, we will send you an email alerting you that the port will be deleted in 10 days\. If you fail to activate the port within the additional 10 day period, the port will automatically be deleted and you'll need to restart the port creation process\.

**Note**  
For more information about pricing, see [AWS Direct Connect Pricing](https://aws.amazon.com/directconnect/pricing/)\. If you no longer want the connection after you have reissued the LOA\-CFA, you must delete the connection yourself\. For more information, see [Delete connections](deleteconnection.md)\.

------
#### [ Console ]

**To download the LOA\-CFA**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

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