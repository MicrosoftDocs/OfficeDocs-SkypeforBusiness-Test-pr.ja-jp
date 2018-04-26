---
title: Remove-CsCallParkOrbit
TOCTitle: Remove-CsCallParkOrbit
ms:assetid: b8e7c236-f8de-45bd-966b-60c815b37aed
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412901(v=OCS.15)
ms:contentKeyID: 48273397
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCallParkOrbit

 

_**トピックの最終更新日:** 2015-03-09_

特定のコール パーク オービット範囲を削除します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsCallParkOrbit -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、**Remove-CsCallParkOrbit** コマンドレットを使用して、Redmond CPO 1 という名前のコール パーク オービット範囲を削除します。

    Remove-CsCallParkOrbit -Identity "Redmond CPO 1"

## 例 2

この例のコマンドは、組織で定義されていたすべてのコール パーク オービット範囲を削除します。最初に、**Get-CsCallParkOrbit** コマンドレットを、パラメーターを指定せずに呼び出して、定義済みのすべてのコール パーク オービット範囲を取得します。次に、コール パーク オービット範囲のコレクションを **Remove-CsCallParkOrbit** コマンドレットにパイプ処理します。これにより、各コール パーク オービットが削除されます。

    Get-CsCallParkOrbit | Remove-CsCallParkOrbit

## 例 3

このコマンドでは、"Redmond 501"、"CP Redmond 1"、"ARedmond" など、Identity に "Redmond" という文字列を含むすべてのコール パーク オービット範囲を削除します。このコマンドでは最初に、**Get-CsCallParkOrbit** コマンドレットを Filter パラメーターを指定して呼び出し、文字列 Redmond を含む Identity のコール パーク オービット範囲をすべて取得します。このコレクションは **Remove-CsCallParkOrbit** コマンドレットにパイプ処理され、これにより、コレクションの内容がすべて削除されます。

    Get-CsCallParkOrbit -Filter *Redmond* | Remove-CsCallParkOrbit

## 解説

**Remove-CsCallParkOrbit** コマンドレットは、Identity パラメーター (このパラメーターは必須です) に渡された名前を持つ、コール パーク オービット範囲を削除します。組織内の各コール パーク オービットには、一意の番号範囲が設定されている必要があります。コール パーク オービットを削除すると、そのコール パーク オービットの番号範囲が解放されます。解放された番号は、新しく定義するコール パーク オービットで使用できるようになります。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Remove-CsCallParkOrbit** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCallParkOrbit"}

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
<td><p>コール パーク オービット範囲の名前。この名前は、コール パーク オービット範囲を定義する際に管理者によって割り当てられたものです。</p></td>
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
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
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

Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit オブジェクト。コール パーク オービット オブジェクトのパイプライン処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit 型のオブジェクトが削除されます。

## 関連項目

#### その他のリソース

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

