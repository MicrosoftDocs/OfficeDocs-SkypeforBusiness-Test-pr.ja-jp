---
title: Get-CsComputer
TOCTitle: Get-CsComputer
ms:assetid: 493931a9-1670-4a76-abba-7d3c7723d2e1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425959(v=OCS.15)
ms:contentKeyID: 48271982
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsComputer

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server インフラストラクチャ内でサービスの役割を実行するコンピューターに関する情報を戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsComputer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsComputer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Local <SwitchParameter>] [-Pool <String>]

## 例

## 例 1

例 1 では、**Get-CsComputer** コマンドレットを使用して、Lync Server インフラストラクチャ内でサービスの役割を実行するすべてのコンピューターに関する情報を戻します。

    Get-CsComputer

## 例 2

例 2 に示すコマンドは、Filter パラメーターを使用して、litwareinc.com ドメインの一部となっているサービスの役割のコンピューターのみを戻します。ワイルドカード文字列 \*.litwareinc.com により、戻される情報を FQDN が ".litwareinc.com" で終わるコンピューターに制限しています。

    Get-CsComputer -Filter "*.litwareinc.com"

## 例 3

例 3 では、Identity パラメーターを使用して、戻されるデータを FQDN が atl-cs-001.litwareinc.com である 1 台のコンピューターに制限します。

    Get-CsComputer -Identity "atl-cs-001.litwareinc.com"

## 例 4

例 4 では、Pool パラメーターを使用して、atl-cs-001.litwareinc.com プールで見つかったすべてのコンピューターに関する情報を戻します。

    Get-CsComputer -Pool "atl-cs-001.litwareinc.com"

## 解説

**Get-CsComputer** コマンドレットを使用すると、Lync Server のサービスまたはサーバーの役割を実行しているコンピューターをすばやく識別できます。パラメーターを何も指定せずに **Get-CsComputer** コマンドレットを呼び出すと、Lync Server のサービスまたはサーバーの役割を実行しているすべてのコンピューターのコレクションが戻されます。このコレクションには、各コンピューターの ID、プール名、および完全修飾ドメイン名 (FQDN) が含まれています。または、Identity、Filter、Pool などのオプションのパラメーターを使用して、戻されるデータを単一のコンピューター、またはコンピューターのセットに制限できます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Get-CsComputer** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。

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
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>戻すコンピューター (複数可) の ID を指定するときに、ワイルドカード文字を使用できます。たとえば、このコマンドでは、文字列値 &quot;atl-&quot; で始まる ID を持つすべてのコンピューターに関する情報を戻しています。-Filter &quot;atl-*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>戻されるコンピューターの FQDN です。次に例を示します。-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p>このパラメーターを指定しないと、Lync Server が実行されているすべてのコンピューターが戻されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Local</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>このパラメーターを指定すると、ローカル コンピューターの情報のみが戻されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>Lync Server プールの FQDN です。このパラメーターを使用すると、指定したプール内のすべてのコンピューターに関する情報が戻されます。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsComputer** コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

**Get-CsComputer** コマンドレットを実行すると、Microsoft.Rtc.Management.Deploy.Internal.Machine オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

