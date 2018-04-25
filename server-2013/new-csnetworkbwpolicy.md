---
title: New-CsNetworkBWPolicy
TOCTitle: New-CsNetworkBWPolicy
ms:assetid: bbc91bd1-453c-4ae6-bb77-3b6be9429ed0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412916(v=OCS.15)
ms:contentKeyID: 48273400
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWPolicy

 

_**トピックの最終更新日:** 2015-03-09_

帯域幅ポリシー プロファイルに適用できる帯域幅ポリシーをメモリ内に作成します。Lync Server では、このポリシーは音声またはビデオのどちらかの帯域幅に適用されます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsNetworkBWPolicy -BWLimit <UInt32> -BWPolicyModality <Audio | Video> -BWSessionLimit <UInt32>

## 例

## 例 1

この例では、新しい帯域幅ポリシーが作成され、それが変数 $bwp に代入されます。**New-CsNetworkBWPolicy** コマンドレットのすべてのパラメーターは、必須です。この例では、帯域幅の合計制限 (BWLimit) を 2000 Kbps に、帯域幅のセッション制限 (BWSessionLimit) を 300 Kbps に指定し、これらの制限をビデオ セッション (BWPolicyModality ビデオ) に適用しています。

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video

## 例 2

例 2 は、新しい帯域幅ポリシーをポリシー プロファイルに割り当てることで、例 1 を拡張しています。1 行目のコマンドは例 1 と同じです。ここでは、ビデオの帯域幅制限を作成しています。次に 2 行目では **New-CsNetworkBandwidthPolicyProfile** コマンドレットを呼び出し、ポリシーを新しいプロファイルに追加しています。新しいプロファイルには LowBWLimit という Identity が付与されています。次に、BWPolicy パラメーターに値 $bwp を指定して使用します。$bmp は、1 行目で作成したばかりの新しい帯域幅ポリシーを代入した変数です。

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video
    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bwp

## 解説

このコマンドレットは、新しい帯域幅ポリシーを作成します。帯域幅ポリシーは、特定のモダリティの帯域幅の制限を定義するのに使用されます (Lync Server では、オーディオとビデオのモダリティのみを帯域幅の制限に割り当てることができます)。帯域幅ポリシーはメモリ内にのみ作成されるため、出力を変数に代入してから **New-CsNetworkBandwidthPolicyProfile** コマンドレットまたは **Set-CsNetworkBandwidthPolicyProfile** コマンドレットの BWPolicy パラメーターに値として渡す必要があります。帯域幅ポリシーはポリシー プロファイルに適用されますが、ポリシー プロファイルでは 1 つのプロファイルに対して複数のポリシーを格納できます。また、これは、通話受付管理 (CAC) 用のグローバル ネットワーク構成に含まれます。

音声ポリシーまたはビデオ ポリシーを割り当てるための推奨される方法は、**New-CsNetworkBandwidthPolicyProfile** コマンドレットまたは **Set-CsNetworkBandwidthPolicyProfile** コマンドレットを呼び出し、AudioBWLimit、AudioBWSessionLimit、VideoBWLimit、および VideoBWSessionLimit の各パラメーターの値を指定して、これらのポリシーを帯域幅ポリシー プロファイルに直接割り当てる方法であることに注意してください。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **New-CsNetworkBWPolicy** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWPolicy"}

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
<td><p><em>BWLimit</em></p></td>
<td><p>必須</p></td>
<td><p>System.UInt32</p></td>
<td><p>BWPolicyModality パラメーターで指定した型のすべての同時セッションの、帯域幅の最大合計 (Kbps)。</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
<td><p>制限する帯域幅の型を決定します。</p>
<p>有効な値は次のとおりです。Audio、Video</p></td>
</tr>
<tr class="odd">
<td><p><em>BWSessionLimit</em></p></td>
<td><p>必須</p></td>
<td><p>System.UInt32</p></td>
<td><p>BWPolicyModality パラメーターで指定した型のすべての単一セッションの、帯域幅の最大合計 (Kbps)。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType 型のオブジェクトを作成します。

## 関連項目

#### その他のリソース

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

