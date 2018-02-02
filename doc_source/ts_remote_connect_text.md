# Troubleshooting a Remote Connection to AWS Direct Connect<a name="ts_remote_connect_text"></a>

You can use the following tasks to diagnose, troubleshoot, and repair a faulty connection to AWS Direct Connect when connecting remotely through a service provider\. To see these tasks in a flow chart, see [Flow Chart: Troubleshooting a Remote Connection to AWS Direct Connect](ts_remote_connect.md)\.

1. Verify that your device is supported by AWS Direct Connect\. If not, get a device that meets the AWS Direct Connect requirements\. For more information, see [What is AWS Direct Connect?](Welcome.md)\.

1. Verify that your AWS Direct Connect cross connects are established\. If they are not, work with your service provider to establish them\.

1. Verify that your router’s link lights are working\. If they are not, turn on your device and activate the ports\.

1. Verify with your service provider that there are no cabling problems\.

1. Ask your service provider to turn off Auto Negotiation on their device, to set their device to Full Duplex, and to set their device to the correct speed\.

1. On your device, turn off Auto Negotiation, set the device to Full Duplex, and set the device to the correct speed\.

1. If you cannot ping the Amazon IP address, verify that the interface IP address is in the VLAN that you provided to AWS, and then verify your firewall settings\. If you still cannot connect to AWS Direct Connect, open a support ticket with AWS support for assistance and include the original ticket number from your letter of authorization \(LOA\)\.

1. If you cannot establish Border Gateway Protocol \(BGP\) after verifying the password provided by Amazon, open a support ticket with AWS support for assistance and include the original ticket number from your LOA\.

1. If you are not receiving Amazon routes and you've verified the BGP routing policy for a public connection, or verified the route tables, security groups, or access control lists \(ACLs\) for a private connection, open a support ticket with AWS support and include your connection ID from your LOA\.