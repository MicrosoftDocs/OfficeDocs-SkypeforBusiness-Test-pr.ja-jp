---
title: Set-CsUnassignedNumber
TOCTitle: Set-CsUnassignedNumber
ms:assetid: e7f52423-58d1-410a-9071-731bde45d3d4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399033(v=OCS.15)
ms:contentKeyID: 48274014
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUnassignedNumber

 

_**トピックの最終更新日:** 2015-03-09_

割り当てられていない番号の既存の範囲と、それらの番号に適用されるルーティング ルールを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsUnassignedNumber [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -AnnouncementName <String> -AnnouncementService <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Priority <Int32>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、名前 UNSet1 の割り当てられていない番号の範囲を変更しています。最初に、Identity パラメーターの値として UNSet1 を渡しています。これは、変更しようとする、割り当てられていない番号の範囲の名前です。次に、NumberRangeStart パラメーター (+14255551000) および NumberRangeEnd (+14255551900) パラメーターを使用して、指定されたアナウンスまたは自動アテンダントの適用先となる割り当てられていない番号の範囲を変更します。

    Set-CsUnassignedNumber -Identity UNSet1 -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551900"

## 例 2

この例では、現在 "Welcome" という文字列を名前に含んでいるアナウンスがある、すべての割り当てられていない番号の範囲の設定のアナウンスを変更しています。まず **Get-CsUnassignedNumber** コマンドレットを呼び出して、割り当てられていない番号設定をすべて取得しています。その設定のコレクションを **Where-Object** コマンドレットにパイプ処理し、コレクションを絞り込んで AnnouncementName プロパティに文字列 Welcome を含む (-match) 設定のみにしています。それらの設定を取得したら **Set-CsUnassignedNumber** コマンドレットにパイプ処理し、AnnouncementService パラメーターを使ってアナウンス サービスのアプリケーション サーバー ID (ApplicationServer:redmond.litwareinc.com) を変更し、AnnouncementName パラメーターを使って新しいアナウンスの名前 (Help Desk Announcement) を変更しています。新しいアナウンスの名前が異なりサービス ID が同じ場合も、サービス ID を名前と共に指定する必要があります。

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"} | Set-CsUnassignedNumber -AnnouncementService ApplicationServer:redmond.litwareinc.com -AnnouncementName "Help Desk Announcement"

## 解説

割り当てられていない番号とは、組織には割り当てられているが特定のユーザーや電話には割り当てられていない電話番号のことです。割り当てられていない番号が呼び出された場合に、その呼び出しが適切な宛先へルーティングされるように Lync Server を設定できます。このコマンドレットは、そうしたルーティングを定義している設定を変更します。

このコマンドレット用の設定の一部を変更するためには、既にシステムで、アナウンスが定義されているか、Exchange UM 自動アテンダントが設定されている必要があります。アナウンスがあるどうかを確認するには、**Get-CsAnnouncement** コマンドレットを呼び出します。新しいアナウンスを作成するには、**New-CsAnnouncement** コマンドレットを呼び出します。Exchange UM 自動アテンダント設定を確認するには、**Get-CsExUmContact** コマンドレットを実行します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーは **Set-CsUnassignedNumber** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUnassignedNumber"}

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
<td><p><em>AnnouncementName</em></p></td>
<td><p>必須</p></td>
<td><p>String</p></td>
<td><p>この番号の範囲の呼び出し処理に使用するアナウンスの名前です。</p></td>
</tr>
<tr class="even">
<td><p><em>AnnouncementService</em></p></td>
<td><p>必須</p></td>
<td><p>String</p></td>
<td><p>アナウンス サーバーの完全修飾ドメイン名 (FQDN) またはサービス ID です。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExUmAutoAttendantPhoneNumber</em></p></td>
<td><p>必須</p></td>
<td><p>String</p></td>
<td><p>この範囲内の呼び出しのルーティング先になる Exchange UM 自動アテンダントの電話番号です。このパラメーターに値を割り当てるには、Exchange UM 自動アテンダントの連絡先が設定済みである必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>変更する割り当てられていない番号の範囲の一意の名前です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>DisplayAnnouncementVacantNumberRange</p></td>
<td><p>割り当てられていない番号設定を格納するオブジェクトへの参照です。このオブジェクトは Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange 型である必要があり、<strong>Get-CsUnassignedNumber</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>割り当てられていない番号の範囲の最後の番号です。NumberRangeStart で指定した番号以上である必要があります。1 つの番号の範囲を指定する場合は、NumberRangeStart と NumberRangeEnd に同じ番号を使用します。</p>
<p>この番号は正規表現 (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})? に一致する必要があります。これは、番号が文字列 tel: で始まり (この文字列を指定しなかった場合は、自動的に追加されます)、正符号 (+)、1 ～ 9 の数字であることを意味します。使用できる電話番号は最大 17 桁で、その後に内線番号を付けることができます。内線番号は ;ext= の後に番号が続く形式です。</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>割り当てられていない番号の範囲の最初の番号です。NumberRangeEnd で指定した値以下である必要があります。</p>
<p>この番号は正規表現 (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})? に一致する必要があります。これは、番号が文字列 tel: で始まり (この文字列を指定しなかった場合は、自動的に追加されます)、正符号 (+)、1 ～ 9 の数字であることを意味します。使用できる電話番号は最大 17 桁で、その後に内線番号を付けることができます。内線番号は ;ext= の後に番号が続く形式です。</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>割り当てられていない番号の範囲は重複してもかまいません。番号が複数の範囲に含まれている場合は、最も優先度の高い範囲が有効になります。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange オブジェクト。割り当てられていない番号オブジェクトのパイプ処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[New-CsAnnouncement](new-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)

