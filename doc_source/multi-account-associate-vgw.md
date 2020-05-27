# Associating a virtual private gateway across accounts<a name="multi-account-associate-vgw"></a>

You can associate a Direct Connect gateway with a virtual private gateway that's in a different AWS account\. The Direct Connect gateway can be an existing gateway, or you can create a new gateway\. The owner of the virtual private gateway creates an *association proposal* and the owner of the Direct Connect gateway must accept the association proposal\.

An association proposal can contain prefixes that will be allowed from the virtual private gateway\. The owner of the Direct Connect gateway can optionally override any requested prefixes in the association proposal\.

## Allowed prefixes<a name="allowed-prefixes"></a>

When you associate a virtual private gateway with a Direct Connect gateway, you specify a list of Amazon VPC prefixes to advertise to the Direct Connect gateway\. The prefix list acts as a filter that allows the same CIDRs, or smaller CIDRs to be advertised to the Direct Connect gateway\. You must set the **Allowed prefixes** to a range that is the same or wider than the VPC CIDR because we provision entire VPC CIDR on the virtual private gateway\. 

Consider the case where the VPC CIDR is 10\.0\.0\.0/16\. You can set the **Allowed prefixes** to 10\.0\.0\.0/16 \(the VPC CIDR value\), or 10\.0\.0\.0/15 \( a value that is wider than the VPC CIDR\)\. 

For more information on how allowed prefixes interact with virtual private gateways and transit gateways, see [Allowed prefixes interactions](allowed-to-prefixes.md)\.

