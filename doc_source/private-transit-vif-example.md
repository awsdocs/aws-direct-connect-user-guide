# Private virtual interface routing example<a name="private-transit-vif-example"></a>

Consider the configuration where the AWS Direct Connect location 1 home Region \(east\) is the same as the VPC home Region\. There is a redundant AWS Direct Connect location 2 is a different Region \(west\)\. There are two private VIFs from AWS Direct Connect location 1 to the Direct Connect gateway\. There is one private VIF from AWS Direct Connect location 2 to the Direct Connect gateway\. To have AWS route traffic over VIF B before VIF A, set the AS\_PATH attribute of VIF B to be shorter than the VIF A AS\_PATH attribute\.

The VIFs have the following configurations:
+ VIF A \(in us\-east\-1\) advertises 172\.16\.0\.0/16 and has an AS\_PATH attribute of 65001, 65001, 65001
+ VIF B \(in us\-east\-1\) advertises 172\.16\.0\.0/16 and has an AS\_PATH attribute of 65001, 65001
+ VIF C \(in us\-west\-1\) advertises 172\.16\.0\.0/16 and has an AS\_PATH attribute of 65001

![\[Private VIF Routing no AS_PATH\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/private-vif-as-path-1.png)

If you change the CIDR range configuration of VIF C, routes that fall in to the VIF C CIDR range use VIF C because it has the longest prefix match\. 
+ VIF C \(in us\-west\-1\) advertises 172\.16\.0\.0/24 and has an AS\_PATH attribute of 65001

![\[Private VIF Routing\]](http://docs.aws.amazon.com/directconnect/latest/UserGuide/images/private-vif-as-path-2.png)