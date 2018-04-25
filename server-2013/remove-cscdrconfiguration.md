---
title: Remove-CsCdrConfiguration
TOCTitle: Remove-CsCdrConfiguration
ms:assetid: 64352746-a03c-434a-9baf-4d9cd630e9da
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398451(v=OCS.15)
ms:contentKeyID: 48272268
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCdrConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

指定された通話詳細記録 (CDR) 設定のコレクションを削除します。CDR により、ピアツーピアのインスタント メッセージング セッション、ボイス オーバー IP (VoIP) 電話での通話、および電話会議などの利用状況を追跡できます。この利用状況データには、発信者と受信者、通話時刻、および通話時間についての情報が含まれます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、**Remove-CsCdrConfiguration** コマンドレットを使用して Redmond サイトに割り当てられた CDR 設定を削除します。Identity パラメーターを使用することで、指定されたサイトに割り当てられた設定のみが削除されます。

    Remove-CsCdrConfiguration -Identity site:Redmond

## 例 2

例 2 に示すコマンドは、サイト スコープで割り当てられていたすべての CDR 設定を削除します。このタスクを実行するには、まず、コマンドで **Get-CsCdrConfiguration** コマンドレットおよび Filter パラメーターを使用して、該当する CDR 設定を取得します。文字列値 "site:\*" を使用することで、文字列 "site:" で始まる Identity を持つ設定のみが戻されます。次に、フィルター処理したコレクションは **Remove-CsCdrConfiguration** コマンドレットにパイプ処理され、コレクション内のすべての項目が削除されます。

    Get-CsCdrConfiguration -Filter site:* | Remove-CsCdrConfiguration

## 例 3

例 3 では、KeepCallDetailForDays プロパティが 30 日未満になっている CDR 設定がすべて削除されます。このタスクを実行するため、コマンドではパラメーターを指定せずに **Get-CsCdrConfiguration** コマンドレットを呼び出して、組織内で現在使用されているすべての CDR 設定のコレクションを戻します。次に、このコレクションは **Where-Object** コマンドレットにパイプ処理され、それにより、KeepCallDetailForDays プロパティが 30 日未満になっている設定のみが選択されます。その後、フィルター処理したコレクションは **Remove-CsCdrConfiguration** コマンドレットにパイプ処理され、コレクション内の各項目が削除されます。

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30} | Remove-CsCdrConfiguration

## 解説

通話詳細記録 (CDR) を使用することにより、Lync Server の機能 (ボイス オーバー IP (VoIP) 電話での通話、インスタント メッセージング、ファイル転送、音声/ビデオ (A/V) 会議、アプリケーション共有セッションなど) の利用状況を追跡できます。使用情報は CDR (監視サービスを展開した場合にのみ使用可能) によって追跡されます。たとえば、通話の関係者、通話時間、ファイル転送の有無などの情報を記録します (ただし CDR では、通話自体は記録されません)。

また、CDR は通話エラーの情報の追跡も行い、ピアツーピア セッションと電話会議の通話の両方の詳細な診断データを追跡します。

管理者として、CDR を組織で使用するかどうかを決めることができます。監視サービスが展開されている場合は、CDR を簡単に有効または無効にすることができます。さらに、この決定をグローバル (その場合、CDR は組織全体で有効または無効のいずれかになります) またはサイトごとに行うことができます。たとえば、CDR を Redmond サイトでは使用可能にして、Paris サイトでは CDR を使用不可能にすることができます。

**New-CsCdrConfiguration** コマンドレットを使用して作成したサイト固有の設定は、後で **Remove-CsCdrConfiguration** コマンドレットを使用して削除できます。サイト固有の設定を削除すると、影響を受けるサイトの CDR は、グローバル CDR 構成設定によって自動的に制御されます。

また、グローバル CDR 設定に対して **Remove-CsCdrConfiguration** コマンドレットを実行することもできます。ただし、グローバル設定は削除できないため、代わりに既定値にリセットされます。たとえば、グローバル設定の KeepCallDetailForDays プロパティの値を 90 に設定するとします。グローバル設定に対して **Remove-CsCdrConfiguration** コマンドレットを実行すると、そのプロパティは既定値の 60 にリセットされます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Remove-CsCdrConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCdrConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>削除する CDR 構成設定の一意の識別子です。グローバル設定を &quot;削除&quot; するには、次の構文を使用します。-Identity global。(繰り返しになりますが、グローバル設定を実際に削除することはできません。プロパティを既定値にリセットできるだけです)。サイト スコープから設定を削除するには、次のような構文を使用します。-Identity site:Redmond。Identity 指定時はワイルドカードは使用できません。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings。**Remove-CsCdrConfiguration** コマンドレットは、パイプライン処理された CDR 構成オブジェクトの入力を受け入れます。

## 戻り値の種類

なし。代わりに、このコマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings オブジェクトのインスタンスを削除します。

## 関連項目

#### その他のリソース

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

