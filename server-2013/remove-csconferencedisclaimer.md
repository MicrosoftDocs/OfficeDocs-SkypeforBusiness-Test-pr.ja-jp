---
title: Remove-CsConferenceDisclaimer
TOCTitle: Remove-CsConferenceDisclaimer
ms:assetid: 196252a1-2526-4944-9064-01d1846f3266
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398243(v=OCS.15)
ms:contentKeyID: 48271410
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDisclaimer

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用される会議免責事項のヘッダーと本文のテキストをクリアします。会議についての免責事項は、ハイパーリンクを使用して会議に参加するユーザー (たとえば、Windows Internet Explorer などのブラウザーに会議へのリンクを貼り付けたユーザー) に表示されるメッセージです。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsConferenceDisclaimer -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 は、グローバルの免責事項のプロパティ値をリセットします。つまり、免責事項のヘッダーと本文の両方が NULL 値に設定されて、免責事項が空白になります。

    Remove-CsConferenceDisclaimer -Identity global

## 解説

会議設定を構成する際に、管理者は、Lync Server によってホストされる会議にユーザーが参加したときに、これらの参加者に表示する法的な免責事項を含めることができます。一般に、この免責事項は、会議に関係する法規制および知的財産権について説明するために使用します。ユーザーは、免責事項で規定されている条項に同意せずに会議に参加することはできません。この免責事項は、ハイパーリンクを使用して会議に参加するユーザーにのみ表示されます。

Lync Server では、会議についての免責事項のグローバル インスタンスを 1 つ持つことができます。**Remove-CsConferenceDisclaimer** コマンドレットを使用すると、会議についての免責事項をリセットできます。このコマンドレットを実行すると、免責事項のヘッダーと免責事項の本文の両方が NULL 値に設定されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Remove-CsConferenceDisclaimer** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDisclaimer"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>削除する会議免責事項の一意の識別子。1 つのグローバル インスタンスの会議についての免責事項のみ利用できますが、<strong>Remove-CsConferenceDisclaimer</strong> コマンドレットを呼び出すときには、さらに Identity パラメーターを使用する必要があります。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer オブジェクト。**Remove-CsConferenceDisclaimer** コマンドレットは会議についての免責事項オブジェクトのパイプライン処理された入力を受け入れます。

## 戻り値の種類

なし。代わりに、**Remove-CsConferenceDisclaimer** コマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer オブジェクトの既存のインスタンスが既定のプロパティ値にリセットされます。

## 関連項目

#### その他のリソース

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

