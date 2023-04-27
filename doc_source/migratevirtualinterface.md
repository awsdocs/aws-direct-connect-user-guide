# Migrate a virtual interface<a name="migratevirtualinterface"></a>

Use this procedure when you want to perform any of the following virtual interface migration operations:
+  Migrate an existing virtual interface associated with a connection to another LAG\.
+  Migrate an existing virtual interface associated with an existing LAG to a new LAG\.
+ Migrate an existing virtual interface associated with a connection to another connection\.

**Note**  
You can migrate a virtual interface to a new connection within the same Region, but you can't migrate it from one Region to another\. When you migrate or associate an existing virtual interface to a new connection, the configuration parameters associated with those virtual interfaces are the same\. To work around this, you can pre\-stage the configuration on the connection, and then update the BGP configuration\. 
You can't migrate a VIF from one hosted connection to another hosted connection\. VLAN IDs are unique; therefore, migrating a VIF in this way would mean the VLANs don't match\. You either need to delete the connection or VIF, and then recreate that using a VLAN that's the same for both the connection and the VIF\.

**Important**  
The virtual interface will go down for a brief period\. We recommend you perform this procedure during a maintenance window\.

**To migrate a virtual interface**

1. Sign in to the AWS Management Console and open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/](https://console.aws.amazon.com/directconnect/v2/)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface, and then choose **Edit**\.

1. For **Connection**, select the LAG or connection\.

1. Choose **Edit virtual interface**\.

**To migrate a virtual interface using the command line or API**
+ [associate\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/associate-virtual-interface.html) \(AWS CLI\)
+ [AssociateVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AssociateVirtualInterface.html) \(AWS Direct Connect API\)