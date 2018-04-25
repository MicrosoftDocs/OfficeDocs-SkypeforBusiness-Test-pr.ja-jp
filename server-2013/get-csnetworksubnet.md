---
title: Get-CsNetworkSubnet
TOCTitle: Get-CsNetworkSubnet
ms:assetid: ad74155a-8d83-42f6-bb1e-8bfc7d57d5b0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412825(v=OCS.15)
ms:contentKeyID: 48273256
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkSubnet

 

_**トピックの最終更新日:** 2015-03-09_

Retrieves information about one or more network subnets. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsNetworkSubnet [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkSubnet [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Examples

## EXAMPLE 1

This example retrieves all subnets within the Lync Server deployment.

    Get-CsNetworkSubnet

## EXAMPLE 2

This example retrieves all information about the subnet with the Identity (the Subnet ID) 172.11.15.0.

    Get-CsNetworkSubnet -Identity 172.11.15.0

## EXAMPLE 3

This example retrieves all subnets with identities that begin with 172.11..

    Get-CsNetworkSubnet -Filter 172.11.*

## EXAMPLE 4

Example 4 retrieves all subnets associated with the Vancouver site. We first call the **Get-CsNetworkSubnet** cmdlet with no parameters, which, as we saw in Example 2, retrieves all defined subnets. We then pipe this collection of subnets to the **Where-Object** cmdlet. The **Where-Object** cmdlet takes that collection and narrows it down to only those subnets with a NetworkSiteID equal to (-eq) Vancouver.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"}

## Detailed Description

Each subnet must be associated with a network site for the purposes of determining the geographic location of the host belonging to this subnet. Use this cmdlet to retrieve information about the subnet, including the Identity (the subnet ID), the number of mask bits, the associated network site, and the description of the subnet.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Get-CsNetworkSubnet** cmdlet locally: RTCUniversalUserAdmins, RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkSubnet"}

## パラメーター


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Required</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Use this parameter to perform a wildcard search of all subnets based on Identity. For example, the Filter value 172.11.* will retrieve all subnets with an Identity beginning with 172.11. (such as 172.11.10.0, 172.11.25.0, etc.).</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>The unique subnet ID of the subnet you want to retrieve. This value will be an IP address (such as 174.11.12.0).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Retrieves the network subnet information from the local replica of the 中央管理ストア, rather than the 中央管理ストア itself.</p></td>
</tr>
</tbody>
</table>


## Input Types

None.

## Return Types

Returns one or more objects of type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType.

## 関連項目

#### その他のリソース

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)

