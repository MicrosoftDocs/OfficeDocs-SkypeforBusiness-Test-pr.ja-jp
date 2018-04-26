---
title: Set-CsClientVersionConfiguration
TOCTitle: Set-CsClientVersionConfiguration
ms:assetid: 7cd2e86f-2d31-4db2-9d0f-f1418fd4aba2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398623(v=OCS.15)
ms:contentKeyID: 48272633
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

クライアント バージョン構成設定の指定したコレクションを変更します。クライアント バージョンの構成設定によって、システムにログオンする各クライアント アプリケーションのバージョン番号を Lync Server が確認するかどうかが決定されます。クライアント バージョン フィルターが有効な場合、クライアント アプリケーションがシステムにアクセス可能かどうかは、該当するクライアント バージョン ポリシーに構成された設定に基づきます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsClientVersionConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、**Set-CsClientVersionConfiguration** コマンドレットを使用して、Identity が "site:Redmond" の設定コレクションを変更します。この場合、クライアント バージョン構成設定を無効にするため、Enabled パラメーターを False に設定しています。

    Set-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## 例 2

例 2 では、組織内で現在使用中のすべてのクライアント バージョン構成設定の DefaultUrl プロパティが変更されます。これを実行するには、まずコマンドで、追加パラメーターを指定せずに **Get-CsClientVersionConfiguration** コマンドレットを呼び出し、すべてのクライアント バージョン構成設定を戻します。その情報を **Set-CsClientVersionConfiguration** コマンドレットにパイプ処理します。その結果、各構成コレクションの DefaultUrl 値が https://litwareinc.com/csclients に設定されます。

    Get-CsClientVersionConfiguration | Set-CsClientVersionConfiguration -DefaultURL "https://litwareinc.com/csclients"

## 例 3

例 3 では、DefaultAction が現在 Block に設定されているクライアント バージョン構成設定をすべて変更します。このタスクを実行するため、まず **Get-CsClientVersionConfiguration** コマンドレットを使用して、現在使用されているすべてのクライアント バージョン構成設定を戻しています。その情報は **Where-Object** コマンドレットにパイプ処理され、DefaultAction プロパティが "Block" と等しい項目のみを選択します。次に、フィルター処理されたコレクションを **Set-CsClientVersionConfiguration** コマンドレットにパイプ処理し、コレクション内の各項目に対して次の 2 つの処理を行います。1) DefaultAction を BlockWithUrl に設定し、2) DefaultUrl を https://litwareinc.com/csclients に設定します。

    Get-CsClientVersionConfiguration | Where-Object {$_.DefaultAction -eq "Block"} | Set-CsClientVersionConfiguration -DefaultAction "BlockWithUrl" -DefaultURL "https://litwareinc.com/csclients"

## 解説

Lync Server では、ユーザーがシステムへのログオンに使用できるクライアント ソフトウェア (および、同様に重要であるソフトウェア バージョン番号) の指定に関して、管理者にかなり大きな裁量が認められています。たとえば、ユーザーに Lync を使用して Lync Server にログオンすることを求める技術上の理由はありません。ユーザーが Microsoft Office Communicator 2007 R2 を使用してログオンすることを妨げる技術的な制限はありません。

その一方で、ユーザーが Office Communicator 2007 R2 を使用してログオンしないようにする必要がある、技術上以外の理由がある場合があります。たとえば、Office Communicator 2007 R2 では Lync にある機能すべてはサポートされません。その結果、Office Communicator 2007 R2 を使用してログオンするユーザーは、Lync を使用してログオンするユーザーとは異なる環境を利用することになります。このため、ユーザーにとっても、多数の異なるクライアント アプリケーションをサポートするヘルプ デスク担当者にとっても対応することが難しくなります。

