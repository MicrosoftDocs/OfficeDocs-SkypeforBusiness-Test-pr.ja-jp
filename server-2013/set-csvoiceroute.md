---
title: Set-CsVoiceRoute
TOCTitle: Set-CsVoiceRoute
ms:assetid: b786aec0-946e-4ce5-812e-25e5d8cfa4d5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412893(v=OCS.15)
ms:contentKeyID: 48273372
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceRoute

 

_**トピックの最終更新日:** 2015-03-09_

ボイス ルートを変更します。ボイス ルートには、エンタープライズ VoIP ユーザーからの呼び出しを公衆交換電話網 (PSTN) または構内交換機 (PBX) の電話番号へルーティングする方法についての Lync Server に対する指示が含まれます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AlternateCallerId <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-NumberPattern <String>] [-Priority <Int32>] [-PstnGatewayList <PSListModifier>] [-PstnUsages <PSListModifier>] [-SuppressCallerId <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

このコマンドにより、Route1 ボイス ルートの Description は "Test Route" に設定されます。

    Set-CsVoiceRoute -Identity Route1 -Description "Test Route"

## 例 2

この例のコマンドにより、Route1 という ID を持つボイス ルートが変更され、このボイス ルートの使用法一覧に PSTN 使用法 (市外通話) が追加されます。市外通話は、グローバル PSTN 使用法一覧に設定する必要があります (この一覧は、**Get-CsPstnUsage** コマンドレットを呼び出すと取得できます)。

    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{add="Long Distance"}

## 例 3

この例では、Route1 というボイス ルートを変更して、そのルートの PSTN 使用法の一覧を、組織の既存の使用法すべてに設定しています。この例では、1 番目のコマンドを実行してグローバル PSTN の使用法一覧を取得しています。**Get-CsPstnUsage** コマンドレットの呼び出しがかっこで囲まれていることに注意してください。これは、PSTN 使用法情報が含まれるオブジェクトを最初に取得することを示しています (グローバルの PSTN 使用法は 1 つしかないため、オブジェクトが 1 つだけ取得されます)。次に、このオブジェクトの Usage プロパティを取得しています。PSTN 使用法一覧を含んだ Usage プロパティを、変数 $x に代入しています。この例の 2 行目で、Route1 という ID を持つボイス ルートを変更するために、**Set-CsVoiceRoute** コマンドレットを呼び出しています。PstnUsages パラメーターに渡される値 @{replace=$x}。この値により、このルートの PstnUsages 一覧のすべてを $x の内容に置き換えるように指示されます。$x には、行 1 で取得した PSTN 使用法が含まれます。

    $x = (Get-CsPstnUsage).Usage
    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{replace=$x}

## 例 4

この一連のコマンドによって、Route1 の ID を持つボイス ルートの Name プロパティが RouteA に変更されます。Name プロパティを変更すると、Identity プロパティも自動的に変更され、この例では RouteA に変更されます。

最初の行で、**Get-CsVoiceRoute** コマンドレットが呼び出されて、Route1 の ID を持つボイス ルートが取得されます。戻されたオブジェクトは変数 $x に格納されます。次に、このオブジェクトの Name プロパティが、"RouteA" という文字列値に割り当てられます。最後に、オブジェクト (変数 $x に格納済み) が **Set-CsVoiceRoute** コマンドレットの Instance パラメーターに渡されて、変更が行われます。

    $x = Get-CsVoiceRoute -Identity Route1
    $x.Name = "RouteA"
    Set-CsVoiceRoute -Instance $x

## 例 5

この例では、Route1 という名前のボイス ルートが変更され、ルートの PSTN ゲートウェイ一覧 (PstnGatewayList) に PstnGateway:192.168.0.100 という Identity を持つゲートウェイのサーバーの役割が設定されます。この例の 1 行目では、**Get-CsVoiceRoute** コマンドレットを呼び出して、変更するボイス ルート (この場合は Route1) を取得しています。次に、Route1 の PstnGatewayList プロパティに対し、Add メソッドを呼び出します。追加するサービスの Identity を Add メソッドに渡しています。最後に、**Set-CsVoiceRoute** コマンドレットを呼び出して、Instance パラメーターに変数 $y を渡しています。これにより、新しく追加された PSTN ゲートウェイで、Route1 ($y に格納済み) が更新されます。

    $y = Get-CsVoiceRoute -Identity Route1
    $y.PstnGatewayList.Add("PstnGateway:192.168.0.100")
    Set-CsVoiceRoute -Instance $y

## 解説

既存のボイス ルートを変更する場合は、このコマンドレットを使用します。ボイス ルートは、公衆交換電話網 (PSTN) の使用法を介して、音声ポリシーに関連付けられます。ボイス ルートには、指定されたボイス ルートを介してルーティングされる電話番号を識別する正規表現が含まれます。正規表現に一致する電話番号が、そのルートを介してルーティングされます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsVoiceRoute** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceRoute"}

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
<td><p><em>AlternateCallerId</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>SuppressCallerId パラメーターが True に設定されていると、発信者の実際の番号ではなく AlternateCallerId パラメーターの値が受信者側に対して表示されます。この番号は有効な番号である必要があり、サポートや人事など組織内の部署を示す場合もあります。</p>
<p>SuppressCallerId パラメーターが False に設定されていると、AlternateCallerId パラメーターは無視されます。</p>
<p>この値は、正規表現 (\+)?[1-9]\d*(;ext=[1-9]\d*) に一致する必要があります。つまり、この値の頭に正符号 (+) が付く場合はありますが、必ずしも正符号が付いている必要はありません。この値は任意の数の数字で構成され、その後に内線番号を付けることができます。この内線番号は、;ext= およびその後に続く任意の数の数字で構成されます (内線番号を追加する場合、その文字列を二重引用符で囲む必要がありますので注意してください)。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>この電話ルートに関する説明です。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>ボイス ルートの一意の ID です。(Test Route など、ルート名にスペースがある場合は、全文字列をかっこで囲む必要があります。)</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>ルート</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。 このオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route 型である必要があり、<strong>Get-CsVoiceRoute</strong> コマンドレットを呼び出して取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberPattern</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>このルートの適用する電話番号を指定する正規表現です。このパターンと一致する番号が、残りのルーティング設定に従ってルーティングされます。たとえば、既定の番号パターン [0-9]{10} は、0 ～ 9 の任意の数字からなる 10 桁の番号を指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Int32</p></td>
<td><p>複数のボイス ルートを解決する番号。複数のルートが利用可能な場合、この優先度によって、適用されるルートの順序が決定されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnGatewayList</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>仲介サーバーは、複数のゲートウェイに関連付けることができます。このパラメーターには、このボイス ルートに関連付けられているゲートウェイの一覧が含まれます。この一覧の各メンバーは、PSTN ゲートウェイか仲介サーバーのサービス ID である必要があります。この値が仲介サーバーを参照できるのは、仲介サーバーが Microsoft Office Communications Server 2007 または Microsoft Office Communications Server 2007 R2 に対して構成されている場合に限ります。Lync Server の場合、PSTN ゲートウェイを使用する必要があります。サービス ID は、ServiceRole:FQDN という形式の文字列です。ServiceRole はサービス ロール名 (PSTNGateway)、FQDN はサーバーのプールまたは IP アドレスの完全修飾ドメイン名 (FQDN) です。たとえば、PSTNGateway:redmondpool.litwareinc.com です。サービス ID は、Get-CsService | Select-Object Identity コマンドを呼び出すと取得できます。</p>
<p>ボイス ルートを変更して PstnGatewayList 一覧を空のままにした場合、またはこの変更によりこの一覧からすべての項目が削除された場合、ユーザーが PSTN 通話できないという警告メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>このボイス ルートに適用できる (ローカルや市外通話などの) PSTN 使用法一覧。PSTN 使用法は、既存のものである必要があります (PSTN 使用法は <strong>Get-CsPstnUsage</strong> コマンドレットを呼び出すことで取得できます)。</p>
<p>ボイス ルートを変更して PstnUsages 一覧を空のままにした場合、またはこの変更によりすべての PSTN 使用法がこの一覧から削除された場合、ユーザーが PSTN 通話できないという警告メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>SuppressCallerId</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>発信通話で発信者 ID を表示するかどうかを決定します。このパラメーターが True に設定されていると、発信者 ID が表示されません。実際の ID の代わりに AlternateCallerId の値が表示されます。SuppressCallerId を True に設定する場合、AlternateCallerId 値を指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route オブジェクト。**Set-CsVoiceRoute** コマンドレットは、ボイス ルート オブジェクトのパイプライン処理された入力を受け入れます。

## 戻り値の種類

**Set-CsVoiceRoute** コマンドレットは、値またはオブジェクトを戻しません。代わりに、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route オブジェクトのインスタンスを構成します。

## 関連項目

#### その他のリソース

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsService](get-csservice.md)