**Topics**
+ [Allowed prefixes](#allowed-prefixes)
+ [Creating an association proposal](#multi-account-create-proposal)
+ [Accepting or rejecting an association proposal](#multi-account-accept-reject-proposal)
+ [Updating the allowed prefixes for an association](#multi-account-update-proposal-routes)
+ [Deleting an association proposal](#multi-account-delete-proposal)

## Creating an association proposal<a name="multi-account-create-proposal"></a>

If you own the virtual private gateway, you must create an association proposal\. The virtual private gateway must be attached to a VPC in your AWS account\. The owner of the Direct Connect gateway must share the ID of the Direct Connect gateway and the ID of its AWS account\. After you create the proposal, the owner of the Direct Connect gateway must accept it in order for you to gain access to the on\-premises network over AWS Direct Connect\.

**To create an association proposal**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual private gateways** and select the virtual private gateway\.

1. Choose **View details**\.

1. Choose **Direct Connect gateway associations** and choose **Associate Direct Connect gateway**\.

1. Under **Association account type**, for **Account owner**, choose **Another account**\.

1. For **Direct Connect gateway owner**, enter the id of the AWS account that owns the Direct Connect gateway\.

1. Under **Association settings**, do the following:

   1. For **Direct Connect gateway ID**, enter the ID of the Direct Connect gateway\.

   1. For **Direct Connect gateway owner**, enter the ID of the AWS account that owns the Direct Connect gateway for the association\.

   1. \(Optional\) To specify a list of prefixes to be allowed from the virtual private gateway, add the prefixes to **Allowed prefixes**, separating them using commas, or entering them on separate lines\.

1. Choose **Associate Direct Connect gateway**\.

**To create an association proposal using the command line or API**
+ [create\-direct\-connect\-gateway\-association\-proposal](https://docs.aws.amazon.com/cli/latest/reference/directconnect/create-direct-connect-gateway-association-proposal.html) \(AWS CLI\)
+ [CreateDirectConnectGatewayAssociationProposal](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateDirectConnectGatewayAssociationProposal.html) \(AWS Direct Connect API\)

## Accepting or rejecting an association proposal<a name="multi-account-accept-reject-proposal"></a>

If you own the Direct Connect gateway, you must accept the association proposal in order to create the association\. Otherwise, you can reject the association proposal\.

**To accept an association proposal**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect gateways**\.

1. Select the Direct Connect gateway with pending proposals and choose **View details**\.

1. On the **Pending proposals** tab, select the proposal and choose **Accept proposal**\.

1. \(\(Optional\) To specify a list of prefixes to be allowed from the virtual private gateway, add the prefixes to **Allowed prefixes**, separating them using commas, or entering them on separate lines\.

1. Choose** Accept proposal**\.

**To reject an association proposal**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Direct Connect gateways**\.

1. Select the Direct Connect gateway with pending proposals and choose **View details**\.

1. On the **Pending proposals** tab, select the virtual private gateway and choose **Reject proposal**\.

1. In the **Reject proposal** dialog box, enter Delete and choose **Reject proposal**\.

**To view association proposals using the command line or API**
+ [describe\-direct\-connect\-gateway\-association\-proposals](https://docs.aws.amazon.com/cli/latest/reference/directconnect/describe-direct-connect-gateway-association-proposals.htm) \(AWS CLI\)
+ [DescribeDirectConnectGatewayAssociationProposals](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeDirectConnectGatewayAssociationProposals.html) \(AWS Direct Connect API\)

**To accept an association proposal using the command line or API**
+ [accept\-direct\-connect\-gateway\-association\-proposal](https://docs.aws.amazon.com/cli/latest/reference/directconnect/accept-direct-connect-gateway-association-proposal.html) \(AWS CLI\)
+ [AcceptDirectConnectGatewayAssociationProposal](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AcceptDirectConnectGatewayAssociationProposal.html) \(AWS Direct Connect API\)

**To reject an association proposal using the command line or API**
+ [delete\-direct\-connect\-gateway\-association\-proposal](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway-association-proposal.html) \(AWS CLI\)
+ [DeleteDirectConnectGatewayAssociationProposal](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGatewayAssociationProposal.html) \(AWS Direct Connect API\)

## Updating the allowed prefixes for an association<a name="multi-account-update-proposal-routes"></a>

You can update the prefixes that are allowed from the virtual private gateway over the Direct Connect gateway\.

If you're the owner of the virtual private gateway, [create a new association proposal](#multi-account-create-proposal) for the same Direct Connect gateway and virtual private gateway, specifying the prefixes to allow\.

If you're the owner of the Direct Connect gateway, update the allowed prefixes when you [accept the association proposal](#multi-account-accept-reject-proposal) or update the allowed prefixes for an existing association as follows\.

**To update the allowed prefixes for an existing association using the command line or API**
+ [update\-direct\-connect\-gateway\-association](https://docs.aws.amazon.com/cli/latest/reference/directconnect/update-direct-connect-gateway-association.html) \(AWS CLI\)
+ [UpdateDirectConnectGatewayAssociation](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_UpdateDirectConnectGatewayAssociation.html) \(AWS Direct Connect API\)

## Deleting an association proposal<a name="multi-account-delete-proposal"></a>

The owner of the virtual private gateway can delete the Direct Connect gateway association proposal if it is still pending acceptance\. After an association proposal is accepted, you can't delete it, but you can disassociate the virtual private gateway from the Direct Connect gateway\. For more information, see [Associating and disassociating virtual private gateways](virtualgateways.md#associate-vgw-with-direct-connect-gateway)\.

**To delete an association proposal**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual private gateways** and select the virtual private gateway\.

1. Choose **View details**\.

1. Choose **Pending Direct Connect gateway associations**, select the association and choose **Delete association**\.

1. In the **Delete association proposal** dialog box, enter Delete and choose **Delete**\.

**To delete a pending association proposal using the command line or API**
+ [delete\-direct\-connect\-gateway\-association\-proposal](https://docs.aws.amazon.com/cli/latest/reference/directconnect/delete-direct-connect-gateway-association-proposal.html) \(AWS CLI\)
+ [DeleteDirectConnectGatewayAssociationProposal](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DeleteDirectConnectGatewayAssociationProposal.html) \(AWS Direct Connect API\)