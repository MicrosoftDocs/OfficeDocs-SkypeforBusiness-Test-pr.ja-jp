---
title: New-CsConferenceDirectory
TOCTitle: New-CsConferenceDirectory
ms:assetid: fd5a4369-10cd-4337-94df-51bcaee4fde9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg413080(v=OCS.15)
ms:contentKeyID: 48274205
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsConferenceDirectory

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用できるように新しい会議ディレクトリを作成します。会議ディレクトリは、ダイヤルイン会議ユーザーが会議情報を検索するのに役立ちます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsConferenceDirectory -HomePool <String> -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

Identity が 42 である新しい会議ディレクトリを作成します。このディレクトリは、atl-cs-001.litwareinc.com というプールでホストされます。

    New-CsConferenceDirectory -Identity 42 -HomePool "atl-cs-001.litwareinc.com"

## 解説

ダイヤルイン会議 URI (Uniform Resource Identifier) を作成すると、それらの URI に対して一意の SIP アドレスが割り当てられます。ただし、SIP アドレスを、SIP 対応ではないデバイス用に変換するのは困難です。たとえば、PSTN (公衆交換電話網) 電話機は SIP アドレスを変換できません。このため、Lync Server は会議ディレクトリを使用して、そのようなデバイスがダイヤルイン会議の検索と接続を実行できるようにします。これを実行するために、各ダイヤルイン会議 URI に関連付けられた SIP 会議ディレクトリを作成し、SIP URI ではなく整数値を使用して識別します。これにより PSTN 電話およびその他のデバイスは、会議に接続するときに (SIP URI ではなく) それらの番号を使用することができます。ダイヤルイン会議への接続時にユーザーが入力する PSTN 会議の識別情報には、ディレクトリ番号が含まれています。

新しい会議ディレクトリを作成するには、**New-CsConferenceDirectory** コマンドレットを呼び出します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**New-CsConferenceDirectory** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsConferenceDirectory"}

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
<th>パラメーター</th>
<th>必須かどうか</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>HomePool</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>新しい会議ディレクトリをホストするレジストラー プールの完全修飾ドメイン名 (FQDN) です。次に例を示します。-Identity atl-cs-001.litwareinc.com です。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>新しい会議ディレクトリに関する一意の識別子 (数値) です。Identity は、0 ～ 9999 の範囲で任意の整数値に設定できます。ただし、Identity は一意である必要があります (たとえば、575 という同じ Identity を持つ 2 つのディレクトリを作成することはできません)。新しいディレクトリを作成するときに、数値の順序に従う必要はありません。たとえば、Identity 999 を持つディレクトリを作成し、その後に Identity 2 を持つディレクトリを作成し、さらに Identity 438 を持つディレクトリを作成することができます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**New-CsConferenceDirectory** コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories オブジェクトの新しいインスタンスを作成します。

## 関連項目

#### その他のリソース

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

