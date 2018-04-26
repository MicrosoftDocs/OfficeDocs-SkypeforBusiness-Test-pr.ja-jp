---
title: Get-CsCdrConfiguration
TOCTitle: Get-CsCdrConfiguration
ms:assetid: 4af8ffa2-63d3-4873-8dac-5afede090d4f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398298(v=OCS.15)
ms:contentKeyID: 48272004
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCdrConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

通話詳細記録 (CDR) の設定に関する情報を戻します。CDR により、ピアツーピアのインスタント メッセージング セッション、ボイス オーバー IP (VoIP) 電話での通話、電話会議などの使用状況を追跡できます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCdrConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

この例では、**Get-CsCdrConfiguration** コマンドレットを使用して、組織内で使用するよう構成されているすべての CDR 設定のコレクションを戻しています。

    Get-CsCdrConfiguration

## 例 2

例 2 では、Identity パラメーターを使用して、ID が site:Redmond の CDR 設定のコレクションを 1 つ戻しています。

    Get-CsCdrConfiguration -Identity site:Redmond

## 例 3

例 3 では、Filter パラメーターを使用して、サイト スコープで構成されているすべての CDR 設定を戻します。フィルター値 "site:\*" を指定して、文字列値 "site:" で始まる ID を持つすべての CDR 設定を戻しています。定義上、これらはサイト スコープで構成されている設定です。

    Get-CsCdrConfiguration -Filter site:*

## 例 4

例 4 では、KeepCallDetailForDays プロパティが 30 日未満であるすべての CDR 設定のコレクションを戻します。これを実行するため、まず、**Get-CsCdrConfiguration** コマンドレットを使用して、組織内に構成されているすべての CDR 設定のコレクションを戻します。次に、このコレクションを **Where-Object** コマンドレットにパイプ処理して、KeepCallDetailForDays 値が 30 日未満になっている設定のみを取得します。

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30}

## 解説

通話詳細記録 (CDR) を使用することにより、Lync Server の機能 (ボイス オーバー IP (VoIP) 電話での通話、インスタント メッセージング (IM)、ファイル転送、音声/ビデオ (A/V) 会議、アプリケーション共有セッションなど) の使用状況を追跡できます。CDR は監視サービスを展開している場合にのみ使用可能で、使用状況の情報を記録します。通話の関係者、通話の長さ、ファイル転送の有無などの情報を記録します (ただし、CDR では通話内容そのものは記録されません)。

また、CDR は通話エラーの情報も記録します。ピアツーピア セッションと電話会議の通話の両方の詳細な診断データを追跡します。

管理者として、CDR を組織で使用するかどうかを決めることができます。監視サービスが展開されている場合は、CDR を有効または無効にすることができます。さらに、この決定をグローバル (その場合、CDR は組織全体で有効または無効のいずれかになります) またはサイトごとに行うことができます。たとえば、CDR を Redmond サイトでは使用可能にして、Paris サイトでは CDR を使用不可能にすることができます。

**Get-CsCdrConfiguration** コマンドレットにより、組織での CDR の使用方法に関する詳細情報を戻すことができます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Get-CsCdrConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCdrConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>ワイルドカード文字を使用して、CDR 構成設定のコレクションを戻すことができます。たとえば、サイト スコープで構成されているすべての設定のコレクションを戻すには、次の構文を使用します。-Filter site:*。Identity の一部の文字列値が &quot;Western&quot; であるすべての設定のコレクションを戻すには、次の構文を使用します。-Filter *Western*。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>戻す対象となる CDR 構成設定のコレクションを表す一意の識別子を示します。グローバル設定を参照するには、次の構文を使用します。-Identity global。サイト スコープで構成されるコレクションを参照するには、次のような構文を使用します。-Identity site:Redmond。Identity 指定時はワイルドカードを使用できないことに注意してください。ワイルドカードを使用する必要がある場合は、代わりに Filter パラメーターを使用してください。</p>
<p>このパラメーターが指定されていない場合は、<strong>Get-CsCdrConfiguration</strong> コマンドレットを実行すると、組織内で現在使用されているすべての CDR 構成設定のコレクションが戻されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア自体からではなく、中央管理ストアのローカル レプリカから CDR 構成データを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsCdrConfiguration** コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

**Get-CsCdrConfiguration** コマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

