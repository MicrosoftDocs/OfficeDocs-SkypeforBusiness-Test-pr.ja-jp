---
title: Set-CsVoiceTestConfiguration
TOCTitle: Set-CsVoiceTestConfiguration
ms:assetid: 7b95fc95-ec0e-4bb3-aed1-e8b72e305999
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398614(v=OCS.15)
ms:contentKeyID: 48272623
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceTestConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

指定のルートおよびルールで電話番号をテストする際のテスト シナリオを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsVoiceTestConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceTestConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DialedNumber <String>] [-ExpectedRoute <String>] [-ExpectedTranslatedNumber <String>] [-ExpectedUsage <String>] [-Force <SwitchParameter>] [-TargetDialplan <String>] [-TargetVoicePolicy <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、TestConfig1 の音声テスト構成のダイヤル番号を 14255551212 に設定しています。この番号で音声ポリシーとボイス ルートをチェックし、正規化が問題なく行われていることと、正しいルートとダイヤル プランが適用されていることを確認します。

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -DialedNumber 14255551212

## 例 2

この例では、TestConfig1 という音声テスト構成の設定を変更しています。このコマンドは、TargetDialplan を site:Redmond1 のダイヤル プランに設定します。ダイヤル プランの変更によって正規化ルールが変更された可能性があるため、ExpectedTranslationNumber も変更したダイヤル プランの正規化ルールの内容を反映して変更されています。

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -TargetDialplan site:Redmond1 -ExpectedTranslatedNumber "+912065551212"

## 解説

ボイス ルートと音声ポリシーを実装する前に、複数の電話番号でテストして予想どおりに動作するかどうか確認することをお勧めします。このコマンドレットを使用してテスト シナリオを変更することで、この確認を行うことができます。

**Set-CsVoiceTestConfiguration** コマンドレットを実行すると、指定の電話番号をテストするボイス ルート、使用法、ダイヤル プラン、および音声ポリシーが変更されます。この情報はすべて、他のコマンドレットを使用して定義、取得できます。これについては、このトピックのパラメーター説明で示されています。

このコマンドレットを使用して変更した構成は、**Test-CsVoiceTestConfiguration** コマンドレットを使用してテストします。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsVoiceTestConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceTestConfiguration"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>ポリシー、使用法などのテストに使用する電話番号です。</p>
<p>512 文字以下にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedRoute</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>構成テスト中に使用されることが予想されるボイス ルートの名前です。対象のダイヤル プランと音声ポリシーに基づいて異なるルートが使用されると、テストは失敗します。<strong>Get-CsVoiceRoute</strong> コマンドレットを呼び出すことで、使用可能なボイス ルートを取得できます。</p>
<p>256 文字以下にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>ExpectedTranslatedNumber</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>変換後の表示形式の電話番号です。これは、正規化後の DialedNumber パラメーター値です。<strong>Test-CsVoiceTestConfiguration</strong> コマンドレットを実行した結果、DialedNumber が ExpectedTranslatedNumber の値にならない場合、テストは失敗とレポートされます。</p>
<p>512 文字以下にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedUsage</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>構成テスト時に使用予定の PSTN 使用法の名前です。対象のダイヤル プランと音声ポリシーに基づいて異なる PSTN 使用法が使用されると、テストは失敗します。<strong>Get-CsPstnUsage</strong> コマンドレットを呼び出すことで利用可能な使用法を取得できます。</p>
<p>256 文字以下にする必要があります。</p></td>
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
<td><p>変更するテスト シナリオを一意に識別する文字列です。</p>
<p>このパラメーターの値にはスコープは含まれません。このオブジェクトがグローバル スコープでのみ作成できるためです。したがって、名前のみが必要です。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>TestConfiguration</p></td>
<td><p>既存の音声テスト構成に変更点を加えた構成が含まれる Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 型のオブジェクトです。この型のオブジェクトは、<strong>Get-CsVoiceTestConfiguraton</strong> コマンドレットを呼び出すと取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetDialplan</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このテストで使用するダイヤル プランの Identity です。ダイヤル プランは、<strong>Get-CsDialPlan</strong> コマンドレットを呼び出すことで取得できます。</p>
<p>40 文字以下にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetVoicePolicy</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このテストを実行する対象の音声ポリシーの Identity です。音声ポリシーは、<strong>Get-CsVoicePolicy</strong> コマンドレットを呼び出すことで取得できます。</p>
<p>40 文字以下にする必要があります。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration オブジェクト。パイプライン処理された音声テスト構成オブジェクトの入力を受け入れます。

## 戻り値の種類

このコマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration 型のオブジェクトが戻されます。

## 関連項目

#### その他のリソース

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)

