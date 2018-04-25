---
title: Remove-CsConfigurationStoreLocation
TOCTitle: Remove-CsConfigurationStoreLocation
ms:assetid: 141be225-c6e4-4377-913b-ba61528929d4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398214(v=OCS.15)
ms:contentKeyID: 48271341
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConfigurationStoreLocation

 

_**トピックの最終更新日:** 2015-03-09_

中央管理ストアの Active Directory サービス コントロール ポイントを削除します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsConfigurationStoreLocation [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 のコマンドは、中央管理ストア の Active Directory サービス コントロール ポイントを削除します。この SCP を復元 (または、新しい SCP を作成) するには、**Set-CsConfigurationStoreLocation** コマンドレットを実行する必要があります。

    Remove-CsConfigurationStoreLocation

## 例 2

例 2 も、中央管理ストア の Active Directory サービス コントロール ポイントを削除します。SCP を削除する以外に、このコマンドを実行して、処理の成功 (または失敗) に関する情報をログ ファイル C:\\Logs\\Store\_Location.html に記録します。このログ ファイルを作成するために、コマンドで Report パラメーターを使用し、パラメーターの後に情報を記録するログ ファイルへのパスを指定します。このファイルが既に存在する場合、コマンドを実行すると内容が上書きされます。ファイルが存在しない場合、コマンドを実行するとファイルが作成されます。

    Remove-CsConfigurationStoreLocation -Report C:\Logs\Store_Location.html

## 解説

Active Directory ドメイン サービス では、サービス コントロール ポイント (SCP) を使用することで、コンピューターがサービスを見つけることができるようになっています。たとえば、Lync Server をインストールすると、SCP が作成されて、Lync Server データを保持するために使用される中央管理ストアの場所情報が割り当てられます。データベースに接続する必要があるコンピューターは、Active Directory に接続し、SCP に格納されている情報を使用することで、正しいコンピューターと SQL Server の正しいインスタンスを見つけることができます。

既に説明したように、Lync Server をインストールすると、中央管理ストア の SCP が自動的に作成されます。通常は、その SCP を削除する必要はありません。削除すると、コンピューターでデータベースを見つけることができなくなります。ただし、SCP を削除することが必要になる場合があります (問題のトラブルシューティングを行う場合など)。その場合には、**Remove-CsConfigurationStoreLocation** コマンドレットを使用します。SCP を削除した後で、**Set-CsConfigurationStoreLocation** コマンドレットを使用して SCP を再作成 (または新しいサービス コントロール ポイントを作成) することができます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Remove-CsConfigurationStoreLocation** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。

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
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>グローバル設定が格納されているドメイン コントローラーの完全修飾ドメイン名 (FQDN) です。グローバル設定が Active Directory のシステム コンテナーに格納されている場合は、このパラメーターでルート ドメイン コントローラーを指定する必要があります。グローバル設定が構成コンテナーに格納されている場合は、すべてのドメイン コントローラーが使用でき、このパラメーターを省略できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレット実行時に作成されるログ ファイルのファイル パスを指定できるようにします。次に例を示します。-Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
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

なし。**Remove-CsConfigurationStoreLocation** コマンドレットはパイプライン処理された入力を受け入れません。

## 戻り値の種類

**Remove-CsConfigurationStoreLocation** コマンドレットを実行しても、オブジェクトや値が戻されることはありません。

## 関連項目

#### その他のリソース

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

