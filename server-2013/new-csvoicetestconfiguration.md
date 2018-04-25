---
title: New-CsVoiceTestConfiguration
TOCTitle: New-CsVoiceTestConfiguration
ms:assetid: da312c27-bc89-46c3-a6c9-c098ed4e7df7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398961(v=OCS.15)
ms:contentKeyID: 48273736
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceTestConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

Creates a test scenario you can use to test phone numbers against specified routes and rules. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsVoiceTestConfiguration -Name <String> <COMMON PARAMETERS>

    New-CsVoiceTestConfiguration -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DialedNumber <String>] [-ExpectedRoute <String>] [-ExpectedTranslatedNumber <String>] [-ExpectedUsage <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-TargetDialplan <String>] [-TargetVoicePolicy <String>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

This example creates a new voice test configuration with default values that has the Identity TestConfig1.

    New-CsVoiceTestConfiguration -Identity TestConfig1

## EXAMPLE 2

This example creates a new voice test configuration named TestConfig1 and sets the TargetDialplan parameter to site:Redmond1. This will result in the tests for expected number, usage, and route to be run against the settings for the dial plan for the site Redmond1.

In this example we declared TestConfig1 without specifying the Identity parameter. Identity is a positional parameter, so the first value in the command following the cmdlet name is recognized by the cmdlet as the Identity.

    New-CsVoiceTestConfiguration TestConfig1 -TargetDialplan site:Redmond1

## EXAMPLE 3

This example creates a new voice test configuration named TestConfig1. This configuration will use the default values to test the DialedNumber 5551212 against an expected output (ExpectedTranslatedNumber) of +5551212. This expectation is based on the normalization rules associated with the dial plan that will be used when a test is run against this object. That test must be run using the **Test-CsVoiceTestConfiguration** cmdlet.

    New-CsVoiceTestConfiguration -Identity TestConfig1 -DialedNumber 5551212 -ExpectedTranslatedNumber +5551212

## Detailed Description

Before implementing voice routes and voice policies, it's a good idea to test them out on various phone numbers to ensure the results are what you're expecting. You can do this testing by creating test scenarios with this cmdlet.

The **New-CsVoiceTestConfiguration** cmdlet defines the voice route, usage, dial plan, and voice policy against which to test a specified phone number. All of this information can be defined and retrieved using other cmdlets; see the parameter descriptions for this topic for more information.

The configurations created with this cmdlet are tested using the **Test-CsVoiceTestConfiguration** cmdlet.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **New-CsVoiceTestConfiguration** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceTestConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>A string uniquely identifying this test scenario.</p>
<p>This string can be up to 32 characters in length and may contain any alphanumeric characters plus the backslash (\), period (.) or underscore (_).</p>
<p>The value of this parameter does not include scope because this object can be created only at the global scope. Therefore only a unique name is required.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>This parameter contains the same value as the Identity. If the Identity parameter is specified, you cannot include the Name parameter in your command. Likewise, if the Name parameter is specified, you cannot specify an Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>DialedNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>The phone number you want to use to test the policies, usages, etc.</p>
<p>Must be 512 characters or fewer.</p>
<p>Default: 1234</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedRoute</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>The name of the voice route expected to be used during the configuration test. If a different route is used, based on the target dial plan and voice policy, the test will fail. You can retrieve available voice routes by calling the <strong>Get-CsVoiceRoute</strong> cmdlet.</p>
<p>Must be 256 characters or fewer.</p></td>
</tr>
<tr class="even">
<td><p><em>ExpectedTranslatedNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>The phone number in the format you expect to see it after translation. This is the value of the DialedNumber parameter after normalization. If you run the <strong>Test-CsVoiceTestConfiguration</strong> cmdlet and the DialedNumber does not result in the value in ExpectedTranslatedNumber, the test will report as Fail.</p>
<p>Must be 512 characters or fewer.</p>
<p>Default: +1234</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedUsage</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>The name of the PSTN usage expected to be used during the configuration test. If a different PSTN usage is used, based on the target dial plan and voice policy, the test will fail. You can retrieve available usages by calling the <strong>Get-CsPstnUsage</strong> cmdlet.</p>
<p>Must be 256 characters or fewer.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>永続的な変更としてオブジェクトをコミットせずに、オブジェクト参照を作成します。このパラメーターを指定して呼び出したコマンドレットの出力を変数に割り当てる場合、オブジェクト参照のプロパティを変更し、コマンドレットに対応する Set- コマンドレットを呼び出してそれらの変更をコミットできます。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetDialplan</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>The Identity of the dial plan to be used for this test. Dial plans can be retrieved by called the <strong>Get-CsDialPlan</strong> cmdlet.</p>
<p>Must be 40 characters or fewer.</p>
<p>Default: Global</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetVoicePolicy</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>The Identity of the voice policy against which to run this test. Voice policies can be retrieved by calling the <strong>Get-CsVoicePolicy</strong> cmdlet.</p>
<p>Must be 40 characters or fewer.</p>
<p>Default: Global</p></td>
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

None.

## Return Types

This cmdlet creates an object of type Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration

## 関連項目

#### その他のリソース

[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)

