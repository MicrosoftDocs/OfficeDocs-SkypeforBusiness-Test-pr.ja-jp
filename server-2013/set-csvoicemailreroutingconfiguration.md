---
title: Set-CsVoicemailReroutingConfiguration
TOCTitle: Set-CsVoicemailReroutingConfiguration
ms:assetid: c16a0d47-318b-46e4-991c-e4842403dbe3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412948(v=OCS.15)
ms:contentKeyID: 48273484
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicemailReroutingConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

公衆交換電話網 (PSTN) の電話番号に対して Exchange UM サブスクライバー アクセス機能および自動応答機能へのアクセスを許可する設定を変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicemailReroutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutoAttendantNumber <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-SubscriberAccessNumber <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例を実行すると、Redmond1 というサイトのボイス メール再ルーティング構成設定が有効化されます。

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -Enabled $True

## 例 2

この例を実行すると、Redmond1 というサイトに適用されるボイス メール再ルーティング設定が変更され、サブスクライバー アクセスの電話番号に +14255551213 が設定されます。

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -SubscriberAccessNumber "+14255551213"

## 解説

このコマンドレットを使用すると、Exchange UM サーバーへの IP 接続切断時の自動応答およびサブスクライバー アクセス通話の再ルーティング先を決定する設定を変更できます。

自動応答およびサブスクライバー アクセスは、Exchange UM の機能です。自動応答機能では、外部の発信者が会社の電話システム内を進んで目的の部門や従業員に到達できるように音声認識とタッチトーン制御 (デュアルトーン多重周波数、または DTMF) を行ったり、留守番電話モードでユーザーのメッセージを録音したりすることができます (留守番電話モードの音声再ルーティングを推奨します)。サブスクライバー アクセスでは、内部のユーザーが電話から Microsoft Outlook のメールボックスにアクセスできます。発信者はこれらの設定で提供された番号を使用して、エンタープライズ VoIP ユーザーにボイス メール メッセージを残すことができます (AutoAttendantNumber 設定)。また、これらのユーザーは、リモート サイトの Lync Server 展開からデータ センター内の Exchange UM に IP 接続できない場合でも、ボイス メールを取得できます (SubscriberAccessNumber 設定)。

これらの設定は、Enabled プロパティが True に設定されていないと、有効にならないことに注意してください。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Set-CsVoicemailReroutingConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられている RBAC のすべての役割 (自分で作成したカスタムの RBAC 役割を含む) の一覧を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicemailReroutingConfiguration"}

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
<td><p><em>AutoAttendantNumber</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>ボイス メール デポジット試行の再ルーティング先の、自動応答の電話番号。</p>
<p>このパラメーターに入力する番号は、既存の連絡先オブジェクトの LineUri である必要があります。</p>
<p>値は、1 から 9 の 1 桁の数字で始まる必要があり、必要に応じて先行するプラス記号 (+) の後に任意の桁数の数字を続けます。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>IP 接続切断時に PSTN を介して再ルーティングされるボイス メールへのアクセスを試行するかどうかを指定します。</p></td>
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
<td><p>変更する構成の一意の識別子です。このコマンドレットでは、ID を Global または Site:&lt;サイト名&gt;とします。&lt;サイト名&gt;は、設定を適用するサイトの名前です。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>VoicemailReroutingConfiguration</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。</p>
<p>このオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 型である必要があります (<strong>Get-CsVoicemailReroutingConfiguration</strong> コマンドレットを呼び出すと取得できます)。</p></td>
</tr>
<tr class="odd">
<td><p><em>SubscriberAccessNumber</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>ボイスメールを取得しようとして再ルーティングされるサブスクライバー アクセス番号。</p>
<p>このパラメーターに入力する番号は、既存の連絡先オブジェクトの LineUri である必要があります。</p>
<p>値は、1 から 9 の 1 桁の数字で始まる必要があり、必要に応じて先行するプラス記号 (+) の後に任意の桁数の数字を続けます。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration オブジェクト。ボイス メールの再ルーティング構成オブジェクトのパイプライン入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

