---
title: Set-CsMonitoringServer
TOCTitle: Set-CsMonitoringServer
ms:assetid: 2c6d6660-7e41-4c56-9e04-27c3d1ea3b95
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425776(v=OCS.15)
ms:contentKeyID: 48271546
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMonitoringServer

 

_**トピックの最終更新日:** 2015-03-09_

Enables you to configure new locations for the 監視サーバー database and reporting pack. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsMonitoringServer [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MonitoringDatabase <String>] [-ReportingUrl <String>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

The command shown in Example 1 configures a new URL for the 監視サーバー reporting pack.

    Set-CsMonitoringServer -Identity "MonitoringServer:atl-cs-001.litwareinc.com" -ReportingUrl "https://atl-cs-001.litwareinc.com/reports"

## Detailed Description

監視サーバー provides you with two important capabilities. For one, it enables you to maintain information about how, and how often, Enterprise Voice is used in your organization. This information is tracked by using call detail recording (CDR), which records such things as who made a call, who that person called, and how long the call lasted. (The actual conversation itself is not recorded.) In addition to that, you can also use 監視サーバー to keep track of Quality of Experience (QoE) data for your Enterprise Voice calls. As the name implies, Quality of Experience data provides information about the quality of a call, measuring such items as packet loss, call degradation, network bitrate, and jitter.

When you install 監視サーバー you must specify the location of the SQL Server database used to store CDR and QoE data. Optionally, you can also install SQL Server Reporting Services and the 監視サーバー Report Pack; these two items enable you to access a website that generates standard monitoring reports for you.

As a general rule, after 監視サーバー has been installed and configured you will not need to change the location of either the back-end database or the reporting URL. However, if you do need to change the location of one (or both) of these items, you can do so by running the **Set-CsMonitoringServer** cmdlet.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Set-CsMonitoringServer** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMonitoringServer"}

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
<td><p>Service location of the 監視サーバー to be modified. For example: -Identity &quot;MonitoringServer:atl-cs-001.litwareinc.com&quot;. You can retrieve the Identity for all of your 監視サーバー by using this command:</p>
<p>Get-CsService –MonitoringServer | Select-Object Identity.</p>
<p>Note that you can leave off the prefix &quot;MonitoringServer:&quot; when specifying a 監視サーバー. For example: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Service location for the new 監視サーバー database. For example: -MonitoringDatabase &quot;MonitoringDatabase:atl-sql-001.litwareinc.com&quot;. Make sure you use the service location of the database store and not the SQL Server path name.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportingUrl</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>URL for the 監視サーバー reports. Note that these reports will not be available unless you install SQL Server Reporting Services and the 監視サーバー Report Pack.</p></td>
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

None. The **Set-CsMonitoringServer** cmdlet does not accept pipelined input.

## Return Types

The **Set-CsMonitoringServer** cmdlet does not return any objects or values. Instead, the cmdlet modifies existing instances of the Microsoft.Rtc.Management.Xds.DisplayMonitoringServer object.

## 関連項目

#### その他のリソース

[Get-CsService](get-csservice.md)

