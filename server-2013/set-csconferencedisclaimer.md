---
title: Set-CsConferenceDisclaimer
TOCTitle: Set-CsConferenceDisclaimer
ms:assetid: 97afce6d-b031-466d-a170-3ca50d6df245
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398776(v=OCS.15)
ms:contentKeyID: 48272962
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceDisclaimer

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用される会議についての免責事項のプロパティ値を変更します。会議についての免責事項は、Windows Internet Explorer などのブラウザーに会議のリンクを貼り付けるなど、ハイパーリンクを使って会議に参加するユーザーに対して表示するメッセージです。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferenceDisclaimer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Body <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Header <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドは、組織の会議についての免責事項の Header プロパティと Body プロパティを両方変更します。この免責事項は 1 つしか使用できないため、**Set-CsConferenceDisclaimer** コマンドレットを実行する際、Identity を指定する必要はありません。

    Set-CsConferenceDisclaimer -Header "Litwareinc.com Online Conference" -Body "Important note: Conferencing proceedings are recorded and archived."

## 解説

管理者は、会議の設定を構成する際、Lync Server がホストする会議への参加時に、参加者に対して表示する法的免責事項を指定できます。一般に、この免責事項は、会議に関係する法規制および知的財産権について説明するために使用します。ユーザーは、免責事項の規定に同意しなければ会議に参加できません。ただし、この免責事項が表示されるのは、ハイパーリンクを使って会議に参加するユーザーに対してのみです。

Lync Server では、会議についての免責事項のグローバル インスタンスを 1 つ使用できます。**Set-CsConferenceDisclaimer** コマンドレットを使用して、組織内で使用する会議についての免責事項を変更できます。

このコマンドレットを実行できるユーザー: 既定では、**Set-CsConferenceDisclaimer** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceDisclaimer"}

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
<td><p><em>Body</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>会議についての免責事項の内容です。</p></td>
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
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>Header</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>会議についての免責事項に与えられたタイトルです。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>会議についての免責事項の一意の Identity です。会議についての免責事項のグローバル インスタンスは 1 つしか使用できないので、<strong>Set-CsConferenceDisclaimer</strong> コマンドレットを呼び出す際、Identity を指定する必要はありません。ただし、グローバルの免責事項を参照するため、次の構文を使用できます。-Identity global。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>ConferenceDisclaimer オブジェクト</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer オブジェクトです。**Set-CsConferenceDisclaimer** コマンドレットは、会議についての免責事項オブジェクトのパイプ処理による入力を受け入れます。

## 戻り値の種類

**Set-CsConferenceDisclaimer** コマンドレットは、オブジェクトまたは値を戻しません。代わりに、Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer オブジェクトの既存のインスタンスを変更します。

## 関連項目

#### その他のリソース

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)

