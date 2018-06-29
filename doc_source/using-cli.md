# Using the AWS CLI<a name="using-cli"></a>

You can use the AWS CLI to create and work with AWS Direct Connect resources\.

The following example uses the AWS CLI commands to create an AWS Direct Connect connection, download the Letter of Authorization and Connecting Facility Assignment \(LOA\-CFA\), and provision a private or public virtual interface\.

Before you begin, ensure that you have installed and configured the AWS CLI\. For more information, see the [AWS Command Line Interface User Guide](http://docs.aws.amazon.com/cli/latest/userguide/)\.

**Topics**
+ [Step 1: Create a Connection](#using-cli-create-connection)
+ [Step 2: Download the LOA\-CFA](#using-cli-loa-cfa)
+ [Step 3: Create a Virtual Interface and get the Router Configuration](#using-cli-create-vif)

## Step 1: Create a Connection<a name="using-cli-create-connection"></a>

The first step is to submit a connection request\. Ensure that you know the port speed that you require and the AWS Direct Connect location\. For more information, see [Connections](WorkingWithConnections.md)\.

**To create a connection request**

1. Describe the AWS Direct Connect locations for your current region\. In the output that's returned, take note of the location code for the location in which you want to establish the connection\.

   ```
   aws directconnect describe-locations
   ```

   ```
   {
       "locations": [
           {
               "locationName": "NAP do Brasil, Barueri, Sao Paulo",
               "locationCode": "TNDB"
           },
           {
               "locationName": "Tivit - Site Transamerica (Sao Paulo)",
               "locationCode": "TIVIT"
           }
       ]
   }
   ```

1. Create the connection and specify a name, the port speed, and the location code\. In the output that's returned, take note of the connection ID\. You need the ID to get the LOA\-CFA in the next step\.

   ```
   aws directconnect create-connection --location TIVIT --bandwidth 1Gbps --connection-name "Connection to AWS"
   ```

   ```
   {
       "ownerAccount": "123456789012",
       "connectionId": "dxcon-fg31dyv6",
       "connectionState": "requested",
       "bandwidth": "1Gbps",
       "location": "TIVIT",
       "connectionName": "Connection to AWS",
       "region": "sa-east-1"
   }
   ```

## Step 2: Download the LOA\-CFA<a name="using-cli-loa-cfa"></a>

After you've requested a connection, you can get the LOA\-CFA using the `describe-loa` command\. The output is base64\-encoded\. You must extract the relevant LOA content, decode it, and create a PDF file\.

**To get the LOA\-CFA using Linux or Mac OS X**

In this example, the final part of the command decodes the content using the base64 utility, and sends the output to a PDF file\.

```
aws directconnect describe-loa --connection-id dxcon-fg31dyv6 --output text --query loaContent|base64 --decode > myLoaCfa.pdf
```

**To get the LOA\-CFA using Windows**

In this example, the output is extracted to a file called myLoaCfa\.base64\. The second command uses the `certutil` utility to decode the file and send the output to a PDF file\.

```
aws directconneawsct describe-loa --connection-id dxcon-fg31dyv6 --output text --query loaContent > myLoaCfa.base64
```

```
certutil -decode myLoaCfa.base64 myLoaCfa.pdf
```

After you've downloaded the LOA\-CFA, send it to your network provider or colocation provider\. 

## Step 3: Create a Virtual Interface and get the Router Configuration<a name="using-cli-create-vif"></a>

After you have placed an order for an AWS Direct Connect connection, you must create a virtual interface to begin using it\. You can create a private virtual interface to connect to your VPC, or you can create a public virtual interface to connect to AWS services that aren't in a VPC\. You can create a virtual interface that supports IPv4 or IPv6 traffic\.

Before you begin, ensure that you've read the prerequisites in [Prerequisites for Virtual Interfaces](WorkingWithVirtualInterfaces.md#vif-prerequisites)\. 

When you create a virtual interface using the AWS CLI, the output includes generic router configuration information\. If you want router configuration that's specific to your device, use the AWS Direct Connect console\. For more information, see [Downloading the Router Configuration File](create-vif.md#vif-router-config)\.

**To create a private virtual interface**

1. Get the ID of the virtual private gateway \(vgw\-*xxxxxxxx*\) that's attached to your VPC\. You need the ID to create the virtual interface in the next step\.

   ```
   aws ec2 describe-vpn-gateways
   ```

   ```
   {
       "VpnGateways": [
           {
               "State": "available", 
               "Tags": [
                   {
                       "Value": "DX_VGW", 
                       "Key": "Name"
                   }
               ], 
               "Type": "ipsec.1", 
               "VpnGatewayId": "vgw-ebaa27db", 
               "VpcAttachments": [
                   {
                       "State": "attached", 
                       "VpcId": "vpc-24f33d4d"
                   }
               ]
           }
       ]
   }
   ```

1. Create a private virtual interface\. You must specify a name, a VLAN ID, and a BGP Autonomous System Number \(ASN\)\. 

   For IPv4 traffic, you need private IPv4 addresses for each end of the BGP peering session\. You can specify your own IPv4 addresses, or you can let Amazon generate the addresses for you\. In the following example, the IPv4 addresses are generated for you\.

   ```
   aws directconnect create-private-virtual-interface --connection-id dxcon-fg31dyv6 --new-private-virtual-interface virtualInterfaceName=PrivateVirtualInterface,vlan=101,asn=65000,virtualGatewayId=vgw-ebaa27db,addressFamily=ipv4
   ```

   ```
   {
       "virtualInterfaceState": "pending",
       "asn": 65000,
       "vlan": 101,
       "customerAddress": "192.168.1.2/30",
       "ownerAccount": "123456789012",
       "connectionId": "dxcon-fg31dyv6",
       "addressFamily": "ipv4", 
       "virtualGatewayId": "vgw-ebaa27db",
       "virtualInterfaceId": "dxvif-ffhhk74f",
       "authKey": "asdf34example",
       "routeFilterPrefixes": [],
       "location": "TIVIT",
       "bgpPeers": [
           {
               "bgpStatus": "down", 
               "customerAddress": "192.168.1.2/30", 
               "addressFamily": "ipv4", 
               "authKey": "asdf34example", 
               "bgpPeerState": "pending", 
               "amazonAddress": "192.168.1.1/30", 
               "asn": 65000
           }
       "customerRouterConfig": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<logical_connection id=\"dxvif-ffhhk74f\">\n  <vlan>101</vlan>\n  <customer_address>192.168.1.2/30</customer_address>\n  <amazon_address>192.168.1.1/30</amazon_address>\n  <bgp_asn>65000</bgp_asn>\n  <bgp_auth_key>asdf34example</bgp_auth_key>\n  <amazon_bgp_asn>7224</amazon_bgp_asn>\n  <connection_type>private</connection_type>\n</logical_connection>\n",
       "amazonAddress": "192.168.1.1/30",
       "virtualInterfaceType": "private",
       "virtualInterfaceName": "PrivateVirtualInterface"
   }
   ```

   To create a private virtual interface that supports IPv6 traffic, use the same command as above and specify `ipv6` for the `addressFamily` parameter\. You cannot specify your own IPv6 addresses for the BGP peering session; Amazon allocates you IPv6 addresses\.

1. To view the router configuration information in XML format, describe the virtual interface you created\. Use the `--query` parameter to extract the `customerRouterConfig` information, and the `--output` parameter to organize the text into tab\-delimited lines\.

   ```
   aws directconnect describe-virtual-interfaces --virtual-interface-id dxvif-ffhhk74f --query virtualInterfaces[*].customerRouterConfig --output text
   ```

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <logical_connection id="dxvif-ffhhk74f">
     <vlan>101</vlan>
     <customer_address>192.168.1.2/30</customer_address>
     <amazon_address>192.168.1.1/30</amazon_address>
     <bgp_asn>65000</bgp_asn>
     <bgp_auth_key>asdf34example</bgp_auth_key>
     <amazon_bgp_asn>7224</amazon_bgp_asn>
     <connection_type>private</connection_type>
   </logical_connection>
   ```

**To create a public virtual interface**

1. To create a public virtual interface, you must specify a name, a VLAN ID, and a BGP Autonomous System Number \(ASN\)\. 

   For IPv4 traffic, you must also specify public IPv4 addresses for each end of the BGP peering session, and public IPv4 routes that you will advertise over BGP\. The following example creates a public virtual interface for IPv4 traffic\.

   ```
   aws directconnect create-public-virtual-interface --connection-id dxcon-fg31dyv6 --new-public-virtual-interface virtualInterfaceName=PublicVirtualInterface,vlan=2000,asn=65000,amazonAddress=203.0.113.1/30,customerAddress=203.0.113.2/30,addressFamily=ipv4,routeFilterPrefixes=[{cidr=203.0.113.0/30},{cidr=203.0.113.4/30}]
   ```

   ```
   {
       "virtualInterfaceState": "verifying",
       "asn": 65000,
       "vlan": 2000,
       "customerAddress": "203.0.113.2/30",
       "ownerAccount": "123456789012",
       "connectionId": "dxcon-fg31dyv6",
       "addressFamily": "ipv4",
       "virtualGatewayId": "",
       "virtualInterfaceId": "dxvif-fgh0hcrk",
       "authKey": "asdf34example",
       "routeFilterPrefixes": [
           {
               "cidr": "203.0.113.0/30"
           },
           {
               "cidr": "203.0.113.4/30"
           }
       ],
       "location": "TIVIT",
       "bgpPeers": [
           {
               "bgpStatus": "down", 
               "customerAddress": "203.0.113.2/30", 
               "addressFamily": "ipv4", 
               "authKey": "asdf34example", 
               "bgpPeerState": "verifying", 
               "amazonAddress": "203.0.113.1/30", 
               "asn": 65000
           }
       ],
       "customerRouterConfig": "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n<logical_connection id=\"dxvif-fgh0hcrk\">\n  <vlan>2000</vlan>\n  <customer_address>203.0.113.2/30</customer_address>\n  <amazon_address>203.0.113.1/30</amazon_address>\n  <bgp_asn>65000</bgp_asn>\n  <bgp_auth_key>asdf34example</bgp_auth_key>\n  <amazon_bgp_asn>7224</amazon_bgp_asn>\n  <connection_type>public</connection_type>\n</logical_connection>\n",
       "amazonAddress": "203.0.113.1/30",
       "virtualInterfaceType": "public",
       "virtualInterfaceName": "PublicVirtualInterface"
   }
   ```

   To create a public virtual interface that supports IPv6 traffic, you can specify IPv6 routes that you will advertise over BGP\. You cannot specify IPv6 addresses for the peering session; Amazon allocates IPv6 addresses to you\. The following example creates a public virtual interface for IPv6 traffic\.

   ```
   aws directconnect create-public-virtual-interface --connection-id dxcon-fg31dyv6 --new-public-virtual-interface virtualInterfaceName=PublicVirtualInterface,vlan=2000,asn=65000,addressFamily=ipv6,routeFilterPrefixes=[{cidr=2001:db8:64ce:ba00::/64},{cidr=2001:db8:64ce:ba01::/64}]
   ```

1. To view the router configuration information in XML format, describe the virtual interface you created\. Use the `--query` parameter to extract the `customerRouterConfig` information, and the `--output` parameter to organize the text into tab\-delimited lines\.

   ```
   aws directconnect describe-virtual-interfaces --virtual-interface-id dxvif-fgh0hcrk --query virtualInterfaces[*].customerRouterConfig --output text
   ```

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <logical_connection id="dxvif-fgh0hcrk">
     <vlan>2000</vlan>
     <customer_address>203.0.113.2/30</customer_address>
     <amazon_address>203.0.113.1/30</amazon_address>
     <bgp_asn>65000</bgp_asn>
     <bgp_auth_key>asdf34example</bgp_auth_key>
     <amazon_bgp_asn>7224</amazon_bgp_asn>
     <connection_type>public</connection_type>
   </logical_connection>
   ```