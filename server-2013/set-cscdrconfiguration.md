---
title: Set-CsCdrConfiguration
TOCTitle: Set-CsCdrConfiguration
ms:assetid: 977f0d3e-796b-43a3-bc0c-82ea91741c52
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398774(v=OCS.15)
ms:contentKeyID: 48272957
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCdrConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

既存の通話詳細記録 (CDR) 設定のコレクションを変更します。CDR では、ピアツーピアのインスタント メッセージング セッション、ボイス オーバー IP (VoIP) 電話の通話、電話会議などの使用状況を追跡できます。この使用状況データの中には、通話の発信者と受信者、通話時刻、通話時間の情報が含まれます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCdrConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、古いレコードを削除する時刻を設定します。この例では、時刻を 23 (11:00 P.M. の 24 時間表記) に設定します。Identity パラメーターを使用して、Identity が site:Redmond の CDR 設定に対してのみ、この変更が適用されるようにします。

    Set-CsCdrConfiguration -Identity site:Redmond -PurgeHourOfDay 23 

## 例 2

例 2 は、例 1 に示したコマンドの変化形です。この例では、組織内で現在使用されている各 CDR 構成設定コレクションの PurgeHourOfDay プロパティを変更します。これを行うため、まず **Get-CsCdrConfiguration** コマンドレットをパラメーターを指定せずに呼び出し、現在使用されているすべての CDR 設定のコレクションを戻します。次に、このコレクションを **Set-CsCdrConfiguration** コマンドレットへパイプ処理し、コレクション内の各項目を取得して、PurgeHourOfDay プロパティの値を 11:00 PM (23) に変更します。

    Get-CsCdrConfiguration | Set-CsCdrConfiguration -PurgeHourOfDay 23 

## 例 3

例 3 では、例 1 で使ったコマンドのもう 1 つの変化形を示しています。この例では、サイト スコープで構成されているすべての CDR 設定について、PurgeHourOfDay プロパティを変更します。これを行うため、まず **Get-CsCdrConfiguration** コマンドレットに Filter パラメーターを指定して呼び出します。フィルター値 "site:\*" により、Identity が文字列値 "site:" で始まる CDR 設定のみが返されます。次に、フィルター後のコレクションを **Set-CsCdrConfiguration** コマンドレットへパイプ処理し、コレクション内の各項目の PurgeHourOfDay プロパティを変更します。

    Get-CsCdrConfiguration -Filter "site:*"| Set-CsCdrConfiguration -PurgeHourOfDay 23

## 解説

通話詳細記録 (CDR) では、ボイス オーバー IP (VoIP) 電話の通話、インスタント メッセージング (IM)、ファイル転送、音声ビデオ (A/V) 会議、アプリケーション共有セッションなどの Lync Server 機能の使用状況を追跡できます。CDR (監視サービスを展開した場合にのみ使用可能) は利用状況に関する情報を保持します。通話者、通話時間、ファイル転送の有無などの情報を記録します。ただし、CDR では通話の内容自体は記録されません。

また、CDR は通話エラーの情報の追跡も行い、ピアツーピア セッションと電話会議の通話の両方の詳細な診断データを追跡します。

CDR を組織内で使用するかどうかは、管理者として決定できます。CDR は、監視サービスが展開されていれば簡単に有効または無効にできます。また、これをグローバルに適用するか (この場合、組織全体で CDR を有効または無効にします)、サイトごとに適用するかも決定できます。たとえば、Redmond サイトでは CDR を使用するが、Paris サイトでは CDR を使用しないようにすることもできます。

管理者は CDR データベースの管理も行うことができます。たとえば、CDR レコードがデータベースから削除されるまでの保持日数を指定できます。このような変更は、**Set-CsCdrConfiguration** コマンドレットを使用して行うことができます。

このコマンドレットを実行できるユーザー: 既定では、**Set-CsCdrConfiguration** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCdrConfiguration"}

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
<td><p><em>EnableCDR</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>CDR が有効か無効かを示します。既定値は True です。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>CDR データベースから CDR レコードを定期的に削除するかどうかを示します。True (既定値) の場合、KeepCallDetailForDays プロパティ (CDR レコードの場合) および KeepErrorReportForDays プロパティ (CDR エラーの場合) で指定されている期間を過ぎると、レコードが削除されます。False の場合、CDR レコードは無期限に保持されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>CDR 構成設定のコレクションに割り当てられた一意の識別子です。グローバル設定を参照するには、次の構文を使用します。-Identity global。サイト スコープで構成されるコレクションを参照するには、次のような構文を使用します。-Identity site:Redmond。Identity を指定するときに、ワイルドカード文字を使用することはできません。</p>
<p>このパラメーターを省略すると、<strong>Set-CsCdrConfiguration</strong> コマンドレットはグローバル設定を変更します。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>CdrSettings オブジェクト</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt32</p></td>
<td><p>CDR データベースに CDR レコードを保持する日数を示します。指定された日数より古いレコードは、自動的に削除されます (削除が実行されるのは、EnablePurging プロパティが True に設定されている場合のみです)。</p>
<p>このプロパティに設定できる値は、1 ～ 2,562 日 (約 7 年) の整数値です。既定値は 60 です。</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt32</p></td>
<td><p>CDR エラー報告を保持する日数を示します。指定された日数より古い報告は、自動的に削除されます。CDR エラー報告は、Lync 2013 などのクライアント アプリケーションがアップロードする診断レポートです。</p>
<p>このプロパティに設定できる値は、1 ～ 2,562 日 (約 7 年) の整数値です。既定値は 60 です。</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt32</p></td>
<td><p>期限切れのレコードが CDR データベースから削除されるときのローカル時刻を示します。この時刻は 24 時間制で指定します。0 は深夜 0 時を表し、23 は午後 11 時を表します。なお、時刻は 1 時間刻みでのみ指定できます。つまり、午前 4:00 に削除が実行されるようにスケジュールすることはできますが、午前 4:30 や午前 4:15 に実行されるようにスケジュールすることはできません。既定値は 2 です (午前 2:00)。削除は業務時間外に実行することをお勧めします。</p>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings です。**Set-CsCdrConfiguration** コマンドレットは、通話詳細記録構成オブジェクトのパイプ処理による入力を受け入れます。

## 戻り値の種類

**Set-CsCdrConfiguration** コマンドレットは、値またはオブジェクトを戻しません。代わりに、Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CDRSettings オブジェクトのインスタンスを構成します。

## 関連項目

#### その他のリソース

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)

