# Creating a Connection<a name="create-connection"></a>

You can create a standalone connection, or you can create a connection to associate with a LAG in your account\. If you associate a connection with a LAG, it's created with the same port speed and location as specified in the LAG\.

If you do not have equipment at an AWS Direct Connect location, first contact an AWS partner at the AWS Partner Network \(APN\)\. For more information, see [APN Partners Supporting AWS Direct Connect](https://aws.amazon.com/directconnect/partners)\.

**To create a new connection**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation bar, select the region in which to connect to AWS Direct Connect\. For more information, see [AWS Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html)\.

1. In the navigation pane, choose **Connections**, **Create Connection**\.

1. In the **Create a Connection** dialog box, enter the following values, and then choose **Create**:  
![\[Create a Connection dialog box\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/create_connection.png)

   1. For **Connection Name**, enter a name for the connection\.

   1. For **LAG Association**, specify whether the connection is standalone, or if it should be associated with a LAG\. If you associate the connection with a LAG, select the LAG ID\. 

   1. For **Location**, select the appropriate AWS Direct Connect location\.

   1. If applicable, for **Sub Location**, choose the floor closest to you or your network provider\. This option is only available if the location has meet\-me rooms \(MMRs\) in multiple floors of the building\.

   1. Select the appropriate port speed that is compatible with your existing network\.

**To create a connection using the command line or API**

+ [create\-connection](http://docs.aws.amazon.com/cli/latest/reference/directconnect/create-connection.html) \(AWS CLI\)

+ [CreateConnection](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateConnection.html) \(AWS Direct Connect API\)

## Downloading the LOA\-CFA<a name="create-connection-loa-cfa"></a>

After AWS has processed your connection request, you can download the Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\)\. 

**To download the LOA\-CFA**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Connections**\.

1. Choose **Actions**, **Download LOA\-CFA**\. 
**Note**  
If the link is not enabled, the LOA\-CFA is not yet available for you to download\. Check your email for a request for more information\. If it's still unavailable, or you haven't received an email after 72 hours, contact [AWS Support](https://aws.amazon.com/support/createCase)\.

1. In the dialog box, optionally enter the name of your provider to have it appear with your company name as the requester in the LOA\-CFA\. Choose **Download**\. The LOA\-CFA is downloaded to your computer as a PDF file\.

1. Send the LOA\-CFA to your network provider or colocation provider so that they can order a cross connect for you\. The contact process can vary for each colocation provider\. For more information, see [Requesting Cross Connects at AWS Direct Connect Locations](Colocation.md)\. 

The LOA\-CFA expires after 90 days\. If your connection is not up after 90 days, we send you an email alerting you that the LOA\-CFA has expired\. To refresh the LOA\-CFA with a new issue date, download it again from the AWS Direct Connect console\. If you do not take any action, we delete the connection\.

**Note**  
Port\-hour billing starts 90 days after you created the connection, or after the connection between your router and the AWS Direct Connect endpoint is established, whichever comes first\. For more information, see [AWS Direct Connect Pricing](https://aws.amazon.com/directconnect/pricing/)\. If you no longer want the connection after you've reissued the LOA\-CFA, you must delete the connection yourself\. For more information, see [Deleting a Connection](deleteconnection.md)\.

**To download the LOA\-CFA using the command line or API**

+ [describe\-loa](http://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-loa.html) \(AWS CLI\)

+ [DescribeLoa](http://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeLoa.html) \(AWS Direct Connect API\)