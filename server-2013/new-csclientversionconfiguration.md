---
title: New-CsClientVersionConfiguration
TOCTitle: New-CsClientVersionConfiguration
ms:assetid: e7aac850-9e29-4d18-8929-74a89e9355cd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399029(v=OCS.15)
ms:contentKeyID: 48274010
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

クライアント バージョン構成設定の新しいコレクションを作成します。クライアント バージョン構成設定を使用すると、システムにログオンする各クライアント アプリケーションのバージョン番号を Lync Server がチェックするかどうかを決定できます。クライアント バージョン フィルターが有効になっている場合は、クライアント アプリケーションがシステムにアクセスできるかどうかが、適切なクライアント バージョン ポリシー内で構成されている設定に基づくことになります。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドでは、Redmond サイト用のクライアント バージョン構成設定の新しいコレクションを作成しています。このコマンドでは、Enabled パラメーターを False に設定しています。このため、Redmond サイトではクライアント フィルターが無効になります。

    New-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## 例 2

例 2 では、クライアント バージョン構成設定の新しいコレクションをメモリ内で作成し、そのコレクションを変更し、その後これらの仮想設定を Redmond サイトに適用する実際の設定のコレクションに変換する方法を示しています。これを行うため、まず **New-CsClientVersionConfiguration** コマンドレットに InMemory パラメーターを指定し、Identity が site:Redmond である設定のメモリ内専用コレクションを作成しています。このコレクションは $x という名前の変数に格納され、メモリ内のみに存在しています。これらのクライアント バージョン構成設定は、Windows PowerShell セッションを終了するか変数 $x を削除すると消滅し、Redmond サイトにはまったく適用されません。

コマンド 2 では、仮想設定の DefaultAction プロパティの値を Block に設定しています。コマンド 3 では、**Set-CsClientVersionConfiguration** コマンドレットを使用して、この仮想設定を Redmond サイトに適用する実際のクライアント バージョン構成設定のコレクションに変換しています。

    $x = New-CsClientVersionConfiguration -Identity site:Redmond -InMemory
    $x.DefaultAction = "Block" 
    Set-CsClientVersionConfiguration -Instance $x

## 解説

Lync Server では、ユーザーがシステムへのログオンに使用できるクライアント ソフトウェア (および、同様に重要であるソフトウェア バージョン番号) の指定に関して、管理者にかなり大きな裁量が認められています。たとえば、Lync Server を使用した Lync へのログオンをユーザーに要求する技術的な理由はありません。また、ユーザーが Microsoft Office Communicator 2007 R2 を使用してログオンすることを妨げる技術的な制限もありません。

ただし、ユーザーは Office Communicator 2007 R2 を使用してログオンしないほうがよい、とする非技術的な理由はいくつか考えられます。たとえば、Office Communicator 2007 R2 は Lync にある機能のすべてをサポートしているわけではありません。そのため、Office Communicator 2007 R2 を使用してログオンするユーザーのエクスペリエンスは、Lync を使用してログオンするユーザーとは異なるものになります。これは、ユーザーにとって問題となる可能性があります。また、多数の異なるクライアント アプリケーションに対するサポートを提供しなければならないヘルプ デスク担当者にとっても問題となる可能性があります。

こうした点が組織にとって問題となる可能性がある場合は、Lync Server へのログオンに使用できるクライアント アプリケーションを指定するために、クライアント バージョン フィルターを利用できます。Lync Server をインストールすると、クライアント バージョン構成設定のグローバル セットがインストールされ、有効になります。これらの設定は、クライアント バージョン フィルターが有効になっているかどうかを決定するために使用されます。

グローバル設定以外に、**New-CsClientVersionConfiguration** コマンドレットを使用して、サイト スコープでクライアント バージョン構成設定を作成できます。サイト スコープでクライアント バージョン構成設定を適用すると、その設定はグローバル設定よりも優先されます。たとえば、グローバル スコープでクライアント バージョン フィルターを有効にしている場合に、Redmond サイトでクライアント バージョン フィルターが無効になっている別の設定コレクションを作成するとします。この場合、Redmond サイトにアカウントを持つすべてのユーザーに対して、クライアント バージョン フィルターが無効になります。

匿名ユーザーは、グローバル設定の影響のみを受けることに注意してください。これは、匿名ユーザーがサイトに関連付けられていないからです。

クライアント バージョン構成はセキュリティ機能ではありません。このテクノロジはクライアント アプリケーションからの自己報告を信頼しています。アプリケーションが本当にアプリケーションであるかどうかの確認や、アプリケーションが申告したバージョン番号の検証を行おうとはしません。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーは **New-CsClientVersionConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionConfiguration"}

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
<td><p>新しいクライアント バージョン構成設定のコレクションに割り当てる一意識別子を表します。新しいコレクションはサイト スコープのみで作成できるので、Identity には常に &quot;site:&quot; のプレフィックスが付きます。その後にサイト名が続きます。たとえば、&quot;site:Redmond&quot; です。Identity site:Redmond の設定コレクションが既に存在している場合、上記のコマンドはエラーになります。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultAction</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>適切なクライアント バージョン ポリシー内に見つからないバージョン番号のクライアント アプリケーションからユーザーがログオンしようとした場合に実行する操作を示します。DefaultAction は、以下に示すいずれかの値に設定する必要があります。</p>
<p>Allow。クライアント アプリケーションのログオンを許可します。</p>
<p>AllowWithUrl。クライアント アプリケーションのログオンを許可します。さらに、承認されたクライアント アプリケーションをダウンロードできる Web ページの URL が記載されているメッセージ ボックスをユーザーに対して表示します。この Web ページの URL は DefaultUrl プロパティの値として指定する必要があります。</p>
<p>Block。クライアント アプリケーションはログオンできません。</p>
<p>BlockWithUrl。クライアント アプリケーションはログオンできません。ただし、&quot;アクセス拒否&quot; のメッセージ ボックスをユーザーに対して表示します。このメッセージ ボックスには、承認されたクライアント アプリケーションをダウンロードできる Web ページの URL が記載されています。この Web ページの URL は DefaultUrl プロパティの値として指定する必要があります。</p>
<p>Enabled プロパティが False に設定されている場合、このプロパティは無視されます。Enabled プロパティが False に設定されている場合、クライアント バージョン フィルターは種類を問わず実行されません。</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultURL</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>承認されたクライアント アプリケーションをダウンロードできる Web ページの URL を指定します。この URL が指定されており、DefaultAction が BlockWithURL に設定されている場合、サポートされていないクライアント アプリケーションからログオンしようとすると、この URL が &quot;アクセスが拒否されました&quot; メッセージ ボックスに表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>クライアント バージョン フィルターが有効か無効かを示します。Enabled プロパティが True の場合、ログオンを試行した各クライアント アプリケーションのバージョン番号がサーバーによって確認されます。そして、適切なクライアント バージョン ポリシーに基づいてアクセスを許可または拒否します。Enabled プロパティが False の場合、ログオン機能を備えたすべてのクライアント アプリケーションのログオンを許可します。</p>
<p>既定値は True です。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>永続的な変更としてオブジェクトをコミットせずに、オブジェクト参照を作成します。このパラメーターを指定して呼び出したコマンドレットの出力を変数に割り当てる場合、オブジェクト参照のプロパティを変更し、コマンドレットに対応する Set- コマンドレットを呼び出してそれらの変更をコミットできます。</p></td>
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

なし。**New-CsClientVersionConfiguration** コマンドレットはパイプライン入力を受け付けません。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration オブジェクトの新しいインスタンスを作成します。

## 関連項目

#### その他のリソース

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

