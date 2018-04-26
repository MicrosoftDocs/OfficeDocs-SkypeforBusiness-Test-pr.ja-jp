---
title: Set-CsNetworkRegion
TOCTitle: Set-CsNetworkRegion
ms:assetid: ffa1774b-ac60-4392-ad55-07bb887bf945
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg413089(v=OCS.15)
ms:contentKeyID: 48274216
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegion

 

_**トピックの最終更新日:** 2015-03-09_

既存のネットワーク地域を変更します。ネットワーク地域は、エンタープライズ ネットワークのうち、ネットワーク ハブまたはバックボーンを表します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegion [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioAlternatePath <$true | $false>] [-BWAlternatePaths <PSListModifier>] [-BypassID <String>] [-CentralSite <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoAlternatePath <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、NorthAmerica というネットワーク地域を変更します。Description パラメーターに、"North American Region" という値を指定します。NorthAmerica 地域に対する Description が存在している場合は、このコマンドを実行すると、この値によって上書きされます。まだ Description の値が設定されていなかった場合は、このコマンドを実行すると、値が設定されます。

    Set-CsNetworkRegion -Identity NorthAmerica -Description "North American Region"

## 例 2

この例では、EMEA というネットワーク地域を変更し、新しいビデオ代替パス設定を割り当てます。これを実行するために **Set-CsNetworkRegion** コマンドレットを呼び出し、EMEA という Identity を渡します。次に、VideoAlternatePath パラメーターを指定し、$False という値を渡します。VideoAlternatePath を False に設定すると、適切な帯域幅が使用できない場合に、ビデオ通話が代替パスにルーティングされず、代わりに、ビデオ通話が確立されません。

    Set-CsNetworkRegion -Identity EMEA -VideoAlternatePath $False

## 例 3

例 3 では、NorthAmerica 地域に対して設定されたのと同じ代替パス設定のセットを Asia ネットワーク地域に割り当てます。この例の最初の行では、NorthAmerica ネットワーク地域のインスタンスを取得し、変数 $a に割り当てます。2 番目の行では最初に (変数 $a に保存されている) NorthAmerica 地域の BWAlternatePaths プロパティの内容を取得します。つまり、$a.BWAlternatePaths です。これは、NorthAmerica 地域におけるすべての代替パス設定から成るコレクションです。

次に、設定から成るコレクションを foreach 関数にパイプ処理します。foreach では、コレクション内の項目を一度に 1 つずつサイクル処理し、続く中かっこ内のアクションを実行します。この例のアクションは、Asia という Identity に対して **Set-CsNetworkRegion** コマンドレットを呼び出し、Asia 地域のプロパティを設定することです。次のパラメーターは BWAlternatePaths です。@{add=$\_} という値をこのパラメーターに渡します。変数 $\_ は、コレクション内にある現在の項目を表します。この例では、現在の代替パスです。値のうち @{add=} という部分は、この項目を、Asia 地域の BWAlternatePath から成るコレクションに追加することを意味します。

    $a = Get-CsNetworkRegion -Identity NorthAmerica
    $a.BWAlternatePaths | foreach {Set-CsNetworkRegion -Identity Asia -BWAlternatePaths @{add=$_}}

## 解説

ネットワーク地域は、複数の地理的な領域にまたがるネットワークのさまざまな部分を相互接続します。各ネットワーク地域は、1 つの セントラル サイト に関連付ける必要が必要があります。このセントラル サイトは、通話受付管理 (CAC) 帯域幅ポリシー サービスが実行されているデータ センター サイトです。オーディオおよびビデオの接続に対して代替パスを許可するか、メディア バイパス構成を持つ地域の中でサイトを関連付けるかなどの設定を含め、既存のネットワーク地域を変更するには、このコマンドレットを使用します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Set-CsNetworkRegion** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegion\\b"}

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
<td><p><em>AudioAlternatePath</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターでは、プライマリ パスの中に適切な帯域幅が存在しない場合に音声通話を代替パスにルーティングするかどうかを決定します。</p>
<p>このパラメーターは、BWAlternatePaths プロパティを設定します。このパラメーターに対して指定した値は、BWPolicyModality の値が Audio になっている代替パス要素のうち、AlternatePath プロパティの中に格納されます。</p>
<p>このパラメーターに値を指定すると、BWAlternatePaths パラメーターには値を指定できません。</p>
<p>いずれかの通話をインターネット通話にする場合は、帯域幅設定に関係なく、この値を True にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>BWAlternatePaths</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>優先パス経由のメディア要求を完了できない (たとえば、そのパスの上限を超えた状況) 場合に代替接続パスを許可するかどうかの情報を含むオブジェクトから成る一覧です。代替パス オブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType 型であることが必要です。この型のオブジェクトは、<strong>New-CsNetworkBWAlternatePath</strong> コマンドレットを呼び出すと作成できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>BypassID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>グローバル一意識別子 (GUID)。この GUID を使用して、CAC または Enhanced 9-1-1 (E9-1-1) のネットワーク構成内で、ネットワーク地域をメディア バイパス設定にマッピングできます (<strong>New-CsNetworkMediaBypassConfiguration</strong> コマンドレットを呼び出すときに、この BypassID の値を使用します)。</p>
<p>(<strong>New-CsNetworkRegion</strong> コマンドレットを呼び出して) 地域を作成するときに、このパラメーターを自動的に生成できます。この値を変更することはお勧めしません。どうしても値を指定する場合は、GUID の形式にする必要があります (たとえば、3b24a047-dce6-48b2-9f20-9fbff17ed62a)。この値を手動で設定するかどうかを確認するために、確認プロンプトが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>CentralSite</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>帯域幅ポリシー サービスを実行している セントラル サイト です。CAC を使用するには、このサービスを有効にする必要があります。このサービスは、フロント エンド サーバー または Standard Edition サーバー で実行されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>地域を識別する文字列です。このパラメーターを使用して、Identity 単体による説明より詳細に、地域の目的に関する説明を明示できます。</p></td>
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
<td><p>変更するネットワーク地域の一意の識別子です。Identity は、地域を一意に識別する文字列の形式です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSObject</p></td>
<td><p>ネットワークオブジェクトへの参照です。このオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 型であることが必要です。<strong>Get-CsNetworkRegion</strong> コマンドレットを呼び出すと取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoAlternatePath</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターでは、プライマリ パスの中に適切な帯域幅が存在しない場合にビデオ通話を代替パスにルーティングするかどうかを決定します。</p>
<p>このパラメーターは、BWAlternatePaths プロパティを設定します。このパラメーターに対して指定した値は、BWPolicyModality の値が Video になっている代替パス要素のうち、AlternatePath プロパティの中に格納されます。</p>
<p>このパラメーターに値を指定すると、BWAlternatePaths パラメーターには値を指定できません。</p>
<p>いずれかの通話をインターネット通話にする場合は、帯域幅設定に関係なく、この値を True にする必要があります。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType オブジェクト。ネットワーク地域オブジェクトのパイプライン入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[New-CsNetworkBWAlternatePath](new-csnetworkbwalternatepath.md)

