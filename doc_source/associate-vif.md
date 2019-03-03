# Associating a Virtual Interface with a Connection or LAG<a name="associate-vif"></a>

You can associate a virtual interface with a link aggregation group \(LAG\), or another connection\.

You cannot associate a virtual interface if the target connection or LAG has an existing associated virtual interface with the following matching attributes:
+ A conflicting VLAN number
+ \(Public virtual interfaces\) The same IP address range for the Amazon router, or for the customer router
+ \(Private virtual interfaces\) The same virtual private gateway and the same IP address range for the Amazon router, or for the customer router

You cannot disassociate a virtual interface from a connection or LAG, but you can re\-associate it or delete it\. For more information, see [Deleting a Virtual Interface](deletevif.md)\.

**Important**  
Connectivity to AWS is temporarily interrupted during the association process\.

**To associate a virtual interface with a connection**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface and choose **Actions**, **Associate Connection or LAG**\.

1. Choose the required connection, select the confirmation check box, and choose **Continue**\.

You can use the same procedure above to associate a virtual interface with a LAG\. Alternatively, you can use the **LAGs** screen\.

**To associate a virtual interface with a LAG**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/](https://console.aws.amazon.com/directconnect/)\.

1. In the navigation pane, choose **LAGs**\.

1. Select the LAG and choose **Actions**, **Associate Virtual Interface**\.

1. Choose the required virtual interface, select the confirmation check box, and choose **Continue**\.

**To associate a virtual interface using the command line or API**
+ [https://docs.aws.amazon.com/cli/latest/reference/directconnect/associate-virtual-interface.html](https://docs.aws.amazon.com/cli/latest/reference/directconnect/associate-virtual-interface.html) \(AWS CLI\)
+ [https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AssociateVirtualInterface.html](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AssociateVirtualInterface.html) \(AWS Direct Connect API\)