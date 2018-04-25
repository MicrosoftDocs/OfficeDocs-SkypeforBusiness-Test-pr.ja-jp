---
title: Get-CsNetworkInterRegionRoute
TOCTitle: Get-CsNetworkInterRegionRoute
ms:assetid: 31c38d92-1cef-40fe-bd04-26e5b373703e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425817(v=OCS.15)
ms:contentKeyID: 48271675
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterRegionRoute

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 構成内のネットワーク地域間を接続するルートを 1 つ以上取得します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterRegionRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 では、Identity が NA\_APAC\_Route になっているルートを取得します。

    Get-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## 例 2

例 2 では、Filter パラメーターを使用して、Identity の一部に文字列 APAC を含むすべてのルートを取得します。

    Get-CsNetworkInterRegionRoute -Filter *APAC*

## 例 3

この例では、ネットワーク地域リンク NA\_EMEA を使用するすべての地域のルートを取得します。このコマンドはまず、**Get-CsNetworkInterRegionRoute** コマンドレットを呼び出します。パラメーターを指定せずにこのコマンドレットを呼び出すと、CAC 構成によって定義されているすべてのルートを取得できます。次に、このルートのコレクションは **Where-Object** コマンドレットにパイプ処理されます。**Where-Object** コマンドレットによりそのコレクションが取得され、コレクション内で NetworkRegionLinks 一覧内に NA\_EMEA という値が含まれるすべての項目が取得されます。

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionLinks -eq "NA_EMEA"}

## 例 4

例 4 では、NorthAmerica 地域を含むすべての地域ルートを取得します。コマンドの最初の部分で、**Get-CsNetworkInterRegionRoute** コマンドレットを呼び出します。このコマンドレットはパラメーターを指定せずに呼び出され、すべての地域ルートを取得します。次に、このルートのコレクションは **Where-Object** コマンドレットにパイプ処理されます。**Where-Object** コマンドレットは、ルート内の地域の 1 つとして NorthAmerica が定義されているルートのみにコレクションを絞り込みます。このコマンドレットでは、ルートの NetworkRegionlD1 値が NorthAmerica に等しい (-eq) かどうか、または (-or)、NetworkRegionlD2 値が NorthAmerica に等しいかどうかを確認することで、これを実行します。

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"}

## 解説

CAC 構成内の各地域から他の各地域にアクセスするいくつかの方法が必要です。地域のリンクが地域間の接続に対する帯域幅制限を設定し、物理リンクも表す一方、ルートはある地域から別の地域へ接続が通過するリンクされたパスを決定します。このコマンドレットは、それらのルートの関連付けに関する情報を取得します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Get-CsNetworkInterRegionRoute** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterRegionRoute"}

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
<td><p>ルートを取得するときに使用する文字列。この文字列は、Identity の値と、このパラメーターに値として渡されるワイルドカード文字列との照合結果に基づいています。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>取得するネットワーク地域ルートの一意の識別子。ネットワーク地域ルートはグローバル スコープのみで作成されるため、この識別子ではスコープを指定する必要はありません。代わりに、特定のルートを識別する一意の名前の文字列が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体からではなく、中央管理ストア のローカル レプリカからネットワーク地域間ルート情報を取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

このコマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 型のオブジェクトを 1 つ以上戻します。

## 関連項目

#### その他のリソース

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)

