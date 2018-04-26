---
title: Set-CsUICulture
TOCTitle: Set-CsUICulture
ms:assetid: 53fbc126-1df9-4ea0-8055-4e9530ab89d6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398354(v=OCS.15)
ms:contentKeyID: 48272101
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUICulture

 

_**トピックの最終更新日:** 2015-03-09_

Enables you to modify the culture (that is, the language and regional settings) used by the Lync Server 管理シェル. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsUICulture -Culture <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

The command shown in Example 1 sets the culture for the Lync Server 管理シェル to U.S. English. This is done by using the language code en-US.

    Set-CsUICulture -Culture "en-US"

## EXAMPLE 2

Example 2 sets the culture for the Lync Server 管理シェル to the default culture value. The default value is the culture setting used when you originally installed Lync Server.

    Set-CsUICulture -Culture "default"

## Detailed Description

Although Lync Server is available in multiple languages, the software is not a true Multilingual User Interface (MUI) application. Among other things, this means that the user interface for the Lync Server 管理シェル does not change languages any time you change the operating system language. For example, suppose you have installed the U.S. English version of Lync Server and are also running the Windows operating system under U.S. English. If you change the operating system culture (that is, the language and regional settings) to Danish, the Lync Server 管理シェル will not automatically follow suit; instead, the Lync Server 管理シェル user interface (including error messages and help text) will remain in U.S. English. If you need to change the culture for the Lync Server 管理シェル, you must run the **Set-CsUICulture** cmdlet.

There are two things to keep in mind when using the **Set-CsUICulture** cmdlet. First, the cmdlet can only be used to modify Lync Server 管理シェル settings on the local computer; the **Set-CsUICulture** cmdlet cannot change a remote instance of Lync Server 管理シェル. This is due to the fact that all the users of a computer share the same instance of the Lync Server 管理シェル: allowing a remote user to change the culture would instantly change the culture for any other users of the Lync Server 管理シェル, including the local user.

Second, you can only set the language to U.S. English ("en-US") or to the language used when you initially installed Lync Server ("default"). For example, if you originally installed an Italian version of Lync Server, then you have two choices for configuring the UI culture: English or Italian.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Set-CsUICulture** cmdlet locally: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins.

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
<td><p><em>Culture</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>Enables you to specify the culture used for the Lync Server 管理シェル. Set the culture to &quot;en-US&quot; for U.S. English, or set the culture to &quot;default&quot; to use the language used when you originally installed Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
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

None. The **Set-CsUICulture** cmdlet does not accept pipelined input.

## Return Types

The **Set-CsUICulture** cmdlet does not return any values or objects. Instead, the cmdlet modifies existing instances of the System.Globalization.CultureInfo class.

## 関連項目

#### その他のリソース

[Get-CsUICulture](get-csuiculture.md)

