# Associating a Transit Gateway Across Accounts<a name="multi-account-associate-tgw"></a>

You can associate a Direct Connect gateway with a transit gateway that's in a different AWS account\. The owner of the transit gateway creates an *association proposal* and the owner of the Direct Connect gateway must accept the association proposal\.

An association proposal can contain prefixes that will be allowed from the transit gateway\. The owner of the Direct Connect gateway can optionally override any requested prefixes in the association proposal\.

You can only associate a Direct Connect gateway and transit gateway when the account that owns the Direct Connect gateway and the account that owns the transit gateway have the same payer ID\.

Consider this scenario of a Direct Connect gateway owner \(Account Z\) who owns the Direct Connect gateway\. Account A owns the transit gateway and wants to use the Direct Connect gateway\. Account Z accepts the association proposals and can optionally update the prefixes that are allowed from Account A's transit gateway\. After Account Z accepts the proposals, The VPCs attached to the transit gateway can route traffic from the transit gateway to the Direct Connect gateway\. Account Z also owns the routing to the customers because Account Z owns the gateway\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/direct-connect-ma-tgw.png)

## Allowed Prefixes<a name="allowed-prefixes-transit-gateway"></a>

For a transit gateway, association, you provision the allowed prefixes list on the Direct Connect gateway\. The list is used to route traffic from on\-premises to AWS into the transit gateway even if the VPCs attached to the transit gateway don not have assigned CIDRs\. Prefixes in the Direct Connect gateway allowed prefix list originate on the Direct Connect gateway and are advertised to the on\-premises network\. For more information on how allowed prefixes interact with transit gateways and virtual private gateways, see [Allowed Prefixes Interactions](allowed-to-prefixes.md)\.

