---
title: Disable-CsComputer
TOCTitle: Disable-CsComputer
ms:assetid: e64128f1-2b53-4569-bf37-90cbbba01b36
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399023(v=OCS.15)
ms:contentKeyID: 48273999
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsComputer

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server を実行しているコンピューターから削除されたサービスまたはサーバーの役割を無効にします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Disable-CsComputer [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-Scorch <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドを実行すると、ローカル コンピューターが無効にされます。

    Disable-CsComputer 

## 例 2

例 2 に示すコマンドを実行しても、ローカル コンピューターが無効にされます。このコマンドを実行して、コンピューターを無効にする以外に、タスクの成功 (または失敗) に関する情報をファイル C:\\Logs\\Disable.html に記録します。このログ ファイルを作成するために、コマンドに Report パラメーターを追加し、情報を記録するログ ファイルへのパスを指定します。

    Disable-CsComputer -Report C:\Logs\Disable.html

## 解説

コンピューターからサービスまたはサーバーの役割を削除しても、Lync Server トポロジは自動的には更新されません。むしろ、変更内容がトポロジ内で完全に更新される前に、そうしたサービスまたは役割を無効にする必要があります。**Disable-CsComputer** コマンドレットにより、管理者はローカル コンピューターから削除されたサービスまたはサーバーの役割を無効にできます。

Scorch パラメーターを使用しない限り、**Disable-CsComputer** コマンドレットによって Lync Server ソフトウェアがアンインストールされることはありません。そのコンピューターがそれまで割り当てられていた役割を果たさなくなるだけです。

このコマンドレットを実行できるユーザー: **Disable-CsComputer** コマンドレットをローカル実行するには、ローカル管理者、およびドメインのメンバーになる必要があります。

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
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>ドメイン内のグローバル カタログ サーバーの完全修飾ドメイン名 (FQDN) です。使用中のドメインの中にアカウントが存在しているコンピューター上で <strong>Disable-CsComputer</strong> コマンドレットを実行する場合は、このパラメーターは必須ではありません。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>グローバル設定が保存されているドメイン コントローラーの FQDN です。グローバル設定が Active Directory ドメイン サービス 内のシステム コンテナーに保存されている場合は、このパラメーターでルート ドメイン コントローラーを指定する必要があります。グローバル設定が構成コンテナーに保存されている場合は、すべてのドメイン コントローラーが使用でき、このパラメーターを省略できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレット実行時に作成されるログ ファイルのファイル パスを指定できるようにします。次に例を示します。-Report &quot;C:\Logs\DisableComputer.html&quot; です。</p></td>
</tr>
<tr class="even">
<td><p><em>Scorch</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>ローカル コンピューターの Lync Server サービスおよびサーバーの役割をすべてアンインストールします。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Disable-CsComputer** コマンドレットはパイプライン入力を受け付けません。

## 戻り値の種類

なし。代わりに、**Disable-CsComputer** コマンドレットは Microsoft.Rtc.Management.Deploy.Internal.Machine オブジェクトのインスタンスを無効にします。

## 関連項目

#### その他のリソース

[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

