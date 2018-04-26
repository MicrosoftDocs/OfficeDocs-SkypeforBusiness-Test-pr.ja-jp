---
title: Set-CsNetworkBandwidthPolicyProfile
TOCTitle: Set-CsNetworkBandwidthPolicyProfile
ms:assetid: 519916b9-d5a0-476e-a516-9b8a3058daf2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398338(v=OCS.15)
ms:contentKeyID: 48272080
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkBandwidthPolicyProfile

 

_**トピックの最終更新日:** 2015-03-09_

既存のネットワーク帯域幅ポリシーのプロファイルを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkBandwidthPolicyProfile [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、LowBWProfile という ID を持つ帯域幅ポリシーのプロファイルの説明を変更しています。変更を行うため、**Set-CsNetworkBandwidthPolicyProfile** コマンドレットを次の 2 つのパラメーターと共に呼び出します。変更するプロファイルの名前を指定する Identity、およびプロファイルの新しい説明を指定する Description。

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -Description "Policy for links of less than 10MB"

## 例 2

例 2 では、LowBWLimit という ID を持つ帯域幅ポリシーのプロファイルの、ビデオ送信の全体的な制限とセッション制限を変更しています。変更するプロファイルの ID を指定し、次に VideoBWLimit パラメーターを使用し、全体的なビデオ制限を 2500 に設定します。さらに、VideoBWSessionLimit パラメーターを使用して、個別のセッション制限を 300 に設定します。このコマンドでは、ビデオ プロファイルが追加されるか、または LowBWLimit 帯域幅ポリシーのプロファイルの、既存のビデオ プロファイルが更新されます。既存のオーディオ プロファイルは、いずれも影響を受けません。

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -VideoBWLimit 2500 -VideoBWSessionLimit 300

## 例 3

この例では、新しい帯域幅ポリシーを作成し、LowBWLimit という ID を持つ帯域幅ポリシーのプロファイルに割り当てています。この例の最初の行は、**New-CsNetworkBWPolicy** コマンドレットの呼び出しです。このコマンドレットを実行すると、新しいプロファイルが作成されます。この場合は、5000 kbps の制限 (-BWLimit 5000) と 200 kbps のセッション制限 (-BWSessionLimit 200) が設定されたビデオ プロファイル (-BWPolicyModality video) です。この新しいプロファイル オブジェクトは、変数 $bp に格納されます。この例では、次の行で **Set-CsNetworkBandwidthPolicyProfile** コマンドレットを呼び出して、プロファイル LowBWLimit (-Identity LowBWLimit) を変更しています。BWPolicy パラメーターを $bp という値と共に使用しています。これにより、このプロファイルの既存のポリシーは、新しく作成されて変数 $bp に格納されているポリシーによってすべて置き換えられます。

    $bp = New-CsNetworkBWPolicy -BWLimit 5000 -BWSessionLimit 200 -BWPolicyModality video
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bp

## 例 4

例 4 では、新しいオーディオの帯域幅ポリシーをプロファイル LowBWProfile にある既存のポリシーのセットに追加しています。1 行目では、**Get-CsNetworkBandwidthPolicyProfile** コマンドレットを呼び出して、ID が LowBWProfile のプロファイルを取得しています。そのプロファイルを変数 $a に格納します。次の行では、**New-CsNetworkBWPolicy** コマンドレットを呼び出し、新しい帯域幅ポリシーを作成しています。このポリシーは、2000 kbps の制限 (-BWLimit 2000) と 300 kbps のセッション制限 (-BWSessionLimit 300) が設定されたオーディオ ポリシー (-BWPolicyModality audio) です。この新しいポリシーは、変数 $ap に格納されます。

3 行目では、新しいオーディオ ポリシー ($ap に格納されています) を 1 行目で取得したプロファイル ($a に格納されています) に追加しています。これは、プロファイルの BWPolicy プロパティの Add メソッドを呼び出し、$ap の値を渡すことで実行されます。この行は、"$ap に格納されている新しいポリシーを、プロファイル LowBWProfile ($a に格納されています) の BWPolicy に追加する" という意味になります。

最後に、**Set-CsNetworkBandwidthPolicyProfile** コマンドレットを呼び出し、LowBWProfile プロファイルを更新します。Instance パラメーターを使用し、変更されたプロファイルを格納する $a の値を渡します。

    $a = Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile
    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    $a.BWPolicy.Add($ap)
    Set-CsNetworkBandwidthPolicyProfile -Instance $a

## 例 5

例 5 は例 4 と機能的に同じです。この例では、新しいオーディオ ポリシーをプロファイル LowBWProfile のポリシーの既存のリストに追加しています。この方法に必要な行数は少ないのですが、例 4 と比べてわかりにくい可能性があります。この方法を説明するのは、単に同じことを違う方法で行えることを示すためです。

1 行目では、新しいオーディオの帯域幅ポリシーを作成しています。帯域幅の制限 (2000) とセッション制限 (300) を設定し、変数 $ap に新しいオブジェクトを格納しています。次に、**Set-CsNetworkBandwidthPolicyProfile** コマンドレットを呼び出して、ID が LowBWProfile のプロファイルを変更します。BWPolicy パラメーターを使用して、プロファイル内のポリシーのリストを変更します。このパラメーターに渡した次の値について注意してください。@{add=$ap}。これは、Windows PowerShell でリストに何かを追加する場合に使用する簡単な方法です。最初に @ 記号を記述し、その後に波かっこ {} を続けます。波かっこの中に、リストに対して実行するアクションを指定します。この場合は、リストへの追加です (削除や置換もできます)。アクション (add) に等号を付けて、その後にリストに追加するオブジェクトを続けます。この場合は、変数 $ap に格納された新しいポリシーです。

    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -BWPolicy @{add=$ap}

## 解説

帯域幅ポリシーは、通話受付管理 (CAC) の一部として、特定のモダリティの帯域幅制限を定義する際に使用します (Lync Server では、オーディオとビデオのモダリティについてのみ帯域幅の制限を指定できます)。このコマンドレットは、これらのポリシーのコンテナー プロファイルを変更します。

重要: プロファイルに複数のポリシー (たとえば、1 つのオーディオ ポリシーと 1 つのビデオ ポリシー) が含まれている場合は、AudioBWLimit、AudioBWSessionLimit、VideoBWLimit、または VideoBWSessionLimit プロパティを使用してプロファイルを変更すると、プロファイル内の既存のポリシーはすべて削除され、新しい値で置き換えられます。プロファイルにビデオを制限するポリシーが含まれていて、AudioBWLimit パラメーターのみを設定する場合は、ビデオ ポリシーが削除されて、オーディオ ポリシーが作成されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsNetworkBandwidthPolicyProfile** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkBandwidthPolicyProfile"}

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
<td><p><em>AudioBWLimit</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>すべてのオーディオ接続に割り当てられる最大帯域幅です。1 つのオーディオ セッションでオーディオの帯域幅制限を超過するような場合は、このセッションを開始できません。</p>
<p>kbps で表されます。たとえば、値が 1000 の場合は 1000 kbps を表します。</p>
<p>このパラメーターに値を指定すると、BWPolicy パラメーターには値を指定できません。</p>
<p>既定値は次のとおりです。AudioBWSessionLimit パラメーターに値を指定しても、AudioBWLimit パラメーターに値を指定しなければ、AudioBWLimit は既定で 0 になります。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>オーディオ セッションごとに割り当てられる最大帯域幅です。kbps で表されます。この値は 40 以上である必要があります。</p>
<p>このパラメーターに値を指定すると、BWPolicy パラメーターには値を指定できません。</p>
<p>既定値は次のとおりです。AudioBWLimit パラメーターに値を指定しても、AudioBWSessionLimit パラメーターに値を指定しなければ、AudioBWSessionLimit は既定で 175 になります。</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicy</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>帯域幅ポリシーのプロファイルを含むオブジェクトのリストです。リスト内の各オブジェクトは、帯域幅モダリティ (オーディオまたはビデオ)、帯域幅制限、および帯域幅のセッション制限です。</p>
<p>このパラメーターに値を指定すると、AudioBWLimit、AudioBWSessionLimit、VideoBWLimit、または VideoBWSessionLimit パラメーターに値を指定することができません。</p>
<p>リスト内のオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType 型にする必要があります。この型のオブジェクトは、<strong>New-CsNetworkBWPolicy</strong> コマンドレットを呼び出すことによって作成することができ、作成されたポリシーは、このパラメーターに値として割り当てることによってプロファイルに追加できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>帯域幅ポリシーのプロファイルの説明です。たとえば、このパラメーターを使用してプロファイルの用途を明示することができます。</p></td>
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
<td><p>変更する帯域幅ポリシーのプロファイルを一意に識別する文字列値です。この文字列値は、プロファイルの BWPolicyProfileID プロパティと同一で、BWPolicyProfileID プロパティの値を変更することによって変更できます。これは、&quot;切り取り/貼り付け&quot; 操作と同等です。プロファイルのプロパティはすべて同じままで残され、名前だけが変更されます。ただし、プロファイルがネットワーク サイトに割り当てられている場合は、この値を変更できません。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>BWPolicyProfileType</p></td>
<td><p>帯域幅ポリシーのプロファイルのオブジェクト (Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 型のオブジェクト) への参照で、プロファイルを変更するために使用する設定が含まれます。このオブジェクトは、<strong>Get-CsNetworkBandwidthPolicyProfile</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>すべてのビデオ接続に割り当てられる最大帯域幅です。1 つのビデオ セッションでビデオの帯域幅制限を超過するような場合は、このセッションを開始できません。</p>
<p>kbps で表されます。たとえば、値が 1000 の場合は 1000 kbps を表します。</p>
<p>このパラメーターに値を指定すると、BWPolicy パラメーターには値を指定できません。</p>
<p>既定値は次のとおりです。VideoBWSessionLimit パラメーターに値を指定しても、VideoBWLimit パラメーターに値を指定しなければ、VideoBWLimit は既定で 0 になります。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>ビデオ セッションごとに割り当てられる最大帯域幅です。kbps で表されます。この値は 100 以上である必要があります。</p>
<p>このパラメーターに値を指定すると、BWPolicy パラメーターには値を指定できません。</p>
<p>既定値は次のとおりです。VideoBWLimit パラメーターに値を指定しても、VideoBWSessionLimit パラメーターに値を指定しなければ、VideoBWSessionLimit は既定で 700 になります。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType オブジェクト。パイプライン処理されたネットワーク帯域ポリシー プロファイル オブジェクトの入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。このコマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

