---
title: Remove-CsConferenceDirectory
TOCTitle: Remove-CsConferenceDirectory
ms:assetid: c2c62a14-f3f3-472f-bf91-1fcea9e45425
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412961(v=OCS.15)
ms:contentKeyID: 48273511
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDirectory

 

_**トピックの最終更新日:** 2015-03-09_

既存の会議ディレクトリを削除します。会議ディレクトリは、ダイヤルイン会議ユーザーが会議情報を検索するのに役立ちます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 のコマンドを実行すると、ID 2 を持つ会議ディレクトリが削除されます。

    Remove-CsConferenceDirectory -Identity 2

## 例 2

例 2 では、UserServer:atl-cs-001.litwareinc.com というサービスにあるすべての会議ディレクトリが削除されます。これを行うため、まず **Get-CsConferenceDirectory** コマンドレットをパラメーターを指定せずに呼び出して、組織内で現在使用中の会議ディレクトリをすべて含むコレクションを取得します。次に、このコレクションを **Where-Object** コマンドレットにパイプ処理して、サービス UserServer:atl-cs-001.litwareinc.com でホストされるディレクトリだけを取得します。次に、このフィルター処理済みのコレクションを **Remove-CsConferenceDirectory** コマンドレットにパイプ処理して削除します。

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"} | Remove-CsConferenceDirectory

## 解説

ダイヤルイン会議の Uniform Resource Identifier (URI) を作成すると、作成した URI に対して一意の SIP アドレスが割り当てられます。ただし、SIP アドレスを、SIP 対応ではないデバイス用に変換するのは困難です。たとえば、公衆交換電話網 (PSTN) の電話は SIP アドレスを変換できません。このため、Lync Server は会議ディレクトリを使用して、このようなデバイスがダイヤルイン会議の検索と接続を実行できるようにします。これは、各ダイヤルイン会議 URI に関連付けられ、SIP URI ではなく整数値で識別される SIP 会議ディレクトリを作成することで実現されます。これにより PSTN 電話およびその他のデバイスは、会議に接続するときに (SIP URI ではなく) それらの番号を使用することができます。ダイヤルイン会議への接続時にユーザーが入力する PSTN 会議の識別情報には、ディレクトリ番号が含まれています。

会議ディレクトリは、**New-CsConferenceDirectory** コマンドレットを使用して作成します。これらのディレクトリのいくつかを削除することが必要な場合があります。たとえば、ディレクトリをホストするプールを使用停止にする必要が生じた場合です。会議ディレクトリは、**Remove-CsConferenceDirectory** コマンドレットを呼び出すことで削除できます。ディレクトリをあるプールから別のプールに移動する必要がある場合は、**Move-CsConferenceDirectory** コマンドレットを呼び出します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Remove-CsConferenceDirectory** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDirectory"}

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
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>削除する会議ディレクトリの ID 番号。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定すると、ディレクトリをホストするプールが現在使用できなくても、会議ディレクトリを削除します。既定では、<strong>Remove-CsConferenceDirectory</strong> コマンドレットは対応するプールと通信できない場合はディレクトリを削除しません。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories オブジェクト。**Remove-CsConferenceDirectory** コマンドレットは、会議ディレクトリ オブジェクトのパイプライン入力を受け入れます。

## 戻り値の種類

なし。代わりに、**Removes-CsConferenceDirectory** コマンドレットが Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories オブジェクトのインスタンスを削除します。

## 関連項目

#### その他のリソース

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)

