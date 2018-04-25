---
title: Get-CsConfigurationStoreLocation
TOCTitle: Get-CsConfigurationStoreLocation
ms:assetid: abfda147-02fa-46a5-a988-d83daf4cc455
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412814(v=OCS.15)
ms:contentKeyID: 48273243
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConfigurationStoreLocation

 

_**トピックの最終更新日:** 2015-03-09_

中央管理ストアに対する Active Directory サービス コントロール ポイントの場所に関するレポートを戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsConfigurationStoreLocation [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## 例

## 例 1

例 1 に示すコマンドは、中央管理ストア をホストしているコンピューター (またはプール) への SQL Server のパスを戻します。

    Get-CsConfigurationStoreLocation

## 例 2

例 2 は、例 1 に示したコマンドの変化形です。ただし、この例では Report パラメーターを指定し、**Get-CsConfigurationStoreLocation** コマンドレットを実行したときに生成されるレポートのパスを指定しています。

    Get-CsConfigurationStoreLocation -Report "C:\Logs\ConfigurationStore.html"

## 解説

Active Directory ドメイン サービス では、サービス コントロール ポイント (SCP) を使用することで、コンピューターがサービスを見つけることができるようになっています。たとえば、Lync Server をインストールする際にサービス コントロール ポイントが作成され、Lync Server のデータの保持に使用される中央管理ストアの場所の情報が提供されます。データベースにアクセスする必要があるコンピューターは、Active Directory に接続して SCP に格納されている情報を使用することで、正しいコンピューターと正しい SQL Server インスタンスを見つけることができます。

**Get-CsConfigurationStoreLocation** コマンドレットでは、中央管理ストア を実行しているコンピューターへの SQL Server のパス (atl-sql-001.litwareinc.com/rtc など) に関するレポートを戻すことができます。

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
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>グローバル設定が格納されているドメイン コントローラーの完全修飾ドメイン名 (FQDN) です。グローバル設定が Active Directory システム コンテナーに格納されている場合は、このパラメーターでルート ドメイン コントローラーを指定する必要があります。グローバル設定が構成コンテナーに保存されている場合は、すべてのドメイン コントローラーが使用でき、このパラメーターを省略できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレット実行時に作成されるログ ファイルのファイル パスを指定できるようにします。次に例を示します。-Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsConfigurationStoreLocation** コマンドレットは、パイプ処理による入力を受け入れません。

## 戻り値の種類

文字列。**Get-CsConfigurationStoreLocation** コマンドレットは、構成ストアの場所に関するレポートを戻します。

## 関連項目

#### その他のリソース

[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

