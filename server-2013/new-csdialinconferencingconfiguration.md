---
title: New-CsDialInConferencingConfiguration
TOCTitle: New-CsDialInConferencingConfiguration
ms:assetid: ac0b6e22-3883-4884-aa94-18f4029c7f1e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412816(v=OCS.15)
ms:contentKeyID: 48273238
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

ダイヤルイン会議の構成設定の新しいコレクションを作成します。これらの設定では、ユーザーがダイヤルイン会議に参加したり、ダイヤルイン会議から退出したりするときの Lync Server の応答方法を決定します。特に、参加者が会議の参加時に名前を記録する必要があるかどうか、およびユーザーの通話参加時や通話終了時のシステムからの通知方法 (または、通知するかどうか) に関する情報を戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsDialInConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableNameRecording <$true | $false>] [-EntryExitAnnouncementsEnabledByDefault <$true | $false>] [-EntryExitAnnouncementsType <UseNames | ToneOnly>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドでは、Redmond サイトに適用されるダイヤルイン会議の構成設定の新しいコレクションを作成しています。さらに、オプションのパラメーター EnableNameRecording を含めて、EnableNameRecording プロパティを False に設定しています。

    New-CSDialInConferencingConfiguration -Identity site:Redmond -EnableNameRecording $False

## 例 2

例 2 では、InMemory パラメーターを使用して、ダイヤルイン会議の構成設定の新しいコレクションを作成しています。このコレクションは、最初はメモリ内にのみ存在します。これを実行するため、まず例では、**New-CSDialInConferencingConfiguration** コマンドレットと変数 $x に格納される仮想の設定コレクションを作成する InMemory パラメーターを呼び出しています (このコレクションには Identity site:Redmond が与えられることに注意してください)。仮想のコレクションを作成したら、2 行目を使用して、EnableNameRecording プロパティの値を変更しています。最後に、例の 3 行目では、**Set-CSDialInConferencingConfiguration** コマンドレットを呼び出し、$x に格納されている仮想の構成設定を Redmond サイトに適用する実際の設定のコレクションに変換しています。

    $x = New-CSDialInConferencingConfiguration -Identity site:Redmond -InMemory
    $x.EnableNameRecording = $False
    Set-CSDialInConferencingConfiguration -Instance $x

## 解説

ユーザーがダイヤルイン会議に参加したり、ダイヤルイン会議から退出したりするときに、Lync Server はさまざまな方法で応答できます。たとえば、会議に参加する前に、参加者に自分の名前を記録するように求めることができます。同様に、管理者は、ダイヤルイン参加者の会議からの退出または会議への参加時に、Lync Server による通知を行うかどうかを決定できます。

このような会議への "参加に関する動作" は、ダイヤルイン会議の構成設定を使用して管理します。これらの設定は、グローバル スコープまたはサイト スコープで構成できます (サイト スコープで構成した設定は、グローバル スコープで構成した設定より優先されます)。初めて Lync Server をインストールするとき、存在するダイヤルイン会議の構成設定はグローバル スコープでの設定だけですが、**New-CSDialInConferencingConfiguration** コマンドレットを使用することにより、サイト スコープで新しい設定を作成できます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **New-CsDialInConferencingConfiguration** コマンドレットのローカルでの実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p>XdsIdentity</p></td>
<td><p>作成するダイヤルイン会議の構成設定の ID を示します。これらの設定はサイト スコープでのみ作成できるため、次のように、&quot;site:&quot; というプレフィックスにサイトの名前を続けて指定する構文を使用します。-Identity site:Redmond。</p>
<p>ダイヤルイン会議の構成設定は、1 サイトあたり 1 セットのみ作成できることに注意してください。site:Redmond という Identity を持つ設定のコレクションが既に存在する場合、サンプルのコマンドは失敗します。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableNameRecording</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>会議に出席する前に名前を記録するようにユーザーに依頼するかどうかを指定します。True ($True) に設定すると名前の記録が必要になります。False ($False) に設定すると名前の記録を行いません。既定値は True です。</p></td>
</tr>
<tr class="even">
<td><p><em>EntryExitAnnouncementsEnabledByDefault</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>True に設定すると、参加者が会議に出席または退席するときに、毎回アナウンスが再生されます。False (既定値) に設定すると、出席および退席のアナウンスは再生されません。</p></td>
</tr>
<tr class="odd">
<td><p><em>EntryExitAnnouncementsType</em></p></td>
<td><p>省略可能</p></td>
<td><p>EntryExitAnnouncementsType</p></td>
<td><p>参加者が会議に参加または会議から退出するたびに、システムが実行するアクションを示します。有効な値は次のとおりです。</p>
<p>UseNames。参加者が会議に参加または会議から退出するたびに、その名前を通知します (たとえば、&quot;Ken Myer は会議から退席します&quot; のように通知します)。</p>
<p>ToneOnly。参加者が会議に出席または会議から退出するときにはいつでも、発信音を再生します。</p>
<p>既定値は UseNames です。アナウンスは、EntryExitAnnouncementsEnabledByDefault プロパティが True に設定されている場合にだけ、再生されることに注意してください。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>永続的な変更としてオブジェクトをコミットせずに、オブジェクト参照を作成します。このパラメーターを指定して呼び出したコマンドレットの出力を変数に割り当てる場合、オブジェクト参照のプロパティを変更し、コマンドレットに対応する Set- コマンドレットを呼び出してそれらの変更をコミットできます。</p></td>
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

なし。**New-CsDialInConferencingConfiguration** コマンドレットは、パイプ処理された入力を許可しません。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration オブジェクトの新しいインスタンスを作成します。

## 関連項目

#### その他のリソース

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

