---
title: Get-CsNetworkConfiguration
TOCTitle: Get-CsNetworkConfiguration
ms:assetid: 08bc8eca-b244-4d5e-b089-1cc95605ba14
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398140(v=OCS.15)
ms:contentKeyID: 48271178
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC)、Enhanced 9-1-1 (E9-1-1)、およびメディア バイパスのグローバル設定を取得します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

この例では、ネットワーク構成設定を取得します。これらの設定はグローバル スコープでのみ定義されているため、1 つの項目のみ戻されます。

    Get-CsNetworkConfiguration

## 例 2-

グローバルに適用されるメディア バイパス設定のセットが 1 つのみ存在します。これらの設定は、ネットワーク構成全体の一部として格納されています。このコマンドでまず、**Get-CsNetworkConfiguration** コマンドレットを呼び出してその構成を取得し、構成の MediaBypassSettings プロパティを取得します。

    (Get-CsNetworkConfiguration).MediaBypassSettings

## 解説

ネットワーク構成オブジェクトには、メディア バイパスのすべてのグローバル設定と、その構成が有効になっているかどうかなど、Lync Server 展開内の CAC 構成全体のすべてのグローバル設定が格納されています。このコマンドレットを使用して、これらの構成と設定を取得できます。ただし、EnableBandwidthPolicyCheck と MediaBypassSettings 以外で CAC 構成設定を取得するには、オブジェクト型に固有なコマンドレットを使用することをお勧めします。たとえば、ネットワーク地域を取得するには、通常、**Get-CsNetworkConfiguration** コマンドレットを呼び出して、その構成の NetworkRegions プロパティを取得するよりも、**Get-CsNetworkRegion** コマンドレットを呼び出す方が簡単です。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Get-CsNetworkConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkConfiguration"}

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
<td><p>1 つのネットワーク構成のみ存在するため、このコマンドレットではこのパラメーターは必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>これは必ず Global にします。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア自体ではなく、中央管理ストアのローカル レプリカからネットワーク構成を取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

**Get-CsNetworkConfiguration** コマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

