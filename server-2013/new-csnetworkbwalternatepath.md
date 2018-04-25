---
title: New-CsNetworkBWAlternatePath
TOCTitle: New-CsNetworkBWAlternatePath
ms:assetid: 9017378e-4583-42bc-9572-aa8e9571cfe3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398732(v=OCS.15)
ms:contentKeyID: 48272822
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWAlternatePath

 

_**トピックの最終更新日:** 2015-03-09_

帯域幅の制限された接続のためインターネット経由でメディアが別のパスにルーティングできるかどうかを定義する新しい設定を作成します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsNetworkBWAlternatePath -AlternatePath <$true | $false> -BWPolicyModality <Audio | Video>

## 例

## 例 1

この例では、新しいネットワーク帯域幅の代替パスを作成し、その設定を新しく作成した地域に割り当てています。この例の最初の行では、**New-CsNetworkBWAlternatePath** コマンドレットを呼び出し、新しい代替パスを作成します。別のパスには 2 つのプロパティのみがあります。BWPolicyModality は、audio または video のどちらかに設定する必要があります (この例では audio を使用しています)。AlternatePath は、True または False のどちらかにする必要があります (この例では True を使用しています)。このコマンドレットからの出力である、作成したばかりの代替パス オブジェクトへの参照を、変数 $a に割り当てます。

この例の 2 行目では、新しいネットワーク地域の作成において、この新しく作成した代替パスを使用します。これを行うため、**New-CsNetworkRegion** コマンドレットを呼び出し、NorthAmerica という Identity を渡します。必須パラメーター CentralSite の値を割り当て (この例では、この地域のセントラル サイトの名前は Redmond-NA-MLS です)、次に BWAlternatePaths パラメーターを指定し、そこに先ほど作成した代替パス オブジェクトを格納している変数 ($a) を渡します。

    $a = New-CsNetworkBWAlternatePath -BWPolicyModality "audio" -AlternatePath $true
    New-CsNetworkRegion -Identity NorthAmerica -CentralSite Redmond-NA-MLS -BWAlternatePaths $a

## 解説

Lync Server の通話受付管理 (CAC) 構成内では、オーディオとビデオの 2 つのモダリティを使用できます。帯域幅の制限はどちらのモダリティにも設定できます。帯域幅の制限により通話が完了できなくなる場合に、インターネット経由の別のパスを使用して通話を確立できることがあります。このコマンドレットにより、通話がモダリティに基づきインターネット経由の別のパスにルーティングできるかどうかを定義する設定を作成できます。この設定は CAC 構成内の地域ごとに適用されます。

このコマンドレットは新しく作成された設定をすぐには保存しません。その代わりに、メモリ内に設定を作成します。これらの設定をネットワーク内の地域に適用するには、コマンドレットの出力を変数に割り当て、その変数を **New-CsNetworkRegion** コマンドレットまたは **Set-CsNetworkRegion** コマンドレットの BWAlternatePaths パラメーターに対する値として使用する必要があります。**New-CsNetworkRegion** コマンドレットおよび **Set-CsNetworkRegion** コマンドレットの AudioAlternatePath および VideoAlternatePath パラメーターを使用して、これらの設定を直接適用できます。この場合、**New-CsNetworkBWAlternatePath** コマンドレットを呼び出して新しいオブジェクトを作成する必要はありません。

このコマンドレットを実行できるユーザー: 既定では、**New-CsNetworkBWAlternatePath** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWAlternatePath"}

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
<td><p><em>AlternatePath</em></p></td>
<td><p>必須</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、BWPolicyModality パラメーター (audio または video のどちらか) で指定したモダリティのメディアで作成された通話は、主要パスに十分な帯域幅がない場合に、別のパス経由でルーティングできます。</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>必須</p></td>
<td><p>BWPolicyModality</p></td>
<td><p>別のパス設定が適用されるモダリティ。</p>
<p>有効な値は次のとおりです。audio、video</p>
<p>完全なデータ型: Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType 型のオブジェクトを作成します。

## 関連項目

#### その他のリソース

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

