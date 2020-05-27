# Setting network MTU for private virtual interfaces or transit virtual interfaces<a name="set-jumbo-frames-vif"></a>

AWS Direct Connect supports an Ethernet frame size of 1522 or 9023 bytes \(14 bytes Ethernet header \+ 4 bytes VLAN tag \+ bytes for the IP datagram \+ 4 bytes FCS\) at the link layer\.

The maximum transmission unit \(MTU\) of a network connection is the size, in bytes, of the largest permissible packet that can be passed over the connection\. The MTU of a virtual private interface can be either 1500 or 9001 \(jumbo frames\)\. The MTU of a transit virtual interface can be either 1500 or 8500 \(jumbo frames\)\. You can specify the MTU when you create the interface or update it after you create it\. Setting the MTU of a virtual interface to 8500 \(jumbo frames\) or 9001 \(jumbo frames\) can cause an update to the underlying physical connection if it wasn't updated to support jumbo frames\. Updating the connection disrupts network connectivity for all virtual interfaces associated with the connection for up to 30 seconds\. To check whether a connection or virtual interface supports jumbo frames, select it in the AWS Direct Connect console and find **Jumbo Frame Capable** on the **Summary** tab\.

After you enable jumbo frames for your private virtual interface, you can only associate it with a connection or LAG that is jumbo frame capable\. Jumbo frames are supported on virtual private interfaces attached to a virtual private gateway or a Direct Connect gateway\. Jumbo frames apply only to propagated routes from AWS Direct Connect\. If you add static routes to your virtual private gateway , traffic that is routed through the static route defaults to 1500 MTU\. If you have two private virtual interfaces that advertise the same route but use different MTU values, 1500 MTU is used\.

**Important**  
Jumbo frames apply only to propagated routes from AWS Direct Connect \. If you add static routes to a route table that point to your virtual private gateway, then traffic routed through the static routes is sent using 1500 MTU\.  
If an EC2 instance doesn't support jumbo frames, it drops jumbo frames from AWS Direct Connect\. All EC2 instance types support jumbo frames except for C1, CC1, T1, and M1\. For more information, see [Network Maximum Transmission Unit \(MTU\) for Your EC2 Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/network_mtu.html) in the *Amazon EC2 User Guide for Linux Instances*\.

**To set the MTU of a private virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1.  Select the virtual interface and then choose **Edit**\.

1. Under **Jumbo MTU \(MTU size 9001\)** or **Jumbo MTU \(MTU size 8500\)**, select **Enabled**\.

1. Under **Acknowledge**, select **I understand the selected connection\(s\) will go down for a brief period**\. The state of the virtual interface is `pending` until the update is complete\.

**To set the MTU of a private virtual interface using the command line or API**
+ [update\-virtual\-interface\-attributes](https://docs.aws.amazon.com/cli/latest/reference/directconnect/update-virtual-interface-attributes.html) \(AWS CLI\)
+ [UpdateVirtualInterfaceAttributes](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_UpdateVirtualInterfaceAttributes.html) \(AWS Direct Connect API\)