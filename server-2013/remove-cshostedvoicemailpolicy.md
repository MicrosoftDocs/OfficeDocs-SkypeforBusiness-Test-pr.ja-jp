---
title: Remove-CsHostedVoicemailPolicy
TOCTitle: Remove-CsHostedVoicemailPolicy
ms:assetid: 13968bbe-1403-46de-b02a-ed61e712d1b3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398211(v=OCS.15)
ms:contentKeyID: 48271334
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsHostedVoicemailPolicy

 

_**トピックの最終更新日:** 2015-03-09_

Removes a hosted voice mail policy. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsHostedVoicemailPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

This command removes the hosted voice mail policy for the ExRedmond per-user policy.

    Remove-CsHostedVoicemailPolicy -Identity ExRedmond

## EXAMPLE 2

The command in Example 2 removes all per-user hosted voice mail policies. The command starts by calling the **Get-CsHostedVoicemailPolicy** cmdlet with a Filter of tag\*, which will retrieve all policies defined as per-user policies. That set of policies is then piped to the **Remove-CsHostedVoicemailPolicy** cmdlet, which deletes each one.

    Get-CsHostedVoicemailPolicy -Filter tag* | Remove-CsHostedVoicemailPolicy

## Detailed Description

This cmdlet removes a policy that specifies how to route unanswered calls to the user to a hosted Exchange ユニファイド メッセージング (UM) service.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Remove-CsHostedVoicemailPolicy** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsHostedVoicemailPolicy"}

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
<td><p>A unique identifier for the hosted voice mail policy that you want to remove. This identifier includes the scope (in the case of global), the scope and site (for a site policy, such as site:Redmond), or the policy name (for a per-user policy, such as HVUserPolicy).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Guid</p></td>
<td><p>Globally unique identifier (GUID) of the Skype for Business Online tenant account for the hosted voicemail policy being deleted. For example:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>You can return the tenant ID for each of your tenants by running this command:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy object. Accepts pipelined input of hosted voice mail policy objects.

## Return Types

This cmdlet does not return an object. It removes an object of type Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy.

## 関連項目

#### その他のリソース

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)

