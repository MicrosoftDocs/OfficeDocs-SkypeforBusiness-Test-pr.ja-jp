---
title: Set-CsNetworkInterRegionRoute
TOCTitle: Set-CsNetworkInterRegionRoute
ms:assetid: 5d9da3c0-56fc-401d-baf3-ed6c0f50f53d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398410(v=OCS.15)
ms:contentKeyID: 48272217
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterRegionRoute

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 構成内のネットワーク地域を接続する既存のルートを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterRegionRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-NetworkRegionLinkIDs <String>] [-NetworkRegionLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、ルート NA\_APAC\_Route を変更しています。変更は、接続が通過するこのルート上の地域のリンクを変更することにより行います。値 "NA\_SA,SA\_APAC" を指定して NetworkRegionLinkIDs パラメーターを使用し、この文字列に指定した 2 つの ID で既存のリンクをすべて置き換えます。

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## 例 2

例 1 と同様、例 2 では、NA\_APAC\_Route ルート内のリンクを変更しています。ただし、この例では、NetworkRegionLinkIDs パラメーターを使用してそのルートのすべてのリンクを置き換えるのではなく、NetworkRegionLinks パラメーターを使用して、そのルート上に既に存在するリンクのリストへのリンクを追加しています。この場合は、リンク SA\_EMEA がルートに追加されます。構文 @{add=\<リンク\>} により、リンクのリストに要素を追加します。また、構文 @{replace=\<リンク\>} を使用して、既存のリンクを \<リンク\> によって指定されたリンクですべて置き換えたり (この動作は、NetworkRegionLinkIDs を使用した場合と本質的に同じです)、または構文 @{remove=\<リンク\>} を使用してリストからリンクを削除したりすることもできます。

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinks @{add="SA_EMEA"}

## 例 3

例 3 では、NA\_Route5 という名前のルートを変更しています。この例では、このルートを構成する地域の 1 つを変更します。NetworkRegionID2 パラメーターを使用して新しい地域を指定し、次に NetworkRegionLinkIDs パラメーターを使用して、このルートの地域を接続するリンクの新しいリストを作成します。

    Set-CsNetworkInterRegionRoute -Identity NA_Route5 -NetworkRegionID2 SouthAmerica -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## 解説

CAC 構成内の各地域から他の各地域にアクセスするいくつかの方法が必要です。地域のリンクが地域間の接続に対する帯域幅制限を設定し、物理リンクも表す一方、ルートはある地域から別の地域へ接続が通過するリンクされたパスを決定します。このコマンドレットは、そのようなルートの関連付けを変更します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsNetworkInterRegionRoute** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterRegionRoute"}

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
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>変更するネットワーク地域のルートを表す一意の識別子です。ネットワーク地域ルートはグローバル スコープのみで作成されるため、この識別子ではスコープを指定する必要はありません。代わりに、そのルートを識別する一意の名前の文字列が含まれます。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>InterNetworkRegionRouteType</p></td>
<td><p>既存の地域のルートへのオブジェクト参照です。このオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 型である必要があります。このオブジェクトは、<strong>Get-CsNetworkInterRegionRoute</strong> コマンドレットを呼び出すことにより取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このルートを介して接続された 2 つの地域のいずれかの Identity (NetworkRegionID) です。このパラメーターに渡された値は NetworkRegionID2 パラメーターの値とは異なる地域である必要があります (つまり、地域をそれ自体にルーティングすることはできません)。また、NetworkRegionID1 と NetworkRegionID2 の組み合わせは一意である必要があります (たとえば、NorthAmerica と EMEA を接続するよう定義されたルートを 2 つ持つことはできません)。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このルートを介して接続された 2 つの地域のいずれかの Identity (NetworkRegionID) です。このパラメーターに渡された値は NetworkRegionID1 パラメーターの値とは異なる地域である必要があります (つまり、地域をそれ自体にルーティングすることはできません)。また、NetworkRegionID1 と NetworkRegionID2 の組み合わせは一意である必要があります (たとえば、NorthAmerica と EMEA を接続するよう定義されたルートを 2 つ持つことはできません)。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionLinkIDs</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このルートに対するすべてのリンクをコンマ区切り値の文字列で指定することができます。値は地域リンクの Identity (NetworkRegionLinkIDs) です。‎NetworkRegionLinkIDs と NetworkRegionLinks の両方に値を入力すると、NetworkRegionLinkIDs は無視されます。このパラメーターを使用して変更したいずれのリンクも、ルートの既存のリンクをすべて置き換えます。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>このルートに適用する地域リンクの Identity (NetworkRegionLinkIDs) を含むオブジェクトのリストです。このコマンドレットでは、このパラメーターは NetworkRegionLinkIDs とは機能が異なります。異なるのは、このルートの既存のリンクをすべて置き換えることができるのに加え、個々のリンクを追加または削除することもできるという点です。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType オブジェクトです。ネットワーク地域間ルート オブジェクトのパイプ処理による入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。このコマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

