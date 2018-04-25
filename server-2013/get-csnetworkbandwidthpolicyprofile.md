---
title: Get-CsNetworkBandwidthPolicyProfile
TOCTitle: Get-CsNetworkBandwidthPolicyProfile
ms:assetid: 31784852-0cf4-4114-bf92-5eef6f346c47
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425815(v=OCS.15)
ms:contentKeyID: 48271690
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkBandwidthPolicyProfile

 

_**トピックの最終更新日:** 2015-03-09_

1 つまたは複数のネットワーク帯域幅ポリシーのプロファイルを取得します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkBandwidthPolicyProfile [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

パラメーターを指定せずに **Get-CsNetworkBandwidthPolicyProfile** コマンドレットを呼び出して、Lync Server 展開内で定義されているすべての帯域幅ポリシーのプロファイルを取得します。

    Get-CsNetworkBandwidthPolicyProfile

## 例 2

この例では、Identity が LowBWProfile の帯域幅ポリシーのプロファイルを取得します。ID は一意である必要があるため、これによって戻されるプロファイルは多くても 1 つです。

    Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## 例 3

この例では、Filter パラメーターを使用して、ワイルドカード文字列に基づいて 1 つまたは複数のプロファイルを取得するように指定しています。文字列値として \*50MB\* を使用することは、Identity 値の一部に 50MB という文字列を含む帯域幅ポリシーのプロファイルすべてを取得しようとしていることを示しています。たとえば、このコマンドを実行すると、"50MB リンクの BW プロファイル"、"50MB オーディオ制限"、および "50MB のビデオ制限" などの ID を持つプロファイルを取得できます。

    Get-CsNetworkBandwidthPolicyProfile -Filter *50MB*

## 解説

帯域幅ポリシーは、通話受付管理 (CAC) の一部として、特定のモダリティの帯域幅制限を定義する際に使用します (Lync Server では、オーディオとビデオのモダリティのみを帯域幅の制限に割り当てることができます)。このコマンドレットは、これらのポリシーの 1 つまたは複数のコンテナー プロファイルを取得します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Get-CsNetworkBandwidthPolicyProfile** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Identity 値がワイルドカード パターンと一致する帯域幅ポリシーのプロファイルを取得するために使用する、ワイルドカードを含む文字列。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>取得する帯域幅ポリシー プロファイルを一意に識別する文字列値。Identity を指定すると、取得されるプロファイルは多くても 1 つになります。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体からではなく、中央管理ストア のローカル レプリカからネットワーク帯域幅ポリシーのプロファイルを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 型のオブジェクトを戻します。

## 関連項目

#### その他のリソース

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

