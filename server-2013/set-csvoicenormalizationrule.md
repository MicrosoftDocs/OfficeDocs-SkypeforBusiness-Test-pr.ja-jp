---
title: Set-CsVoiceNormalizationRule
TOCTitle: Set-CsVoiceNormalizationRule
ms:assetid: 68850abb-4ac7-4ae1-bb6e-d991385f92a4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398491(v=OCS.15)
ms:contentKeyID: 48272347
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceNormalizationRule

 

_**トピックの最終更新日:** 2015-03-09_

音声正規化ルールを変更します。音声正規化ルールは、電話のダイヤル要件 (外線接続の際に 9 をダイヤルするなど) を Lync Server で使用されている E.164 の電話番号形式に変換するために使用します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceNormalizationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-IsInternalExtension <$true | $false>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、サイト Redmond のプレフィックス Redmond というルールに、"サイト Redmond のすべての番号にプレフィックスを追加する" という説明を設定しています。

    Set-CsVoiceNormalizationRule -Identity "site:Redmond/Prefix Redmond" -Description "Add a prefix to all numbers on site Redmond"

## 例 2

この例では、Identity が global/SeattleFourDigit になっている音声正規化ルールを変更します。ルールに対する変更を反映した新しい説明が指定されています。また、変換のルールを変更する変換値が指定されています。これにより、このルールの既存パターンと一致する番号が、同じ番号にプレフィックス +1206556 を付けたものに変換されます。たとえば、既存パターンが任意の 4 桁の番号であり、番号を 1234 と入力した場合、この内線番号は +12065561234 という番号に変換されます。

    Set-CsVoiceNormalizationRule -Identity global/SeattleFourDigit -Description "Translate an internal four-digit extension" -Translation '+1206556$1'

## 例 3

例 3 では、正規化ルールの名前を変更しています。名前を変更すると、Identity の名前部分も変更される点に留意してください。**Set-CsVoiceNormalizationRule** コマンドレットには Name パラメーターがないため、名前を変更するには、まず **Get-CsVoiceNormalizationRule** コマンドレットを呼び出して global/RedmondFourDigit という Identity を持つルールを取得し、戻されたオブジェクトを変数 $a に割り当てます。次に、RedmondRule という文字列をオブジェクトの Name プロパティに割り当てます。その後、この変数を **Set-CsVoiceNormalizationRule** コマンドレットの Instance パラメーターに渡して変更を確定します。

    $a = Get-CsVoiceNormalizationRule -Identity global/RedmondFourDigit
    $a.name = "RedmondRule"
    Set-CsVoiceNormalizationRule -Instance $a

## 解説

このコマンドレットを実行すると、指定の音声正規化ルールが変更されます。これらのルールは、電話の認証および呼び出しルーティングの必要部分です。これらのルールによって、番号を Lync Server の内部形式から標準 (E.164) 形式に変換する際の要件を定義します。変換する番号パターンを定義する際には、正規表現を理解していると便利です。

このコマンドレットを使用して変更したルールはダイヤル プランの一部となります。このルールには、**Get-CsVoiceNormalizationRule** コマンドレット経由のほか、**Get-CsDialPlan** コマンドレットを呼び出すことで戻される NormalizationRules プロパティ経由でもアクセスできます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsVoiceNormalizationRule** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceNormalizationRule"}

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
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>正規化ルールのわかりやすい説明です。</p>
<p>最長文字列:512 文字</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>ルールの一意の識別子です。指定した Identity には、site:Redmond/Rule1 のように、後ろのスラッシュの後に名前が付いているスコープが含まれている必要があります。ここでは、site:Redmond がスコープで Rule1 が名前です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>NormalizationRule</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。 このオブジェクトは、NormalizationRule 型にする必要があり、<strong>Get-CsVoiceNormalizationRule</strong> コマンドレットを呼び出して取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>IsInternalExtension</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True に設定されていると、このルールは社内の番号に適用されます。False に設定されていると、ルールは外線番号に適用されます。関連付けられているダイヤル プランの OptimizeDeviceDialing プロパティが False に設定されている場合、この値は無視されます。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Pattern</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>このルールを適用するダイヤル番号が一致する必要のある正規表現です。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Int32</p></td>
<td><p>ルールの適用順序です。番号が複数のルールと一致する場合があります。このパラメーターによって、番号に対してルールをテストする順序を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Translation</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>番号を E.164 形式に変換するために適用する正規表現のパターンです。</p>
<p></p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule オブジェクト。**Set-CsVoiceNormalizationRule** コマンドレットは、パイプライン処理された音声正規化ルール オブジェクトの入力を受け入れます。

## 戻り値の種類

**Set-CsVoiceNormalizationRule** コマンドレットを実行しても値やオブジェクトが戻されることはありません。代わりに、このコマンドレットは、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule オブジェクトのインスタンスを構成します。

## 関連項目

#### その他のリソース

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

