---
title: Export-CsConfiguration
TOCTitle: Export-CsConfiguration
ms:assetid: 7da7e133-e405-466c-a852-06a4fb678c59
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398627(v=OCS.15)
ms:contentKeyID: 48272643
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server のトポロジ、ポリシー、および構成設定をファイルにエクスポートします。また、アップグレード、ハードウェア障害、またはその他の問題のためにデータを消失してしまっても、このファイルを使用して、これらの情報を中央管理ストアに復元することができます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Export-CsConfiguration [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    Export-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 に示すコマンドは、Lync Server データを中央管理ストアから C:\\Config.zip という名前のファイルにエクスポートします。

    Export-CsConfiguration -FileName "C:\Config.zip"

## 解説

Lync Server サービスまたはサーバーの役割を実行するコンピューターが、割り当てられた役割で機能できるようにするためには、現在のトポロジ、現在の構成設定、および現在のポリシーのコピーを保持することが必要です。Lync Server には、情報を必要とする各コンピューターに、その情報を確実に渡す役割があります。

中央管理ストア のアップグレード時に、**Export-CsConfiguration** コマンドレットおよび **Import-CsConfiguration** コマンドレットを使用して、Lync Server のトポロジ、構成設定、およびポリシーをバックアップして復元します。**Export-CsConfiguration** コマンドレットを使用して、データを .ZIP ファイルにエクスポートできます。それから、**Import-CsConfiguration** コマンドレットを使用してその .ZIP ファイルを読み取り、トポロジ、構成設定、およびポリシーを 中央管理ストア に復元できます。その後、Lync Server のレプリケーション サービスにより、Lync Server サービスを実行している他のコンピューターに、復元された情報をレプリケートします。

境界ネットワークに存在するコンピューター (たとえば、エッジ サーバー) を最初に構成するときには、構成データのエクスポートおよびインポート機能も使用します。境界ネットワークのコンピューターを構成する場合には、まず、CsConfiguration コマンドレットを使用して手動レプリケーションを実行する必要があります。それから、**Export-CsConfiguration** コマンドレットを使用して構成データをエクスポートしてから、境界ネットワークのコンピューターにその .ZIP ファイルをコピーする必要があります。その後、**Import-CsConfiguration** コマンドレットと LocalStore パラメーターを使用してデータをインポートできます。この操作は一度だけ実行する必要があり、その後は、レプリケーションは自動的に実行されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Export-CsConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsConfiguration"}

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
<td><p><em>FileName</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p><strong>Export-CsConfiguration</strong> コマンドレットの実行時に作成される .ZIP ファイルへのパス。次に例を示します。-FileName &quot;C:\Config.zip&quot;。<strong>Export-CsConfiguration</strong> コマンドレットを呼び出すときは、FileName パラメーターまたは AsBytes パラメーターのどちらかを含める必要がありますが、両方を含める必要はありません。</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>トポロジ情報をバイト配列として戻します。戻されたデータは、<strong>Import-CsConfiguration</strong> コマンドレットで使用するため、変数に格納する必要があります。AsBytes と FileName の両方を同じコマンドで使用することはできません。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。Force パラメーターを True に設定するには、次の構文を使用します。</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア自体からではなくローカル コンピューターから、構成データを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Export-CsConfiguration** コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

AdBytes パラメーターを指定して **Export-CsConfiguration** コマンドレットを呼び出すと、バイト配列形式で構成情報が戻されます。

## 関連項目

#### その他のリソース

[Import-CsConfiguration](import-csconfiguration.md)

