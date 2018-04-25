---
title: Import-CsConfiguration
TOCTitle: Import-CsConfiguration
ms:assetid: 9a9c27f2-313c-4327-aeed-c47852a831ec
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398800(v=OCS.15)
ms:contentKeyID: 48272996
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server のトポロジ、ポリシー、および構成設定を、中央管理ストアまたはローカル コンピューターのどちらかにインポートします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Import-CsConfiguration -ByteInput <Byte[]> <COMMON PARAMETERS>

    Import-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 に示すコマンドは、現在のトポロジ、構成設定、およびポリシーを、C:\\Config.zip というファイルから中央管理ストアへインポートします。

    Import-CsConfiguration -FileName "C:\Config.zip"

## 例 2

例 2 は、境界ネットワークに配置されるコンピューターに対する、最初のデータ レプリケーションの方法を示しています。この例では、Config.zip というファイルに構成データをエクスポートし、境界ネットワークに配置されたコンピューターの C:\\ フォルダーへこのファイルをコピーします。次に、Import-CsConfiguration を使って、そのデータをインポートします。LocalStore パラメーターを指定することで、データは 中央管理ストア ではなく、ローカル コンピューターへインポートされます。

    Import-CsConfiguration -FileName "C:\Config.zip" -LocalStore

## 例 3

例 3 に示す 2 つのコマンドは、現在のトポロジ、構成設定、およびポリシーをエクスポートして、そのデータをローカル コンピューターへインポートします。ただし、すべての処理を .ZIP ファイルを使わずに行います。これを行うため、最初のコマンドでは、**Export-CsConfiguration** コマンドレットと AsBytes パラメーターを使用し、現在のトポロジ、構成設定、およびポリシーをバイト配列としてエクスポートします。このバイト配列は、$x という変数に格納されます。2 番目のコマンドでは、**Import-CsConfiguration** コマンドレットと ByteInput パラメーターを使用して、$x に格納された情報をインポートします。LocalStore パラメーターにより、データは 中央管理ストア ではなく、ローカル コンピューターへインポートされます。結果的に、中央管理ストア からローカル コンピューターへデータがコピーされます。

    $x = Export-CsConfiguration -AsBytes
    Import-CsConfiguration -ByteInput $x -LocalStore

## 解説

Lync Server サービスまたはサーバーの役割を実行するコンピューターが、それぞれに指定された役割で機能するには、現在のトポロジ、現在の構成設定、現在のポリシーなどのコピーが必要です。Lync Server は、この情報が各コンピューターの必要に応じて転送されるようにする役割を担います。

Import-CsConfiguration コマンドレットおよび Export-CsConfiguration コマンドレットは、中央管理ストア をアップグレードする際に、Lync Server のトポロジ、構成設定、ポリシーをバックアップおよび復元するために使用します。**Export-CsConfiguration** コマンドレットでは、データを .ZIP ファイルでエクスポートできます。そして、**Import-CsConfiguration** コマンドレットを使ってこの .ZIP ファイルを読み込み、トポロジ、設定、およびポリシーを 中央管理ストア へ復元します。復元された情報は、その後、Lync Server のレプリケーション サービスによって、サービスを実行するコンピューターへレプリケートされます。

構成データをエクスポートおよびインポートする機能は、境界ネットワーク内に配置されるコンピューター (エッジ サーバー など) の初期構成の際にも使用されます。境界ネットワーク内に配置されるコンピューターを構成する場合は、まず CsConfiguration コマンドレットを使って、レプリケーションを手動で実行する必要があります。その際は、**Export-CsConfiguration** コマンドレットを使用して構成データをエクスポートし、その .ZIP ファイルを境界ネットワーク内のコンピューターへコピーする必要があります。その後、そのデータを **Import-CsConfiguration** コマンドレットと LocalStore パラメーターを使用してインポートすることができます。この処理が必要なのは 1 回限りです。その後は、レプリケーションは自動で実行されます。

このコマンドレットを実行できるユーザー: 既定では、**Import-CsConfiguration** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットを実行するには、RTCUniversalServerAdmins のメンバーであることに加えて、ローカル管理者であるか、ローカル構成レプリケーター アクセス許可が必要です。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsConfiguration"}

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
<td><p><em>ByteInput</em></p></td>
<td><p>必須かどうか</p></td>
<td><p>System.Byte[]</p></td>
<td><p>変数に格納されたバイト配列からトポロジ情報を読み取ります。このバイト配列は、<strong>Export-CsConfiguration</strong> コマンドレットの呼び出し時に ByteInput パラメーターを指定すると作成されます。</p>
<p>ByteInput パラメーターと FileName パラメーターを同じコマンドで両方使用することはできません。</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>Export-CsConfiguration により作成された .ZIP ファイルへのパスです。次に例を示します。-FileName &quot;C:\Config.zip&quot;。<strong>Import-CsConfiguration</strong> コマンドレットを呼び出す際は、FileName パラメーターか ByteInput パラメーターのどちらかを指定する必要がありますが、両方指定することはできません。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する、致命的ではないエラーに対するメッセージを表示しないようにします。Force パラメーターを True に設定するには、次の構文を使用します。</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>構成データを、中央管理ストア ではなくローカル コンピューターへコピーします。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Import-CsConfiguration** コマンドレットは、パイプ処理による入力を受け入れません。

## 戻り値の種類

**Import-CsConfiguration** コマンドレットは、値またはオブジェクトを戻しません。

## 関連項目

#### その他のリソース

[Export-CsConfiguration](export-csconfiguration.md)

