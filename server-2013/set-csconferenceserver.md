---
title: Set-CsConferenceServer
TOCTitle: Set-CsConferenceServer
ms:assetid: 90f9f1f1-0029-4f97-a8f4-719523cfad56
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398738(v=OCS.15)
ms:contentKeyID: 48272844
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceServer

 

_**トピックの最終更新日:** 2015-03-09_

音声ビデオ会議サーバー (会議サーバーとも呼ばれます) のプロパティを変更します。会議サーバーは、会議において音声とビデオ (A/V) を利用できるようにします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsConferenceServer [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AppSharingSipPort <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-AudioVideoSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-DataPsomPort <UInt16>] [-EdgeServer <String>] [-Force <SwitchParameter>] [-ImSipPort <UInt16>] [-MeetingPsomPort <UInt16>] [-PhoneSipPort <UInt16>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドは、会議サーバー ConferencingServer:atl-cs-001.litwareinc.com のインスタント メッセージング SIP ポートを変更します。この例では、ポートは 5075 に変更されます。

    Set-CsConferenceServer -Identity "ConferencingServer:atl-cs-001.litwareinc.com" -ImSipPort 5075

## 例 2

例 2 は、例 1 で示したコマンドの変化形です。ただし、この例では、組織のすべての会議サーバーのインスタント メッセージング SIP ポートが変更されます。これを行うため、まず **Get-CsService** コマンドレットと ConferencingServer パラメーターを使用して、現在使用されているすべての会議サーバーのコレクションを戻しています。次に、このコレクションを **ForEach-Object** コマンドレットへパイプ処理し、コレクション内の各サーバーに対して **Set-CsConferenceServer** コマンドレットを実行して、ImSipPort を 5075 に設定しています。

    Get-CsService -ConferencingServer | ForEach-Object {Set-CsConferenceServer -Identity $_.Identity -ImSipPort 5075}

## 解説

会議サーバー (音声ビデオ会議サーバーとも呼ばれます) は、会議において音声とビデオを利用できるようにするために使われます。そして、**Set-CsConferenceServer** コマンドレットを使用して、これらのサーバーのプロパティを変更できます。具体的には、オーディオ トラフィック、ビデオ トラフィック、アプリケーション共有などに使用するポートを指定することができます。また、**Set-CsConferenceServer** コマンドレットを使用して、特定のサーバーを エッジ サーバー または アーカイブ サーバー に関連付けることができます。

このコマンドレットを実行できるユーザー: 既定では、**Set-CsConferenceServer** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceServer"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>アプリケーション共有に割り当てられたポートの合計数です。開かれる実際のポートは AppSharingPortStart に指定された値から始まり、AppSharingPortCount に指定されたポート数まで続きます。たとえば、AppSharingPortStart を 60000 に、AppSharingPortCount を 100 に設定すると、ポート 60000 から 60099 までがアプリケーション共有に使用されます。</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>アプリケーション共有に割り当てるメディア ポート範囲の先頭のポートです。次に例を示します。–AppSharingPortStart 60000。</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingSipPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>アプリケーション共有要求をリッスンする際に使用する SIP ポートです。アプリケーション共有において実際に使用するポートは、AppSharingPortStart と AppSharingPortCount を使って構成します。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortCount</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>オーディオ トラフィックの送受信に割り当てられたポートの合計数です。開かれる実際のポートは AudioPortStart に指定された値から始まり、AudioPortCount に指定されたポート数まで続きます。たとえば、AudioPortStart を 60000 に、AudioPortCount を 100 に設定すると、ポート 60000 から 60099 までがオーディオ トラフィックに使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortStart</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>オーディオ トラフィックの送受信に割り当てるメディア ポート範囲の先頭のポートです。次に例を示します。–AudioPortStart 60000。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioVideoSipPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>オーディオおよびビデオ サービスの着信要求をリッスンする際に使用する SIP ポートです。オーディオ トラフィックおよびビデオ トラフィックにおいて実際に使用するポートは、AudioPortCount、AudioPortStart、VideoPortCount、および VideoPortStart を使って構成します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>DataPsomPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>永続共有オブジェクト モデル (PSOM) プロトコルで使用するデータ ポートです。</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>会議サーバーに関連付ける エッジ サーバー のサービスの場所です。次に例を示します。-EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>変更する会議サーバーのサービスの場所です。次に例を示します。-Identity &quot;ConferencingServer:atl-cs-001.litwareinc.com&quot;</p>
<p>なお、会議サーバーを指定する場合、プレフィックス &quot;ConferencingServer:&quot; は省略できます。次に例を示します。-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>ImSipPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>インスタント メッセージング トラフィックに使用するポートです。</p></td>
</tr>
<tr class="odd">
<td><p><em>MeetingPsomPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>永続共有オブジェクト モデル (PSOM) プロトコルで使用するポートです。PSOM プロトコルは、マイクロソフトの会議用プロトコルです。</p></td>
</tr>
<tr class="even">
<td><p><em>PhoneSipPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>テレフォニー トラフィックに使用されるポートです。</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>ビデオ トラフィックの送受信に割り当てられたポートの合計数です。開かれる実際のポートは VideoPortStart に指定された値から始まり、VideoPortCount に指定されたポート数まで続きます。たとえば、VideoPortStart を 60000 に、VideoPortCount を 100 に設定すると、ポート 60000 から 60099 までがビデオ トラフィックに使用されます。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>ビデオ トラフィックの送受信に割り当てられたポートの範囲内の最初のポートです。次に例を示します。–VideoPortStart 60000。</p></td>
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

なし。**Set-CsConferenceServer** コマンドレットは、パイプ処理による入力を受け入れません。

## 戻り値の種類

**Set-CsConferenceServer** コマンドレットは、オブジェクトまたは値を戻しません。代わりに、Microsoft.Rtc.Management.Xds.DisplayConferenceServer オブジェクトの既存のインスタンスが変更されます。

## 関連項目

#### その他のリソース

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[Get-CsService](get-csservice.md)

