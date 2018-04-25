---
title: New-CsSipProxyCustom
TOCTitle: New-CsSipProxyCustom
ms:assetid: 3dc75cb0-c3d2-48bd-af32-2b2034b655dd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425904(v=OCS.15)
ms:contentKeyID: 48271871
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipProxyCustom

 

_**トピックの最終更新日:** 2015-03-09_

Used to assign a custom realm (SIP Communications Service) to a collection of proxy configuration settings. Realms (also known as protection domains) are used to authenticate user credentials during logon. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsSipProxyCustom -CustomValue <String>

## Examples

## EXAMPLE 1

The command shown in Example 1 assigns a custom realm (Litwareinc Communications Service) to a variable named $x.

    $x = New-CsSipProxyCustom -CustomValue "Litwareinc Communications Service"

## Detailed Description

Each proxy server must be associated with a realm; realms (also known as protection domains) indicate where a user’s logon credentials should be processed. By default, Lync Server uses SIP Communications Service as its default realm; however, it is possible to change the realm used by a proxy server. This is done by creating a SipProxy.Custom object and then assigning that object to the Realm property of the appropriate proxy server (or servers). You can create a custom realm by using the **New-CsSipProxyCustom** cmdlet.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **New-CsSipProxyCustom** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipProxyCustom"}

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
<td><p><em>CustomValue</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>Name of the realm to be used for authentication purposes.</p></td>
</tr>
</tbody>
</table>


## Input Types

None. The **New-CsSipProxyCustom** cmdlet does not accept pipelined input.

## Return Types

The **New-CsSipProxyCustom** cmdlet creates new instances of the Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.Custom object.

## 関連項目

#### その他のリソース

[New-CsSipProxyRealm](new-cssipproxyrealm.md)  
[New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

