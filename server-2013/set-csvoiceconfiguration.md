---
title: Set-CsVoiceConfiguration
TOCTitle: Set-CsVoiceConfiguration
ms:assetid: dbab35ac-9a55-41d2-a726-9a26b2ff8e85
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398967(v=OCS.15)
ms:contentKeyID: 48273824
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

音声テスト構成の一覧を変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsVoiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-VoiceTestConfigurations <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

音声構成内の音声テスト構成を変更するには、複数の手順を実行する必要があります。この例では、まず、**Get-CsVoiceConfiguration** コマンドレットを呼び出して、音声構成オブジェクトを取得します。取得したオブジェクト (1 つのオブジェクトのみ) を変数 $a に割り当てます。

この例の 2 行目で、変数 $a から VoiceTestConfigurations プロパティの内容を取得します。これは、音声テスト構成オブジェクトのコレクションです。次に、このコレクションを **Where-Object** コマンドレットにパイプ処理し、ここで、文字列 TestConfig2 と一致する Name を持つすべての音声テスト構成オブジェクトのコレクションを検索します。このオブジェクトを変数 $b に割り当てます。

次に、プロパティ DialedNumber および ExpectedTranslatedNumber に新しい値を割り当てることで、TestConfig2 音声テスト構成オブジェクトを変更します。このオブジェクトの更新により、変数 $a 内のオブジェクトを更新します。ただし、このオブジェクトはまだメモリ内にあります。最後の手順として、$a を **Set-CsVoiceConfiguration** コマンドレットの Instance パラメーターに渡して、これらの変更を保存する必要があります。

この方法で音声構成を変更することは推奨しません。以下に示すように、個々の音声テスト構成を **Set-CsVoiceTestConfiguration** コマンドレットで変更するだけで、音声構成を変更できます。

Set-CsVoiceTestConfiguration -Identity TestConfig2 -DialedNumber 5551212 -ExpectedTranslatedNumber +5551212

この 1 行により、例 1 に示すものと同じタスクが実行されます。

    $a = Get-CsVoiceConfiguration
    $b = $a.VoiceTestConfigurations | Where-Object {$_.Name -eq "TestConfig2"}
    $b.DialedNumber = "5551212"
    $b.ExpectedTranslatedNumber = "+5551212"
    Set-CsVoiceConfiguration -Instance $a

## 解説

音声テスト構成は、特定の音声ポリシー、ルート、およびダイヤル プランに対する電話番号のテストを行うために使用されます。このコマンドレットを使用すると、Lync Server の展開用のすべての音声テスト構成を含む一覧にある音声テスト構成を変更できます。

このコマンドレットは、VoiceConfiguration 型のオブジェクトを変更します。このオブジェクトは単純に、音声テスト構成用のコンテナー オブジェクトです。したがって、このコマンドレットの使用は推奨しません。音声構成を変更するには、**Set-CsVoiceTestConfiguration** コマンドレットを呼び出して、個々の音声テスト構成を変更します。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが **Set-CsVoiceConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsIdentity</p></td>
<td><p>このオブジェクトの範囲です。このパラメーターで唯一使用できる値は、Global です。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>VoiceConfiguration</p></td>
<td><p>音声構成 (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration) オブジェクトへの参照です。この型のオブジェクトは、<strong>Get-CsVoiceConfiguration</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceTestConfigurations</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>Lync Server の展開のために定義されているすべての音声テスト構成 (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration オブジェクト) の一覧です。</p>
<p>個々の音声テスト構成オブジェクトは、<strong>Set-CsVoiceTestConfiguration</strong> コマンドレットを使用して変更する必要があります。この一覧の構成の変更にはこの方法を推奨します。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration オブジェクト。**Set-CsVoiceConfiguration** コマンドレットは、音声構成オブジェクトのパイプ処理された入力を受け取ります。

## 戻り値の種類

**Set-CsVoiceConfiguration** コマンドレットは、値またはオブジェクトを戻しません。代わりに、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration オブジェクトのインスタンスを構成します。

## 関連項目

#### その他のリソース

[Remove-CsVoiceConfiguration](remove-csvoiceconfiguration.md)  
[Get-CsVoiceConfiguration](get-csvoiceconfiguration.md)  
[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

