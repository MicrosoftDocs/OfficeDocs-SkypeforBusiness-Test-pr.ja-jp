---
title: Set-CsConfigurationStoreLocation
TOCTitle: Set-CsConfigurationStoreLocation
ms:assetid: 1c69a872-8e78-4c78-ba27-f20f04dce59f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398258(v=OCS.15)
ms:contentKeyID: 48271435
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConfigurationStoreLocation

 

_**トピックの最終更新日:** 2015-03-09_

中央管理ストアの Active Directory サービス コントロール ポイントを設定します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsConfigurationStoreLocation -SqlServerFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-MirrorSqlInstanceName <String>] [-MirrorSqlServerFqdn <Fqdn>] [-Report <String>] [-SkipLookup <SwitchParameter>] [-SqlInstanceName <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 のコマンドは、Lync Server 中央管理ストア の Active Directory サービス コントロール ポイントを設定します。この例では、SCP は、コンピューター atl-sql-001.litwareinc.com と SQL Server インスタンス Rtc を指しています。

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc

## 例 2

例 2 のコマンドは、例 1 のコマンドの変化形です。このコマンドでも、Lync Server 中央管理ストア の Active Directory SCP を設定します。さらに、この処理の成功 (または失敗) に関する情報が C:\\Logs\\Store\_Location.html に記録されます。このログを生成するには、Report パラメーターの後にログ ファイルへの完全なパスを指定します。

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc -Report C:\Logs\Store_Location.html

## 解説

Active Directory ドメイン サービス では、サービス コントロール ポイント (SCP) を使用することで、コンピューターがサービスを見つけることができるようになっています。たとえば、Lync Server をインストールすると、サービス コントロール ポイントが作成されて、Lync Server データを保持するために使用される中央管理ストアの場所情報が割り当てられます。データベースに接続する必要があるコンピューターは、Active Directory に接続し、SCP に格納されている情報を使用することで、正しいコンピューターと SQL Server の正しいインスタンスを見つけることができます。

既に説明したように、Lync Server をインストールすると、中央管理ストア の SCP が自動的に作成されます。そのデータベースを別のコンピューターに移動する必要がある場合や、別の SQL Server インスタンスに移動する必要がある場合は、対応するサービス コントロール ポイントを更新する必要があります。**Set-CsConfigurationStoreLocation** コマンドレットを使用すると、このタスクを実行できます。このタスクを実行すると、**Set-CsConfigurationStoreLocation** コマンドレットによって Active Directory で SqlServer パラメーターによって指定されたコンピューターが検索されます。次に、保存場所が、そのコンピューターの FQDN に設定されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Set-CsConfigurationStoreLocation** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。

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
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>中央管理ストア がインストールされているコンピューターの完全修飾ドメイン名 (FQDN)。次に例を示します。-SqlServer atl-sql-001.litwareinc.com。</p></td>
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
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>グローバル設定が格納されているドメイン コントローラーの FQDN。グローバル設定が Active Directory のシステム コンテナーに格納されている場合は、このパラメーターでルート ドメイン コントローラーを指定する必要があります。グローバル設定が構成コンテナーに格納されている場合は、すべてのドメイン コントローラーが使用でき、このパラメーターを省略できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>MirrorSqlInstanceName</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>Lync Server ミラー データベースのテーブルとデータを含む SQL Server インスタンスの名前。次に例を示します。-SqlInstanceName &quot;rtc&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorSqlServerFqdn</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>中央管理ストアのミラー データベースがインストールされているコンピューターの完全修飾ドメイン名 (FQDN)。次に例を示します。-SqlServer atl-mirror-001.litwareinc.com。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレット実行時に作成されるログ ファイルのファイル パスを指定できるようにします。次に例を示します。-Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipLookup</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>このパラメーターを指定している場合、<strong>Set-CsConfigurationStoreLocation</strong> コマンドレットを実行しても、指定のコンピューターと指定の SQL Server インスタンスが利用できるかどうかは確認されません。代わりに、サービス コントロール ポイントが変更されるだけです。</p>
<p>このパラメーターを指定していない場合、SCP が変更される前に、指定のコンピューターと指定の SQL Server インスタンスの両方が利用できるようになっている必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>Lync Server のテーブルとデータを含む SQL Server インスタンスの名前。次に例を示します。-SqlInstanceName &quot;rtc&quot;。</p></td>
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

なし。**Set-CsConfigurationStoreLocation** コマンドレットはパイプライン処理された入力を受け入れません。

## 戻り値の種類

**Set-CsConfigurationStoreLocation** コマンドレットを実行しても、オブジェクトや値が戻されることはありません。

## 関連項目

#### その他のリソース

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)