**Topics**
+ [Allowed Prefixes](#allowed-prefixes-transit-gateway)
+ [Creating a Transit Gateway Association Proposal](#multi-account-tgw-create-proposal)
+ [Accepting or Rejecting a Transit Gateway Association Proposal](#multi-account-tgw-accept-reject-proposal)
+ [Updating the Allowed Prefixes for a Transit Gateway Association](#multi-account-tgw-update-proposal-routes)
+ [Deleting a Transit Gateway Association Proposal](#multi-account-tgw-delete-proposal)

## Creating a Transit Gateway Association Proposal<a name="multi-account-tgw-create-proposal"></a>

If you own the transit gateway, you must create the association proposal\. The transit gateway must be attached to a VPC or VPN in your AWS account\. The owner of the Direct Connect gateway must share the ID of the Direct Connect gateway and the ID of its AWS account\. After you create the proposal, the owner of the Direct Connect gateway must accept it in order for you to gain access to the on\-premises network over AWS Direct Connect\.

**To create an association proposal**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Transit gateways** and then select the virtual private gateway\.

1. Choose **View details**\.

1. Choose **Direct Connect gateway associations** and then choose **Associate Direct Connect gateway**\.

1. Under **Association account type**, for **Account owner**, choose **Another account**\.

1. For **Direct Connect gateway owner**, enter the ID of the AWS account that owns the Direct Connect gateway\.

1. For **Direct Connect gateway owner**, enter the ID of the AWS account that owns the Direct Connect gateway\.

1. Under **Association settings**, do the following:

   1. For **Direct Connect gateway ID**, enter the ID of the Direct Connect gateway\.

   1. For **Virtual interface owner**, enter the ID of the AWS account that owns the virtual interface for the association\.

   1. \(Optional\) To specify a list of prefixes to be allowed from the transit gateway, add the prefixes to **Allowed prefixes**, separating them using commas\.

1. Choose **Associate Direct Connect gateway**\.

**To create an association proposal using the command line or API**
+ [create\-direct\-connect\-gateway\-association\-proposal](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-direct-connect-gateway-association-proposal.html) \(AWS CLI\)
+ [CreateDirectConnectGatewayAssociationProposal](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateDirectConnectGatewayAssociationProposal.html) \(AWS Direct Connect API\)

## Accepting or Rejecting a Transit Gateway Association Proposal<a name="multi-account-tgw-accept-reject-proposal"></a>

If you own the Direct Connect gateway, you must accept the association proposal in order to create the association\. You also have the option of rejecting the association proposal\.

**To accept an association proposal**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect gateways**\.

1. Select the Direct Connect gateway with pending proposals and then choose **View details**\.

1. On the **Pending proposals** tab, select the proposal and then choose **Accept proposal**\.

1. \(Optional\) To specify a list of prefixes to be allowed from the transit gateway, add the prefixes to **Allowed prefixes**, separating them using commas\.

1. Choose **Accept proposal**\.

**To reject an association proposal**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect gateways**\.

1. Select the Direct Connect gateway with pending proposals and then choose **View details**\.

1. On the **Pending proposals** tab, select the transit gateway and then choose **Reject proposal**\.

1. In the **Reject proposal** dialog box, enter Delete and then choose **Reject proposal**\.

**To view association proposals using the command line or API**
+ [describe\-direct\-connect\-gateway\-association\-proposals](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-association-proposals.htm) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAssociationProposals](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAssociationProposals.html) \(AWS Direct Connect API\)

**To accept an association proposal using the command line or API**
+ [accept\-direct\-connect\-gateway\-association\-proposal](https://docs.aws.amazon.com/cli/latest/reference/directconnect/accept-direct-connect-gateway-association-proposal.html) \(AWS CLI\)
+ [AcceptDirectConnectGatewayAssociationProposal](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AcceptDirectConnectGatewayAssociationProposal.html) \(AWS Direct Connect API\)

**To reject an association proposal using the command line or API**
+ [delete\-direct\-connect\-gateway\-association\-proposal](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway-association-proposal.html) \(AWS CLI\)
+ [DeleteDirectConnectGatewayAssociationProposal](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGatewayAssociationProposal.html) \(AWS Direct Connect API\)

## Updating the Allowed Prefixes for a Transit Gateway Association<a name="multi-account-tgw-update-proposal-routes"></a>

You can update the prefixes that are allowed from the transit gateway over the Direct Connect gateway\.

If you're the owner of the transit gateway, [create a new association proposal](#multi-account-tgw-create-proposal) for the same Direct Connect gateway and virtual private gateway, specifying the prefixes to allow\.

If you're the owner of the Direct Connect gateway, update the allowed prefixes when you [accept the association proposal](#multi-account-tgw-accept-reject-proposal) or update the allowed prefixes for an existing association as follows\.

**To update the allowed prefixes for an existing association using the command line or API**
+ [update\-direct\-connect\-gateway\-association](https://docs.aws.amazon.com/cli/latest/reference/directconnect/update-direct-connect-gateway-association.html) \(AWS CLI\)
+ [UpdateDirectConnectGatewayAssociation](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_UpdateDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)

## Deleting a Transit Gateway Association Proposal<a name="multi-account-tgw-delete-proposal"></a>

The owner of the transit gateway can delete the Direct Connect gateway association proposal if it is still pending acceptance\. After an association proposal is accepted, you can't delete it, but you can disassociate the transit gateway from the Direct Connect gateway\. For more information, see [Creating a Transit Gateway Association Proposal](#multi-account-tgw-create-proposal)\.

**To delete an association proposal**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Transit gateways** and then select the transit gateway\.

1. Choose **View details**\.

1. Choose **Pending gateway associations**, select the association and then choose **Delete association**\.

1. In the **Delete association proposal** dialog box, enter **Delete** and then choose **Delete**\.

**To delete a pending association proposal using the command line or API**
+ [delete\-direct\-connect\-gateway\-association\-proposal](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway-association-proposal.html) \(AWS CLI\)
+ [DeleteDirectConnectGatewayAssociationProposal](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGatewayAssociationProposal.html) \(AWS Direct Connect API\)