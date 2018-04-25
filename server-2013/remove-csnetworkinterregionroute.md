---
title: Remove-CsNetworkInterRegionRoute
TOCTitle: Remove-CsNetworkInterRegionRoute
ms:assetid: 91948c03-2bcb-4e25-b0b6-23827e85bbb3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398743(v=OCS.15)
ms:contentKeyID: 48272863
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterRegionRoute

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 構成内のネットワーク地域に接続するルートを削除します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsNetworkInterRegionRoute -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 は ID が NA\_APAC\_Route のルートを削除します。

    Remove-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## 例 2

例 2 は NorthAmerica 地域を含むすべての地域ルートを削除します。コマンドの最初の部分では、**Get-CsNetworkInterRegionRoute** コマンドレットを呼び出しています。このコマンドレットはパラメーターを指定せずに呼び出され、すべての地域ルートを取得します。次に、このルート コレクションを **Where-Object** コマンドレットへパイプ処理しています。**Where-Object** コマンドレットによって、ルート内の地域の 1 つとして NorthAmerica が定義されているルートのみのコレクションに絞り込みます。このコマンドレットでは、ルートの NetworkRegionlD1 値が NorthAmerica に等しい (-eq) かどうか、または (-or)、NetworkRegionlD2 値が NorthAmerica に等しいかどうかを確認することで、これを実行します。NorthAmerica 地域を含むルートのみがコレクションに含まれるようにした後、そのコレクションを **Remove-CsNetworkInterRegionRoute** コマンドレットへパイプ処理し、それらの各ルートを削除しています。

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"} | Remove-CsNetworkInterRegionRoute

## 解説

CAC 構成内の各地域から他の各地域にアクセスするいくつかの方法が必要です。地域のリンクが地域間の接続に対する帯域幅制限を設定し、物理リンクも表す一方、ルートはある地域から別の地域へ接続が通過するリンクされたパスを決定します。このコマンドレットはこのようなルートの関連付けのいずれかを削除します。

このコマンドレットを実行できるユーザー: 既定では、**Remove-CsNetworkInterRegionRoute** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterRegionRoute"}

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
<td><p>削除するネットワーク地域ルートの一意の識別子です。ネットワーク地域ルートはグローバル スコープのみで作成されるため、この識別子ではスコープを指定する必要はありません。代わりに、そのルートを識別する一意の名前の文字列が含まれます。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType オブジェクトです。ネットワーク地域間ルート オブジェクトのパイプ処理による入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 型のオブジェクトを削除します。

## 関連項目

#### その他のリソース

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

