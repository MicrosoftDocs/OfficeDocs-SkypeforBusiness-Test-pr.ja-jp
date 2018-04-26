---
title: Update-CsAdminRole
TOCTitle: Update-CsAdminRole
ms:assetid: 42cc9cc2-c408-4d0c-814a-6c6367cba834
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ204851(v=OCS.15)
ms:contentKeyID: 48271918
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsAdminRole

 

_**トピックの最終更新日:** 2015-03-09_

Updates the role-based access control (RBAC) definitions stored in the Central Management database without affecting any other database tables. このコマンドレットは Lync Server 2013 で導入されました。

## 構文

    Update-CsAdminRole [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Examples

## Example 1

The command shown in Example 1 updates the RBAC definitions stored in the Central Management database.

    Update-CsAdminRole

## Detailed Description

The **Update-CsAdminRole** cmdlet provides a way for you to update the RBAC role definitions stored in the Central Management database. This cmdlet is typically used in coexistence/migration scenarios where the Central Management database is currently located in a Microsoft Lync Server 2010 pool.

To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell コマンドライン インターフェイス prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Update-CsAdminRole"}

**Lync Server コントロール パネル:** The functions carried out by the **Update-CsAdminRole** cmdlet are not available in the Lync Server コントロール パネル.

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
<td><p>Prompts you for confirmation before executing the command.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses the display of any non-fatal error message that might occur when running the command.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describes what would happen if you executed the command without actually executing the command.</p></td>
</tr>
</tbody>
</table>


## Input Types

None. The **Update-CsAdminRole** cmdlet does not accept pipelined input.

## Return Types

None. The **Update-CsAdminRole** cmdlet does not return any data or objects.

