---
title: Set-CsManagementServer
TOCTitle: Set-CsManagementServer
ms:assetid: 6607580d-f111-4dff-961a-71525bf2e482
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398465(v=OCS.15)
ms:contentKeyID: 48272338
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsManagementServer

 

_**トピックの最終更新日:** 2015-03-09_

Modifies the replication port used by the Lync Server 中央管理サービス. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsManagementServer [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ReplicationServicePort <UInt16>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

The command shown in Example 1 connects to the 中央管理サービス with the Identity ManagementServer:atl-cs-001.litwareinc.com and sets the replication service port to port 5076.

    Set-CsManagementServer -Identity "ManagementServer:atl-cs-001.litwareinc.com" -ReplicationServicePort 5076

## Detailed Description

The 中央管理サービス is responsible for replicating data between the 中央管理ストア and computers running Lync Server services or server roles. The 中央管理サービス runs on a single フロント エンド プール (or a single Standard Edition サーバー) and facilitates replication throughout the Lync Server infrastructure.

The **Set-CsManagementServer** cmdlet enables you to specify the port that the 中央管理サービス uses for replication.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Set-CsManagementServer** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsManagementServer"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses the display of any non-fatal error message that might occur when running the command.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Unique identifier for the 中央管理サービス. For example: -Identity &quot;ManagementServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Note that you can leave off the prefix &quot;ManagementServer:&quot; when specifying a 中央管理サーバー. For example: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicationServicePort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port number for the replication port used by the 中央管理サービス.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## Input Types

None. The **Set-CsManagementServer** cmdlet does not accept pipelined input.

## Return Types

The **Set-CsManagementServer** cmdlet does not return any objects or values. Instead, the cmdlet modifies existing instances of the Microsoft.Rtc.Management.Xds.DisplayManagementServer object.

## 関連項目

#### その他のリソース

[Get-CsService](get-csservice.md)  
[Move-CsManagementServer](move-csmanagementserver.md)

