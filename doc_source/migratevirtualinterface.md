# Migrating a virtual interface<a name="migratevirtualinterface"></a>

Use this procedure when you want to perform any of the following virtual interface migration operations:
+  Migrate an existing virtual interface associated with a connection to another LAG\.
+  Migrate an existing virtual interface associated with an existing LAG to a new LAG\.
+ Migrate an existing virtual interface associated with a connection to another connection\.

**Note**  
When you migrate or associate an existing virtual interface to a new connection, the configuration parameters that are associated with the virtual interfaces are the same\. You can pre\-stage the configuration on the connection, and then update the BGP configuration\.

**Important**  
The virtual Interface will go down for a brief period\. We recommend you perform this procedure during a maintenance window\.

**To migrate a virtual interface**

1. Open the AWS Direct Connect console at [https://console\.aws\.amazon\.com/directconnect/v2/home](https://console.aws.amazon.com/directconnect/v2/home)\.

1. In the navigation pane, choose **Virtual Interfaces**\.

1. Select the virtual interface, and then choose **Edit**\.

1. For **Connection**, select the LAG or connection\.

1. Choose **Edit virtual interface**\.

**To migrate a virtual interface using the command line or API**
+ [associate\-virtual\-interface](https://docs.aws.amazon.com/cli/latest/reference/directconnect/associate-virtual-interface.html) \(AWS CLI\)
+ [AssociateVirtualInterface](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_AssociateVirtualInterface.html) \(AWS Direct Connect API\)