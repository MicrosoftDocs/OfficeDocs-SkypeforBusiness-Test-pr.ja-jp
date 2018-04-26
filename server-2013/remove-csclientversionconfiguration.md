---
title: Remove-CsClientVersionConfiguration
TOCTitle: Remove-CsClientVersionConfiguration
ms:assetid: 42065d1d-a0ef-4fa4-826b-d65b14b343c9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425925(v=OCS.15)
ms:contentKeyID: 48271905
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

指定したクライアント バージョンの構成設定のコレクションを削除します。クライアント バージョン構成設定により、システムにログオンする各クライアント アプリケーションのバージョン番号を Lync Server が確認するかどうかを決定します。クライアント バージョンのフィルター処理が有効になっている場合、クライアント アプリケーションがシステムにアクセスできるかどうかは、該当するクライアント バージョン ポリシーに構成されている設定に基づきます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 のコマンドでは、"site:Redmond" という Identity を持つクライアント バージョン構成設定を削除しています。

    Remove-CsClientVersionConfiguration -Identity site:Redmond

## 例 2

例 2 では、サイト スコープで適用されているクライアント バージョンの構成設定をすべて削除しています。このタスクを実行するため、コマンドでまず Filter パラメーターを指定して **Get-CsClientVersionConfiguration** コマンドレットを呼び出します。フィルター値 "site:\*" により、文字列値 "site:" で始まる Identity を持つクライアント バージョン構成設定のみが返されます。このフィルター処理したコレクションを **Remove-CsClientVersionConfiguration** コマンドレットにパイプ処理し、コレクション内の各項目を削除します。

    Get-CsClientVersionConfiguration -Filter site:* | Remove-CsClientVersionConfiguration

## 例 3

例 3 では、現在無効となっているクライアント バージョンの構成設定をすべて削除しています。これを行うため、コマンドでまず **Get-CsClientVersionConfiguration** コマンドレットを使用して、組織で現在使用中のすべてのクライアント バージョン構成設定のコレクションを戻します。このデータが戻された後、コレクションを **Where-Object** コマンドレットにパイプ処理し、Enabled プロパティが False と等しい設定のみ取得します。次に、フィルター処理されたコレクションを **Remove-CsClientVersionConfiguration** コマンドレットにパイプ処理し、コレクション内の各項目を削除します。

    Get-CsClientVersionConfiguration | Where-Object {$_.Enabled -eq $False} | Remove-CsClientVersionConfiguration

## 解説

Lync Server では、システムへのログオンにユーザーが使用できるクライアント ソフトウェアの指定に関して、(および同じく重要な点として、そのソフトウェアのバージョン番号の指定に関しても) 管理者に大きな自由度が与えられています。たとえば、ユーザーに Lync Server を使用して Lync にログオンすることを求める技術上の理由はありません。技術上の観点からは、ユーザーが Microsoft Office Communicator 2007 R2 を使用してログオンできないようにする必要はありません。

ただし、ユーザーが Office Communicator 2007 R2 を使用してログオンしないようにする必要がある、技術上以外の理由がある場合があります。たとえば、Office Communicator 2007 R2 では、Lync の機能すべてはサポートされていません。そのため、Office Communicator 2007 R2 を使用してログオンするユーザーは、Lync を使用してログオンするユーザーとは操作性が異なります。このことは、ユーザーを混乱させる可能性があります。また複数の異なるクライアント アプリケーションをサポートする必要があるため、ヘルプデスク要員を混乱させる可能性もあります。

これが組織で問題となる場合は、クライアント バージョンのフィルター処理を使用して、Lync Server へのログオンに使用できるクライアント アプリケーションを指定できます。Lync Server のインストール時、グローバルなクライアント バージョン構成設定のセットがインストールされて有効になります。クライアント バージョン構成設定は、グローバル設定のほかサイト スコープでも適用できます。

作成したサイト設定は、**Remove-CsClientVersionConfiguration** コマンドレットを使用して後で削除できます。また、**Remove-CsClientVersionConfiguration** コマンドレットをグローバル設定に対して実行することもできます。この場合、グローバル設定は削除されるのではなく、グローバル プロパティが既定値にリセットされます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Remove-CsClientVersionConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionConfiguration"}

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
<td><p>削除するクライアント バージョンの構成設定のコレクションを表す一意の識別子です。グローバル コレクションの削除には、次の構文を使用します。-Identity global (ただしこの場合、グローバル設定は実際に削除されるのではなく、グローバル プロパティがすべて既定値にリセットされます)。サイト コレクションを削除するには、次のような構文を使用します。-Identity site:Redmond。Identity 指定時はワイルドカードを使用できないことに注意してください。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration オブジェクト。**Remove-CsClientVersionConfiguration** コマンドレットは、クライアント バージョン構成オブジェクトのパイプ処理されたインスタンスを受け入れます。

## 戻り値の種類

なし。代わりに、Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration オブジェクトのインスタンスを削除します。

## 関連項目

#### その他のリソース

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

