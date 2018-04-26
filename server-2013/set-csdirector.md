---
title: Set-CsDirector
TOCTitle: Set-CsDirector
ms:assetid: 74eb6f17-812f-47df-84ee-fa6e42990f2e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398565(v=OCS.15)
ms:contentKeyID: 48272472
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDirector

 

_**トピックの最終更新日:** 2015-03-09_

Modifies the properties of one or more Directors. Directors can be used to authenticate user requests, but do not host user accounts. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsDirector [-Identity <XdsGlobalRelativeIdentity>] [-ArchivingServer <String>] [-Confirm [<SwitchParameter>]] [-EdgeServer <String>] [-Force <SwitchParameter>] [-MirrorMonitoringDatabase <String>] [-MonitoringDatabase <String>] [-MonitoringServer <String>] [-SipHealthPort <UInt16>] [-SipPort <UInt16>] [-SipServerTcpPort <UInt16>] [-WebPort <UInt16>] [-WebServer <String>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

The command shown in Example 1 changes the アーカイブ サーバー associated with the ディレクター Director:atl-cs-001.litwareinc.com. In this example, the アーカイブ サーバー is switched to ArchivingServer:dublin-cs-001.litwareinc.com.

    Set-CsDirector -Identity "Director:atl-cs-001.litwareinc.com" -ArchivingServer "ArchivingServer:dublin-cs-001.litwareinc.com"

## EXAMPLE 2

Example 2 changes the SIP port for all the Directors currently in use in the organization. To do this, the command first uses the **Get-CsService** cmdlet and the Director parameter to return a collection of all the Directors in the organization. That collection is then piped to the **ForEach-Object**. In turn, the **ForEach-Object** cmdlet runs the **Set-CsDirector** cmdlet against each site in the collection, changing the value of the SipPort property to 5072.

    Get-CsService -Director | ForEach-Object {Set-CsDirector -Identity $_.Identity -SipPort 5072}

## Detailed Description

The ディレクター authenticates users and responds to user requests without actually hosting user accounts. Directors are typically used for organizations that allow external access to the network through Edge Servers. In that scenario, Directors not only help alleviate the strain on Front End Servers (by handling authentication requests), but also help shield the internal network from denial-of-service attacks and other malicious traffic. Directors are also useful any time multiple Front End Servers are deployed in a central site. In that case, Directors receive all user requests and then channel those requests to the appropriate server pool. This, again, helps to ease the burden placed on the Front End Servers.

The **Set-CsDirector** cmdlet enables you to modify the property values for any of the Directors currently in use in your organization. This includes changing such things as the アーカイブ サーバー or エッジ サーバー associated with the ディレクター, or changing the port used for sending and receiving SIP traffic.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Set-CsDirector** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDirector"}

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
<td><p><em>ArchivingServer</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Service location of the アーカイブ サーバー to be associated with the ディレクター. For example: -ArchivingServer &quot;ArchivingServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Service location of the エッジ サーバー to be associated with the ディレクター. For example: -EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;</p></td>
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
<td><p>Service location of the ディレクター to be modified. For example: -Identity &quot;Director:atl-cs-001.litwareinc.com&quot;.</p>
<p>Note that you can leave off the prefix &quot;Director:&quot; when specifying a Director. For example: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorMonitoringDatabase</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Service location of the mirror monitoring database to be associated with the ディレクター.</p></td>
</tr>
<tr class="odd">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Service location of the monitoring database to be associated with the ディレクター.</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringServer</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Service location of the 監視サーバー to be associated with the ディレクター. For example: -MonitoringServer &quot;MonitoringServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipHealthPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port used for monitoring server health.</p></td>
</tr>
<tr class="even">
<td><p><em>SipPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port used for Session Initiation Protocol (SIP) traffic.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipServerTcpPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>SIP listening port. The default value is 5060.</p></td>
</tr>
<tr class="even">
<td><p><em>WebPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port used for communicating with Web サービス.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebServer</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Web サービス location of the server to be associated with the ディレクター. For example: -WebServer &quot;WebServer:atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## Input Types

None. The **Set-CsDirector** cmdlet does not accept pipelined input.

## Return Types

The **Set-CsDirector** cmdlet does not return any objects or values. Instead, the cmdlet modifies existing instances of the Microsoft.Rtc.Management.Xds.DisplayDirector object.

## 関連項目

#### その他のリソース

[Get-CsService](get-csservice.md)

