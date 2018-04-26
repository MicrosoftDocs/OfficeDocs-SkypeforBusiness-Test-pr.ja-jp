---
title: Set-CsRoutingConfiguration
TOCTitle: Set-CsRoutingConfiguration
ms:assetid: ab69c6e8-262a-4ecb-b1af-513383c494fe
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412811(v=OCS.15)
ms:contentKeyID: 48273233
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRoutingConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

ボイス ルートの一覧を変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsRoutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

ルーティング構成内のボイス ルートを変更するには、複数の手順を実行する必要があります。この例では、まず、**Get-CsRoutingConfiguration** コマンドレットを呼び出して、ルーティング構成オブジェクトを取得します。取得したオブジェクト (1 つのオブジェクトのみ) を変数 $a に割り当てます。

この例の 2 行目で、変数 $a から Route プロパティの内容を取得します。これは、ボイス ルート オブジェクトのコレクションです。次に、このコレクションは **Where-Object** コマンドレットにパイプ処理され、その結果、文字列 LocalRoute に一致する名前を持つすべてのボイス ルート オブジェクトのコレクションを検索します。このオブジェクトを変数 $b に割り当てます。

次に、値 $False をプロパティ SuppressCallerId に割り当てて、LocalRoute ボイス ルート オブジェクトを変更します。このオブジェクトの更新により、変数 $a 内のオブジェクトを更新します。ただし、このオブジェクトはまだメモリ内にあります。最後の手順として、$a を **Set-CsRoutingConfiguration** コマンドレットの Instance パラメーターへ渡して、これらの変更を保存する必要があります。

この方法でルーティング構成を変更することは推奨しません。ここに示すように、個々のボイス ルートを **Set-CsVoiceRoute** コマンドレットで変更するだけで、ルーティング構成を変更できます。

Set-CsVoiceRoute -Identity LocalRoute -SuppressCallerId $False

この 1 行により、例 1 に示すタスクと同じタスクが実行されます。

    $a = Get-CsRoutingConfiguration
    $b = $a.Route | Where-Object {$_.Name -match "LocalRoute"}
    $b.SuppressCallerId = $False
    Set-CsRoutingConfiguration -Instance $a

## 解説

ボイス ルートには、エンタープライズ VoIP ユーザーからの呼び出しを公衆交換電話網 (PSTN) または構内交換機 (PBX) の電話番号へルーティングする方法についての Lync Server に対する指示が含まれます。このコマンドレットを使用すると、Lync Server 展開内で定義されたボイス ルートのすべての設定を変更できます。

このコマンドレットの使用は推奨しません。ルーティング構成を変更するには、**Set-CsVoiceRoute** コマンドレットを呼び出して、個々のボイス ルートを変更します。

このコマンドレットを実行できるユーザー: 既定では、**Set-CsRoutingConfiguration** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRoutingConfiguration"}

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
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>True に設定すると、音声ルーティングの管理において、発信ユーザーと着信ユーザーの両方のロケーションが考慮されます。既定値は False です。</p></td>
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
<td><p>XdsIdentity</p></td>
<td><p>ルーティング構成のスコープ。グローバルにする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>ルーティング構成 (Microsoft.Rtc.Management.WritablConfig.Policy.Voice.PstnRoutingSettings) オブジェクトです。この型のオブジェクトは、<strong>Get-CsRoutingConfiguration</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Route</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>Lync Server 展開用に定義されたすべてのボイス ルート (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route オブジェクト) の一覧です。</p>
<p>個々のボイス ルート オブジェクトは、<strong>Set-CsVoiceRoute</strong> コマンドレットを使用して変更する必要があります。この一覧のルートの変更には、この方法を推奨します。</p></td>
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

Microsoft.Rtc.WritableConfig.Management.Policy.Voice.PSTNRoutingSettings オブジェクトです。ルーティング構成オブジェクトのパイプ処理による入力を受け入れます。

## 戻り値の種類

**Set-CsRoutingConfiguration** コマンドレットは、値またはオブジェクトを戻しません。代わりに、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings オブジェクトのインスタンスを構成します。

## 関連項目

#### その他のリソース

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

