---
title: Remove-CsConferencingConfiguration
TOCTitle: Remove-CsConferencingConfiguration
ms:assetid: a3dff4b0-100b-46fa-9078-d3b0d4914d87
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412767(v=OCS.15)
ms:contentKeyID: 48273162
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferencingConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

指定された会議構成設定のコレクションを削除します。会議構成設定では、会議コンテンツや資料の最大許容サイズ、コンテンツの猶予期間、サポートされているクライアントの内部ダウンロード用および外部ダウンロード用の URL などを指定します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、Redmond サイトに適用されていた会議構成設定が削除されます。このようなサイト設定が削除されると、そのサイトのユーザーは、グローバル会議構成設定の各種設定を自動的に継承します。

    Remove-CsConferencingConfiguration -Identity site:Redmond

## 例 2

例 2 に示すコマンド を実行すると、サイト スコープに適用されていたすべての会議構成設定が削除されます。これを行うため、まず **Get-CsConferencingConfiguration** コマンドレットに Filter パラメーターとフィルター値 "site:" を指定して呼び出します。これにより、"site:" という文字列で始まる ID を持つ設定だけが戻されます。次に、このフィルター処理されたコレクションを **Remove-CsConferencingConfiguration** コマンドレットにパイプ処理し、コレクション内の各項目を削除しています。

    Get-CsConferencingConfiguration -Filter site:* | Remove-CsConferencingConfiguration

## 例 3

例 3 では、組織が Litwareinc に設定されていないすべての会議構成設定が削除されます。これを行うため、まず、パラメーターを指定せずに **Get-CsConferencingConfiguration** コマンドレットを呼び出して、組織で使用されているすべての会議構成設定のコレクションを戻します。次に、このコレクションを **Where-Object** コマンドレットにパイプ処理し、Organization プロパティが Litwareinc に等しくない設定のみを選択します。最後に、フィルターされたコレクションを **Remove-CsConferencingConfiguration** コマンドレットにパイプ処理し、コレクション内のすべての設定を削除します。

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"} | Remove-CsConferencingConfiguration

## 解説

会議に関しては、運用管理を行うコマンドレットが 2 つのセットに分かれています。ユーザーに対して許可することと許可しないことを管理する場合は、**CsConferencingPolicy** コマンドレットを使う必要があります。これは、たとえば匿名ユーザーの会議への参加を招待できるようにすることや、会議中のアプリケーション共有の実行やファイル転送をユーザーに許可する場合です。

管理者はユーザー アクティビティのほかに、Web 会議サービス を管理する必要があります。たとえば、1 つの会議に割り当てるコンテンツ保存領域のサイズの上限を指定したり、会議資料が自動的に削除されるまでの猶予期間を指定したりできる必要があります。また管理者は、アプリケーション共有やファイル転送などのアクティビティで使用するポートも指定できる必要があります。

後から述べた方の作業は、**CsConferencingConfiguration** コマンドレットを使って管理できます。これらのコマンドレットを使用すると、実際のサーバーそのものを管理できます。**CsConferencingConfiguration** コマンドレット (グローバル スコープ、サイト スコープ、およびサービス スコープに適用できます) では、ユーザーに対して会議中のアプリケーション共有を許可するかどうかを指定することはできませんが、アプリケーション共有が許可されている場合はこのコマンドレットを使って、そのアクティビティに使用するポートを指定できます。同様に、このコマンドレットを使用して、保存領域の上限や有効期限、ユーザーが会議に関するヘルプや資料を取得できる内部 URL および外部 URL などを指定できます。

**Remove-CsConferencingConfiguration** コマンドレットでは、組織内で使用するように作成された会議構成設定のカスタム コレクションのいずれかを削除できます。設定のコレクションを削除すると、その設定によってそれまで適用されていたサーバーは、自動的に次の階層 (サービス - サイト - スコープ) のコレクションによって管理されるようになります。削除した設定がサービス スコープに適用されていた場合は、該当するサーバーはサイト設定で管理されるようになります。サイト スコープに設定がない場合は、該当するサーバーはグローバル設定で管理されるようになります。同様に、サイト スコープの設定を削除した場合、そのサイト設定によってそれまで管理されていたサーバーは、グローバル設定で管理されるようになります。

なお、**Remove-CsConferencingConfiguration** コマンドレットはグローバル設定に対しても実行できます。ただし、その場合、グローバル設定は削除されません (Lync Server ではグローバル設定を削除できないため)。その代わりに、グローバル コレクション内のすべてのプロパティが既定値でリセットされます。たとえば、それまでコンテンツの保存領域のサイズの上限値を 200 MB に変更していた場合、このプロパティは既定値の 100 MB にリセットされます。

このコマンドレットを実行できるユーザー: 既定では、**Remove-CsConferencingConfiguration** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferencingConfiguration"}

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
<td><p>削除する会議構成設定コレクションの一意の識別子。サイト スコープで構成されている設定を削除するには、次のような構文を使用します: -Identity &quot;site:Redmond&quot;。サービス スコープで構成されている設定を削除するには、次のような構文を使用します: -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;。</p>
<p><strong>Remove-CsConferencingConfiguration</strong> コマンドレットはグローバル設定に対しても実行できます。ただしこの場合設定は削除されず、代わりにすべてのプロパティが既定値にリセットされます。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings オブジェクトです。**Remove-CsConferencingConfiguration** コマンドレットは、会議構成オブジェクトのインスタンスをパイプ処理で受け入れます。

## 戻り値の種類

なし。代わりに、**Remove-CsConferencingConfiguration** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings オブジェクトの既存のインスタンスを削除します。

## 関連項目

#### その他のリソース

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

