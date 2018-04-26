---
title: Set-CsKerberosAccountAssignment
TOCTitle: Set-CsKerberosAccountAssignment
ms:assetid: 16a964d2-2515-4a37-9686-3e377de58b14
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398232(v=OCS.15)
ms:contentKeyID: 48271385
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsKerberosAccountAssignment

 

_**トピックの最終更新日:** 2015-03-09_

Associates a Kerberos account, which is used for IIS Internet Information Services (IIS) authentication, with a site. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsKerberosAccountAssignment [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsKerberosAccountAssignment [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-UserAccount <String>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

The commands shown in Example 1 associate an existing Kerberos account (litwareinc\\keberostest) with the Redmond site, then use the **Enable-CsTopology** cmdlet to enable the new association. To do this, the first command in the example uses the **Set-CsKerberosAccountAssignment** cmdlet to associate the account litwareinc\\keberostest with the Redmond site; the second command then calls the **Enable-CsTopology** cmdlet in order to create the required service principal name in Active Directory and to enable the modified account assignment.

    Set-CsKerberosAccountAssignment -UserAccount "litwareinc\keberostest" -Identity "site:Redmond"
    Enable-CsTopology

## Detailed Description

In Microsoft Office Communications Server 2007 and Microsoft Office Communications Server 2007 R2, IIS ran under a standard user account. This had the potential to cause issues: if that password expired you could lose your Web サービス, an issue that was often difficult to diagnose. To help avoid the issue of expiring passwords, Lync Server enables you to create a computer account (for a computer that doesn’t actually exist) that can serve as the authentication principal for all the computers in a site that are running IIS. Because these accounts use the Kerberos authentication protocol, the accounts are referred to as Kerberos accounts, and the new authentication process is known as Kerberos web authentication. This enables you to manage all your IIS servers by using a single account.

To run your servers under this new authentication principal, you must first create a computer account by using the **New-CsKerberosAccount** cmdlet; this account is then assigned to one or more sites. After the assignment has been made, the association between the account and the Lync Server site is enabled by running the **Enable-CsTopology** cmdlet. Among other things, this creates the required service principal name (SPN) in Active Directory ドメイン サービス. SPNs provide a way for client applications to locate a particular service.

The **Set-CsKerberosAccountAssignment** cmdlet enables you to change the Kerberos account assigned to a given site. This cmdlet is used for sites that are already associated with an account. To assign an account to a site that currently is not associated with a Kerberos account, use the **New-CsKerberosAccountAssignment** cmdlet instead.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Set-CsKerberosAccountAssignment** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsKerberosAccountAssignment"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Unique identifier of the site where the Kerberos account was assigned. (This is the Identity of the site, not of the computer account.) For example: -Identity &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>KerberosAccountAssignment object</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserAccount</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Account name for the account to be assigned, using the format domain_name\user_name. For example: -UserAccount &quot;litwareinc\kerberostest&quot;. The user name portion of the account (kerberostest) is a NETBIOS name and can contain a maximum of 15 characters.</p>
<p>Note that, despite the name UserAccount, the account is actually a computer account, not a user account.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment object. The **Set-CsKerberosAccountAssignment** cmdlet accepts pipelined instances of the Kerberos account assignment object.

## Return Types

The **Set-CsKerberosAccountAssignment** cmdlet does not return any objects or values. Instead, the cmdlet modifies existing instances of the Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment object.

## 関連項目

#### その他のリソース

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccount](new-cskerberosaccount.md)  
[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)

