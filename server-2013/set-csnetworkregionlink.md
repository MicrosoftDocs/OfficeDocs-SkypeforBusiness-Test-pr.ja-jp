---
title: Set-CsNetworkRegionLink
TOCTitle: Set-CsNetworkRegionLink
ms:assetid: b3d5d203-2aa7-4a54-93d4-30bcda391d68
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412867(v=OCS.15)
ms:contentKeyID: 48273318
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegionLink

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 用に構成された 2 つのネットワーク地域間のリンクを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegionLink [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、NA\_EMEA という名前のネットワーク地域リンクの帯域幅ポリシー プロファイルを、HighBWLimits プロファイルに変更します。変更するネットワーク地域リンクの名前は、Identity パラメーターの値として指定されています。次に、HighBWLimits という値を BWPolicyProfile パラメーターに代入しています。これにより、HighBWLimits という帯域幅ポリシー プロファイルで定義されている帯域幅の制限が、これらの地域間接続に割り当てられます。

    Set-CsNetworkRegionLink -Identity NA_EMEA -BWPolicyProfileID HighBWLimits

## 解説

ネットワーク内の地域は、WAN 接続で物理的にリンクされています。このコマンドレットでは、リンクされている地域と、その地域間の音声ビデオ接続における帯域幅の制限を変更できるようにすることで、2 地域間のリンクを変更します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsNetworkRegionLink** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegionLink"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>そのリンクの制限を定義する、帯域幅のポリシー プロファイル ID。<strong>Get-CsNetworkBandwidthPolicyProfile</strong> コマンドレットを呼び出すと、利用可能なプロファイルの一覧を取得できます。</p></td>
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
<td><p>変更するネットワーク地域リンクの一意の識別子。ネットワーク地域リンクは、グローバル スコープでのみ作成されるため、この識別子にスコープを指定する必要はありません。その代わり、そのリンクを識別する一意の名前を表す文字列を含みます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>NetworkRegionLinkType</p></td>
<td><p>ネットワーク地域リンクに対するオブジェクト参照。このオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 型である必要があります。<strong>Get-CsNetworkRegionLink</strong> コマンドレットを呼び出すと取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>NetworkRegionID2 プロパティで識別される地域にリンクされている地域の ID (NetworkRegionID)。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>NetworkRegionID1 プロパティで識別される地域にリンクされている地域の ID (NetworkRegionID)。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType オブジェクト。ネットワーク地域リンク オブジェクトのパイプライン処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

