---
title: New-CsCdrConfiguration
TOCTitle: New-CsCdrConfiguration
ms:assetid: e5890ac3-7a6c-4609-a866-84c39b76d3a9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399018(v=OCS.15)
ms:contentKeyID: 48273885
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCdrConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

新しい通話詳細記録 (CDR) 設定セットを作成します。CDR を使用すると、ピアツーピア インスタント メッセージング セッション、ボイス オーバー IP (VoIP) 電話での通話、電話会議の通話などの使用状況を追跡できます。こうした使用状況データには、だれがいつ、だれに通話し、どれほどの通話時間であったかに関する情報が含まれます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 のコマンドでは、**New-CsCdrConfiguration** コマンドレットを使用して、Identity が site:Redmond の新しい CDR 設定を作成しています。この新しい設定に Identity site:Redmond のほか、EnableCDR プロパティ False も設定しています。サイト設定はグローバル設定よりも優先されるため、グローバル スコープで CDR が有効になっているかどうかにかかわらず、Redmond サイトでは CDR を使用しません。

    New-CsCdrConfiguration -Identity site:Redmond -EnableCDR $False

## 例 2

例 2 では、InMemory パラメーターを使用して、最初にメモリ内だけに存在する新しい CDR 構成設定コレクションを作成する方法を示しています。これを行うため、例ではまず **New-CsCdrConfiguration** コマンドレットに InMemory パラメーターを指定して Identity が site:Redmond の設定の仮想コレクションを作成し、この仮想コレクションを変数 $x に格納しています。このコレクションは、変数に格納しないと作成後すぐに消滅します。

仮想コレクションを作成した後、2 行目のコマンドで EnableCDR プロパティの値を False ($False) に設定しています。次に、3 行目で **Set-CsCdrConfiguration** コマンドレットを使用して、仮想コレクション $x を Redmond サイトに適用する実際の CDR 構成設定コレクションに変換しています。**Set-CsCdrConfiguration** コマンドレットを呼び出さなければ、この仮想コレクションは Windows PowerShell セッションが終了したとき、または変数 $x が削除されたときにすぐ消滅します。

    $x = New-CsCdrConfiguration -Identity site:Redmond -InMemory
    $x.EnableCDR = $False
    Set-CsCdrConfiguration -Instance $x

## 解説

通話詳細記録 (CDR) を使用すると、ボイス オーバー IP (VoIP) 電話での通話、インスタント メッセージング (IM)、ファイル転送、音声またはビデオ (A/V) 会議、アプリケーション共有セッションなど、Lync Server 機能の使用状況を追跡できます。CDR (監視サービスを展開している場合にのみ使用可能) は、使用状況の情報を追跡し、通話の関係者、通話時間の長さ、ファイル転送の有無といった情報をログに記録します (ただし、CDR では通話そのものの録音は行われません)。

また、CDR は通話エラーの情報の追跡も行い、ピアツーピア セッションと電話会議の通話の両方の詳細な診断データを追跡します。

管理者として、組織で CDR を使用するかどうかを決定できます。監視サービスが展開されていれば、容易に CDR を有効または無効にできます。さらに、この決定をグローバル (その場合、CDR は組織全体で有効または無効のいずれかになります) またはサイトごとに行うことができます。たとえば、CDR を Redmond サイトでは使用可能にして、Paris サイトでは CDR を使用不可能にすることができます。

**New-CsCdrConfiguration** コマンドレットを使用して、サイト スコープで新しい CDR 設定コレクションを作成できます (グローバル スコープで新しい設定を作成することはできません)。各サイトがホストできるのは 1 つの CDR 設定コレクションだけであることに注意してください。つまり、Redmond サイトに既に CDR 構成設定がある場合、このサイトに新しいコレクションを作成することはできません。作成しようとすると、コマンドは失敗します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーは **New-CsCdrConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCdrConfiguration"}

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
<td><p>必須かどうか</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>新しい CDR 構成設定コレクションに割り当てる一意の識別子を表します。新しいコレクションはサイト スコープのみで作成できるので、Identity には常に &quot;site:&quot; のプレフィックスが付きます。その後にサイト名が続きます。たとえば、&quot;site:Redmond&quot; です。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCDR</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>CDR が有効かどうかを示します。既定値は True です。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>CDR の記録を CDR データベースから定期的に削除するかどうかを示します。True (既定値) の場合、KeepCallDetailForDays プロパティ (CDR の場合) と KeepErrorReportForDays プロパティ (CDR エラーの場合) により指定された期間を過ぎると記録が削除されます。False の場合、CDR の記録は無期限に保持されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>永続的な変更としてオブジェクトをコミットせずに、オブジェクト参照を作成します。このパラメーターを指定して呼び出したコマンドレットの出力を変数に割り当てる場合、オブジェクト参照のプロパティを変更し、コマンドレットに対応する Set- コマンドレットを呼び出してそれらの変更をコミットできます。</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt32</p></td>
<td><p>CDR の記録を CDR データベースに保持する日数を示します。指定した日数より古い記録は自動的に削除されます (ただし、この削除が実行されるのは EnablePurging プロパティが True に設定されている場合のみです)。</p>
<p>KeepCallDetailForDays には、1 ～ 2,562 日 (約 7 年間) の間の整数値を設定できます。既定値は 60 です。</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt32</p></td>
<td><p>CDR エラー報告を保持する日数を指定します。指定した日数を超えて保持されている報告は、自動的に削除されます。CDR エラー報告は、Lync 2013 のようなクライアント アプリケーションによってアップロードされる診断レポートです。</p>
<p>このプロパティには、1 ～ 2,562 日 (約 7 年間) の間の整数値を設定できます。既定値は 60 です。</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt32</p></td>
<td><p>CDR データベースの期限切れの記録の削除を実行するローカル時刻を示します。時刻は 24 時間制を使用して指定します。0 は夜中 12 時 (12:00 AM) を、23 は 11:00 PM を表します。時刻は正時しか指定できないことに注意してください。削除を 4:00 AM に実行するようにスケジュールすることはできますが、4:30 AM や 4:15 AM に実行するようにスケジュールすることはできません。既定値は 2 (2:00 AM) です。削除を実行する時刻は、作業を行わない時間帯に設定することをお勧めします。</p>
<p>データベースの削除は、EnablePurging プロパティが True に設定されている場合にのみ実行されます。</p></td>
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

なし。**New-CsCdrConfiguration** コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings オブジェクトのインスタンスを作成します。

## 関連項目

#### その他のリソース

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

