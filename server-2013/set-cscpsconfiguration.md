---
title: Set-CsCpsConfiguration
TOCTitle: Set-CsCpsConfiguration
ms:assetid: 9c2c0ad1-12f8-47b6-a7ec-60d91c9685bf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412721(v=OCS.15)
ms:contentKeyID: 48273020
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCpsConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

既存の Call Park Service 設定のコレクションを変更します。コール パークは、ユーザーが着信通話を保留 (パーク) できるようにするサービスです。通話をパークすると、指定された範囲 (オービット) の番号に通話を転送し、次にその通話を直ちに保留にします。正しい番号を入力するだけで、だれでも (最初に電話に出た人以外も)、どの電話からでも通話を再開できます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCpsConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CallPickupTimeoutThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnableMusicOnHold <$true | $false>] [-Force <SwitchParameter>] [-MaxCallPickupAttempts <Int32>] [-OnTimeoutURI <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドは、Identity が site:Redmond1 の Call Park Service 構成を変更し、パークされた通話による応答電話へのかけ直し回数の上限を 2 に設定します。これを行うため、MaxCallPickupAttempts パラメーターを指定し、パラメーター値を 2 に指定しています。

    Set-CsCpsConfiguration -Identity site:Redmond1 -MaxCallPickupAttempts 2

## 例 2

例 2 は、例 1 で示したコマンドの変化形です。ただし、この例では、(1 つだけではなく) すべての Call Park Service 構成の MaxCallPickupAttempts プロパティの値が 2 になるように設定します。これを行うため、**Get-CsCpsConfiguration** コマンドレットを使用して、組織内で使用されているすべての Call Park Service 設定のコレクションを取得します。次に、このコレクションは **Set-CsCpsConfiguration** コマンドレットにパイプ処理され、これにより、コレクションの個々の項目が取り込まれ、MaxCallPickupAttempts プロパティの値が 2 に設定されます。

    Get-CsCpsConfiguration | Set-CsCpsConfiguration -MaxCallPickupAttempts 2

## 例 3

この例では、サイト Redmond1 のコール パークの構成を変更し、パークされた通話によるかけ直しまでの経過時間 (CallPickupTimeoutThreshold プロパティに格納されています) を 45 秒に設定します。

    Set-CsCpsConfiguration -Identity site:Redmond1 -CallPickupTimeoutThreshold 00:00:45

## 解説

このコマンドレットは、既存の Call Park Service 構成を変更する場合に使用します。Call Park Service 構成は、パークされた通話の処理方法を指定します。たとえば、パークされた通話がしばらくの間応答されない場合は、管理者や応答グループなど、別の人に自動的に転送されます。通話は、応答忘れを防ぐために、一定の時間が経過した後にかけ直すように構成することができます。また、通話がパークされている間、発信者に対して保留音が再生されるように Call Park Service を構成することもできます。

このコマンドレットを実行できるユーザー: 既定では、**Set-CsCpsConfiguration** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCpsConfiguration"}

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
<td><p><em>CallPickupTimeoutThreshold</em></p></td>
<td><p>省略可能</p></td>
<td><p>TimeSpan</p></td>
<td><p>通話がパークされてから、呼び出しに応答した電話にかけ直されるまでの経過時間です。</p>
<p>hh:mm:ss (hh = 時間、mm = 分、ss = 秒) の形式で入力する必要があります。</p>
<p>最小値: 10 秒 (00:00:10)、最大値: 10 分 (00:10:00)</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMusicOnHold</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>通話がパークされている間、発信者に対してメロディを再生するかどうかを決定します。</p>
<p>Lync Server には、既定の保留音ファイルが付属しています。<strong>Set-CsCallParkServiceMusicOnHoldFile</strong> コマンドレットを使用すると、このファイルを変更できます (その結果、パークされている間に発信者に対して再生されるメロディも変更されます)。</p></td>
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
<td><p>変更する構成の一意の識別子です。ID により、構成の適用範囲を指定します。グローバルまたは特定のサイト (site:&lt;サイト名&gt; の形式。site:Redmond など) のどちらかを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>CallParkServiceSettings</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 型の Call Park Service 構成オブジェクトへのオブジェクト参照です。このオブジェクトは、<strong>Get-CsCpsConfiguration</strong> コマンドレットを呼び出すことで取得できます。その後、オブジェクトを変更してから、このパラメーターの <strong>Set-CsCpsConfiguration</strong> コマンドレットに渡すと、変更を保存できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxCallPickupAttempts</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>パークされた通話が、かけ直しをやめて、代替 Uniform Resource Identifier (URI) に転送されるまでに、応答した電話にかけ直す回数です。代替 URI は、OnTimeoutURI パラメーターで設定します。</p>
<p>最小値: 1、最大値: 10。</p></td>
</tr>
<tr class="even">
<td><p><em>OnTimeoutURI</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>パークされた通話が応答されなかった場合のルーティング先のユーザーまたは応答グループの SIP アドレスです。MaxCallPickupAttempts パラメーターで定義された回数のリングバックが実行された後で、パークされた通話はルーティングされます。このパラメーターが Null に設定されている場合、OnTimeoutURI は無視され、パークされた通話はリングバックの試行に失敗した後で切断されます。</p>
<p>値は、文字列 sip: で始まる SIP URI にする必要があります。たとえば、sip:rgs1@litwareinc.com のようにします。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings オブジェクトです。Call Park Service 構成オブジェクトのパイプ処理による入力を受け入れます。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

