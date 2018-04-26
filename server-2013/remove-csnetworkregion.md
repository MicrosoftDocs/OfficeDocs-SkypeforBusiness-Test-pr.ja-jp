---
title: Remove-CsNetworkRegion
TOCTitle: Remove-CsNetworkRegion
ms:assetid: 661dce40-f601-4181-b8f1-3277a76d5df4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398466(v=OCS.15)
ms:contentKeyID: 48272314
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegion

 

_**トピックの最終更新日:** 2015-03-09_

既存のネットワーク地域を削除します。ネットワーク地域は、エンタープライズ ネットワークのネットワーク ハブまたはバックボーンです。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsNetworkRegion -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、Identity が NorthAmerica のネットワーク地域を削除します。identity は一意なので、このコマンドは 1 つのネットワーク地域のみを削除します。

    Remove-CsNetworkRegion -Identity NorthAmerica

## 例 2

この例では、セントラル サイト Redmond と関連付けられたすべてのネットワーク地域を削除します。まず、**Get-CsNetworkRegion** コマンドレットをパラメーターを指定せずに呼び出して、Lync Server 展開用に定義されたすべてのネットワーク地域のコレクションを取得します。次にこのコレクションを、**Where-Object** コマンドレットにパイプ処理します。**Where-Object** コマンドレットは、このコレクションをフィルター処理して、CentralSite 値が site:Redmond と等しい (-eq) 項目 (ネットワーク地域) のみを戻します。コレクションの内容をそれらの項目に絞り込んだら、この新しいコレクションを **Remove-CsNetworkRegion** コマンドレットにパイプ処理して、そのコレクション内の各項目を削除します。

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"} | Remove-CsNetworkRegion

## 例 3

この例では、Identity が NorthAmerica のネットワーク地域を削除します。ただし、地域がサイトに関連付けられている場合は、地域を削除することはできません。そのため、この例ではまず、NorthAmerica 地域とサイト間の関連付けをすべて削除します。

まず、**Get-CsNetworkSite** コマンドレットをパラメーターを指定せずに呼び出して、Lync Server 展開用に定義されたすべてのネットワーク サイトのコレクションを取得します。次にこのコレクションを、**Where-Object** コマンドレットにパイプ処理します。**Where-Object** コマンドレットは、このコレクションをフィルター処理して、NetworkRegionID 値が NorthAmerica に等しい (-eq) 項目 (ネットワーク サイト) のみを戻します。コレクションの内容をこれらの項目に絞り込んだら、この新しいコレクションを **Set-CsNetworkSite** コマンドレットにパイプ処理します。NorthAmerica の NetworkRegionID を持つサイトごとに、NetworkRegionID を Null ($null) に設定します。これにより、サイトの地域への参照が削除されます。ただし、バイパス ID がサイトに関連付けられていない場合、サイトはバイパス ID を持つことはできません。そのため、NetworkRegionID を Null に設定して地域への参照を削除することに加えて、BypassID を Null に設定することで、バイパスの関連付けも削除する必要があります。

行 1 の完了後、NorthAmerica 地域に関連付けられていたサイトは、地域またはバイパス設定に結び付けられなくなります。この時点で行 2 を呼び出して、ネットワーク地域を削除します。

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"} | Set-CsNetworkSite -NetworkRegionID $null -BypassID $null
    Remove-CsNetworkRegion -Identity "NorthAmerica"

## 解説

ネットワーク地域により、複数の地理的領域にわたって、ネットワークのさまざまな部分を相互接続します。すべてのネットワーク地域は、セントラル サイトと関連付ける必要があります。セントラル サイトは、帯域幅ポリシー サービスが実行されているデータセンター サイトです。ネットワーク地域を削除する場合は、このコマンドレットを使用します。

ネットワーク地域がネットワークサイトに関連付けられている場合 (つまり、任意のサイトの NetworkRegionID が地域の Identity と同じ場合)、そのネットワーク地域を削除することはできません。サイトに関連付けられている地域を削除しようとすると、エラー メッセージが表示されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Remove-CsNetworkRegion** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegion"}

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
<td><p>削除するネットワーク地域の一意の識別子。Identity は、その地域を一意に識別する文字列形式となります。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType オブジェクト。パイプライン処理されたネットワーク地域オブジェクトの入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 型のオブジェクトを削除します。

## 関連項目

#### その他のリソース

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)

