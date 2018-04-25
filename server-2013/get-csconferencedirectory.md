---
title: Get-CsConferenceDirectory
TOCTitle: Get-CsConferenceDirectory
ms:assetid: 2b7927ab-c6b3-42ce-9c27-9825cd47fd77
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425771(v=OCS.15)
ms:contentKeyID: 48271647
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDirectory

 

_**トピックの最終更新日:** 2015-03-09_

組織用に構成された会議ディレクトリに関する情報を戻します。会議ディレクトリは、ダイヤルイン会議ユーザーが会議情報を検索するのに役立ちます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsConferenceDirectory [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDirectory [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 に示すコマンドにより、組織用に構成されたすべての会議ディレクトリに関する情報が戻されます。

    Get-CsConferenceDirectory

## 例 2

例 2 では、ID が 2 の会議ディレクトリに関する情報が戻されます。ID は一意である必要があるため、このコマンドでは複数の会議ディレクトリが戻されることはありません。

    Get-CsConferenceDirectory -Identity 2

## 例 3

例 3 では、UserServer:atl-cs-001.litwareinc.com サービスに属するすべての会議ディレクトリが戻されます。これを行うため、このコマンドはまず、パラメーターを指定せずに **Get-CsConferenceDirectory** コマンドレットを呼び出して、組織内のすべての会議ディレクトリのコレクションを戻します。次に、このコレクションは **Where-Object** コマンドレットにパイプ処理され、Where-Object では、ServiceID が "UserServer:atl-cs-001.litwareinc.com" という文字列と一致するディレクトリのみを選択します。

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"}

## 解説

ダイヤルイン会議の URI (Uniform Resource Identifier) を作成すると、それらの URI に一意の SIP アドレスが割り当てられます。ただし、SIP アドレスは、SIP 対応ではないデバイス用に変換するのは困難です。たとえば、公衆交換電話網 (PSTN) の電話では、SIP アドレスを変換できません。このため、Lync Server は会議ディレクトリを使用して、そのようなデバイスがダイヤルイン会議の検索と接続を実行できるようにします。これを実現するため、各ダイヤルイン会議 URI に関連付けられるとともに、SIP URI ではなく整数値によって識別される、SIP 会議ディレクトリを作成します。PSTN 電話およびその他のデバイスは、会議に接続するときに (SIP URI ではなく) それらの番号を使用できます。ダイヤルイン会議への接続時にユーザーが入力する PSTN 会議の識別情報には、ディレクトリ番号が含まれています。

**Get-CsConferenceDirectory** コマンドレットにより、組織用に構成されたすべての会議ディレクトリに関する情報を戻すことができます。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが、**Get-CsConferenceDirectory** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDirectory"}

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
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>取得する会議ディレクトリ (複数可) の ID を指定するときに、ワイルドカードを使用できるようにします。ディレクトリの ID は数値であるため、このパラメーターは最小の値になります。ただし、次の構文を使用すると、数字の 3 で始まる ID を持つすべての会議ディレクトリが戻されます。-Filter &quot;3*&quot;。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>戻される会議ディレクトリの数値識別子 (例、7)。このパラメーターを省略すると、<strong>Get-CsConferenceDirectory</strong> コマンドレットは、組織で使用中のすべての会議ディレクトリに関する情報を戻します。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体からではなく、中央管理ストア のローカル レプリカから会議ディレクトリのデータを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsConferenceDirectory** コマンドレットは、パイプ処理された入力を受け入れません。

## 戻り値の種類

**Get-CsConferenceDirectory** コマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