このことが自組織にとって問題になる場合はクライアント バージョン フィルターを使用して、どのクライアント アプリケーションが Lync Server へのログオンに使用できるかを指定できます。Lync Server のインストール時、グローバルなクライアント バージョン構成設定のセットがインストールされて有効になります。これらの設定を使用して、クライアント バージョン フィルターを有効にするかどうかを指定します。このグローバル設定のほかに、クライアント バージョンの構成設定はサイト スコープでも適用できます。その場合は、サイト設定がグローバル設定よりも優先されます。

**Set-CsClientVersionConfiguration** コマンドレットを使用して、クライアント バージョン構成設定の既存のコレクションを変更できます。

クライアント バージョン構成がセキュリティ機能ではないという点に注意してください。このテクノロジはクライアント アプリケーションからの自己報告を信頼しています。アプリケーションが本当にそのアプリケーションであるかどうかの確認や、アプリケーションが申告したバージョン番号の検証を行おうとはしません。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsClientVersionConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionConfiguration"}

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
<td><p><em>DefaultAction</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>対象のクライアント バージョン ポリシー内に見つからないバージョン番号のクライアント アプリケーションから、ユーザーがログオンしようとした場合に、実行されるアクションを示します。DefaultAction は、以下に示すいずれかの値に設定されます。</p>
<p>Allow。クライアント アプリケーションのログオンを許可します。</p>
<p>AllowWithUrl。クライアント アプリケーションのログオンを許可します。また、承認されたクライアント アプリケーションをユーザーがダウンロードすることができる Web ページの URL が記載されたメッセージ ボックスが、ユーザーに対して表示されます。この Web ページの URL は、DefaultUrl プロパティの値として指定する必要があります。</p>
<p>Block。クライアント アプリケーションはログオンできません。</p>
<p>BlockWithUrl。クライアント アプリケーションはログオンできません。ただし、&quot;アクセス拒否&quot; のメッセージ ボックスをユーザーに表示します。このメッセージ ボックスには、承認されたクライアント アプリケーションをユーザーがダウンロードできる Web ページの URL が記載されています。この Web ページの URL は、DefaultUrl プロパティの値として指定する必要があります。</p>
<p>Enabled プロパティが False に設定されている場合、このプロパティは無視されます。Enabled プロパティが False に設定されている場合、クライアント バージョン フィルターは種類を問わず実行されません。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultURL</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>承認されたクライアント アプリケーションをユーザーがダウンロードできる Web ページの URL を指定します。この URL が指定されており、DefaultAction が BlockWithURL に設定されている場合、サポートされていないクライアント アプリケーションからログオンしようとすると、この URL が &quot;アクセスが拒否されました&quot; メッセージ ボックスに表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>クライアント バージョン フィルター処理を有効にするか無効にするかを指定します。Enabled プロパティが True の場合、ログオンしようとしている各クライアント アプリケーションのバージョン番号がサーバーでチェックされ、該当するクライアント バージョン ポリシーに基づいてアクセスが許可または拒否されます。Enabled プロパティが False の場合、ログオン機能を備えたすべてのクライアント アプリケーションのログオンを許可します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>変更するクライアント バージョン構成設定の一意の識別子を表します。グローバル設定を変更するには、次のような構文を使用します。-Identity global。サイト スコープに割り当てられた設定を変更するには、次のような構文を使用します。&quot;site:Redmond&quot;。</p>
<p>このパラメーターが含まれない場合は、<strong>Set-CsClientVersionConfiguration</strong> コマンドレットがグローバル設定を自動的に構成します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>ClientVersionPolicy オブジェクト</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration オブジェクト。**Set-CsClientVersionConfiguration** コマンドレットは、パイプライン処理されたクライアント バージョン構成オブジェクトのインスタンスを受け入れます。

## 戻り値の種類

**Set-CsClientVersionConfiguration** コマンドレットは、値またはオブジェクトを戻しません。代わりに、Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration オブジェクトのインスタンスを構成します。

## 関連項目

#### その他のリソース

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)

