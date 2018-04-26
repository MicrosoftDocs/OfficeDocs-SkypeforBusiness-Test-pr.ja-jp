---
title: Get-CsConferenceDisclaimer
TOCTitle: Get-CsConferenceDisclaimer
ms:assetid: 2382aaef-9c5e-43f8-99de-6c880134db7d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425714(v=OCS.15)
ms:contentKeyID: 48271498
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDisclaimer

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用される会議の免責事項に関する情報を戻します。会議の免責事項は、ハイパーリンクを使用して会議に参加するユーザー (たとえば、Windows Internet Explorer などのブラウザーに会議へのリンクを貼り付けているユーザー) に表示されるメッセージです。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDisclaimer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 に示すコマンドにより、組織用に構成された会議免責事項に関する情報が戻されます。グローバル スコープで構成された単一の免責事項に限られているため、このコマンドを実行するときに ID を指定する必要はありません。

    Get-CSConferenceDisclaimer

## 解説

会議の設定を行う場合、管理者は、Lync Server によってホストされる会議に参加者が参加するときに表示する法的免責事項を含めることができます。一般に、この免責事項は、会議に関係する法規制および知的財産権について説明するために使用し、ユーザーは、免責事項で規定されている条項に同意せずに会議に参加することはできません。この免責事項は、ハイパーリンクを使用して会議に参加するユーザーにのみ表示されます。

**Get-CsConferenceDisclaimer** コマンドレットにより、組織の免責事項の本文と見出しを表示できます。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが、**Get-CsConferenceDisclaimer** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDisclaimer"}

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
<td><p>会議免責事項を参照するときに、ワイルドカード値を使用できるようにします。会議免責事項のグローバル インスタンスは 1 つしか存在できないため、Filter パラメーターを使用する理由はありません。ただし、次の構文を使用して、グローバルの免責事項を参照することができます。-Filter &quot;g*&quot;。この構文を使用すると、ID が文字 &quot;g&quot; で始まるすべての会議免責事項が戻されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>会議免責事項の一意の Identity。会議免責事項のグローバル インスタンスは 1 つしか存在できないため、<strong>Get-CsConferenceDisclaimer</strong> コマンドレットを呼び出すときに ID を指定する必要はありません。ただし、次の構文を使用して、グローバルの免責事項を参照することができます。-Identity global。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体からではなく、中央管理ストア のローカル レプリカから会議の免責事項のデータを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

**Get-CsConferenceDisclaimer** コマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

