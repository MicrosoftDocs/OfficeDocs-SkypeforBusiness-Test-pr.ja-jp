---
title: Test-CsKerberosAccountAssignment
TOCTitle: Test-CsKerberosAccountAssignment
ms:assetid: 442bbb32-7ad1-40c4-bf17-42ecde0a7286
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425938(v=OCS.15)
ms:contentKeyID: 48271926
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsKerberosAccountAssignment

 

_**トピックの最終更新日:** 2015-03-09_

Verifies the configuration of the Kerberos account assigned to a site. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsKerberosAccountAssignment -Identity <XdsIdentity> [-Report <String>]

## Examples

## EXAMPLE 1

The command shown in Example 1 verifies that the Kerberos account assigned to the Redmond site is configured correctly and is working as expected.

    Test-CsKerberosAccountAssignment -Identity site:Redmond

## Detailed Description

In Microsoft Office Communications Server 2007 and Microsoft Office Communications Server 2007 R2, IIS ran under a standard user account. This had the potential to cause issues: if that password expired you could lose your Web サービス, an issue that was often difficult to diagnose. To help avoid the issue of expiring passwords, Lync Server enables you to create a computer account (for a computer that doesn’t actually exist) that can serve as the authentication principal for all the computers in a site that are running IIS. Because these accounts use the Kerberos authentication protocol, the accounts are referred to as Kerberos accounts, and the new authentication process is known as Kerberos web authentication. This enables you to manage all your IIS servers by using a single account.

The **Test-CsKerberosAccountAssignment** cmdlet provides a way for you to verify that a Kerberos account has been associated with a given site, that this account has been configured correctly, and that the account is working as expected.

Who can run this cmdlet: To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsKerberosAccountAssignment"}

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
<td><p><em>Identity</em></p></td>
<td><p>Required</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Name of the site where the Kerberos account was assigned. For example: -Identity &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Enables you to specify a file path for the log file created when the cmdlet runs. For example: -Report &quot;C:\Logs\TestKerberos.html&quot;.</p></td>
</tr>
</tbody>
</table>


## Input Types

None. The **Test-CsKerberosAccountAssignment** cmdlet does not accept pipelined input.

## Return Types

The **Test-CsKerberosAccountAssignment** cmdlet does not return any objects or values.

## 関連項目

#### その他のリソース

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)  
[Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

