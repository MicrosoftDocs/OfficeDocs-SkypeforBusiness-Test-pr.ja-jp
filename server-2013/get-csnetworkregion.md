---
title: Get-CsNetworkRegion
TOCTitle: Get-CsNetworkRegion
ms:assetid: 5c9eef10-16c1-45f7-ae7b-2bee0965b421
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398406(v=OCS.15)
ms:contentKeyID: 48272241
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegion

 

_**トピックの最終更新日:** 2015-03-09_

1 つ以上のネットワーク地域を取得します。ネットワーク地域は、エンタープライズ ネットワークにおけるネットワーク ハブまたはバックボーンを表します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegion [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 では、組織で定義されているすべてのネットワーク地域を取得しています。

    Get-CsNetworkRegion

## 例 2

例 2 では、NorthAmerica という ID を持つネットワーク地域を取得しています。ID は一意であるため、このコマンドが取得するのは、多くても 1 つのネットワーク地域です。

    Get-CsNetworkRegion -Identity NorthAmerica

## 例 3

この例では、"America" という文字列で終わる ID を持つすべてのネットワーク地域を取得しています。この結果、NorthAmerica、SouthAmerica、CentralAmerica などの ID を持つ地域が取得されます。

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## 例 4

この例では、セントラル サイト Redmond と関連付けられたすべてのネットワーク地域を取得しています。このコマンドではまず、パラメーターを指定せずに **Get-CsNetworkRegion** コマンドレットを呼び出して、Lync Server 展開用に定義されたすべてのネットワーク地域のコレクションを取得します。次にこのコレクションを、**Where-Object** コマンドレットにパイプ処理します。**Where-Object** コマンドレットは、このコレクションをフィルター処理して、CentralSite 値が site:Redmond と等しい (-eq) 項目 (ネットワーク地域) のみを戻します。

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## 解説

ネットワーク地域により、複数の地理的領域にわたって、ネットワークのさまざまな部分を相互接続します。すべてのネットワーク地域は、セントラル サイトと関連付ける必要があります。1 つ以上のネットワーク地域に関する情報を取得するには、このコマンドレットを使用します。取得する情報には、オーディオおよびビデオの接続で代替パスを許可するかどうかを決定したり、地域内のサイトをメディア バイパス構成と関連付けたりする、関連付けられたセントラル サイトおよび設定などがあります。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Get-CsNetworkRegion** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegion"}

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
<td><p>このパラメーターを使用すると、組織で構成されているすべてのネットワーク地域の ID に対してワイルドカード検索を実行できます。ID の任意の部分をフィルターするには、ワイルドカード文字を使用します。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>取得するネットワーク地域の一意の識別子です。Identity は、地域を一意に識別する文字列の形式です (ID は NetworkRegionID と同じであることに注意してください)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア自体からではなく、中央管理ストアのローカル レプリカから、ネットワーク地域情報を取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 型の 1 つ以上のオブジェクトを戻します。

## 関連項目

#### その他のリソース

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

