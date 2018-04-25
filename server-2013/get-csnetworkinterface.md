---
title: Get-CsNetworkInterface
TOCTitle: Get-CsNetworkInterface
ms:assetid: 06a5fedf-d87e-4469-9bd6-ad16c1f9a801
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398121(v=OCS.15)
ms:contentKeyID: 48271137
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterface

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server サービスまたはサーバーの役割を実行しているコンピューターで使用されているネットワーク インターフェイスに関する情報を戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsNetworkInterface [-Identity <NetworkInterfaceIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterface [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ComputerFqdn <Fqdn>]

## 例

## 例 1

例 1 では、組織で使用するために構成されている、すべてのネットワーク インターフェイスに関する情報が戻されます。

    Get-CsNetworkInterface

## 例 2

例 2 のコマンドを実行すると、単一のネットワーク インターフェイス (atl-cs-001.litwareinc.com.com/Primary/1 という Identity を持つインターフェイス) に関する情報が戻されます。

    Get-CsNetworkInterface -Identity atl-cs-001.litwareinc.com/Primary/1

## 例 3

例 3 では、ドメイン litwareinc.com に存在するすべてのネットワーク インターフェイスに関する情報が戻されます。このタスクを実行するには、フィルター値 "\*.litwareinc.com\*" を指定して Filter パラメーターを使用します。このフィルター値で、インターフェイスの返りデータを文字列値 "litwareinc.com" を含む Identity に制限します。

    Get-CsNetworkInterface -Filter "*.litwareinc.com*"

## 例 4

例 4 では、IP アドレス 192.168.0.240 用に構成されているすべてのネットワーク インターフェイスに関する情報が戻されます。これを行うために、コマンドでまず、パラメーターを指定せずに **Get-CsNetworkInterface** コマンドレットを呼び出します。これにより、組織で使用するために構成されているすべてのネットワーク インターフェイスのコレクションが戻されます。その後、このコレクションが **Where-Object** コマンドレットにパイプ処理されます。このコマンドレットは、IPAddress プロパティが 192.168.0.240 と等しいインターフェイスのみを選択します。

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -eq "192.168.0.240"}

## 例 5

例 5 のコマンドは、例 4 のコマンドの変化形です。ただし、この場合は、サブネット "192.168.0.\*" 用に構成されているすべてのネットワーク インターフェイスに関する情報が戻されます。これを行うには、すべてのネットワーク インターフェイスのコレクションを取得し、そのコレクションを **Where-Object** コマンドレットにパイプ処理して、IPAddress が文字列値 "192.168.0." で始まるインターフェイスのみ取得します。

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -like "192.168.0.*"}

## 例 6

例 6 では、外部アクセス用に構成されているすべてのネットワーク インターフェイスが戻されます。これを行うために、まず、パラメーターを指定せずに **Get-CsNetworkInterface** コマンドレットを呼び出します。これにより、現在使用されているすべてのネットワーク インターフェイスのコレクションが戻されます。このコレクションが **Where-Object** コマンドレットにパイプ処理され、Interface プロパティが External と等しい項目のみ取得されます。

    Get-CsNetworkInterface | Where-Object {$_.Interface -eq "External"}

## 解説

情報を別のコンピューターに転送するためには、これらのコンピューターで、ネットワーク インターフェイスとして、コンピューターとネットワーク間の接続が必要です。Lync Server サービスまたはサーバーの役割を実行しているコンピューターには、少なくとも 1 つのネットワーク インターフェイスが備えられている必要があります。ネットワーク インターフェイスがない場合は、他のコンピューターと通信することはできません。ただし、これらのコンピューターに複数のネットワーク インターフェイスが備えられている場合もあります。たとえば、エッジ サーバーには、内部ネットワークへの接続用のインターフェイスと、インターネットへの接続用の別のインターフェイスが備えられている場合があります。**Get-CsNetworkInterface** コマンドレットを実行すると、管理者は、Lync Server サービスまたはサーバーの役割を実行しているコンピューターで現在使用されている、ネットワーク インターフェイスに関する情報を戻すことができます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Get-CsNetworkInterface** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterface"}

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
<td><p><em>ComputerFqdn</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>ネットワーク インターフェイス情報が戻されるコンピューターの FQDN です。たとえば、コンピューター atl-cs-001.litwareinc.com (およびそのコンピューターのみ) のネットワーク インターフェイス情報を戻すには、次の構文を使用します。-ComputerFqdn atl-cs-001.litwareinc.com。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>戻されるネットワーク インターフェイスを 1 つまたは複数指定する際に、ワイルドカードを使用できます。たとえば、次の構文によって、Lync Server サービスまたはサーバーの役割を実行しているすべてのコンピューターで使用されている、プライマリ ネットワーク インターフェイスに関する情報が戻されます。-Filter &quot;*/Primary/*&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.NetworkInterfaceIdentity</p></td>
<td><p>戻されるネットワーク インターフェイスの一意の識別子です。ネットワーク インターフェイス Identity は、3 つの部分で構成されています。</p>
<p>コンピューター自体の完全修飾ドメイン名 (FQDN) (atl-cs-001.litwareinc.com など)。</p>
<p>ネットワーク インターフェイスの &quot;側&quot; (プライマリ、内部、外部、公衆交換電話網)。側は、ポートが使用されているトラフィックの種類を示します。</p>
<p>その特定の側のネットワーク インターフェイス番号。</p>
<p>次に例を示します。-Identity &quot;atl-cs-001.litwareinc.com/Primary/1&quot;。</p>
<p>Identity、ComputerFqdn、および Filter パラメーターは、単独で使用する必要があります。たとえば、ComputerFqdn と Identity の両方を使用してコマンドを実行することはできません。また、Identity を指定する際に、ワイルドカード文字を使用することはできません。ワイルドカードを使用するには、Filter パラメーターを使用します。</p>
<p>Identity、ComputerFqdn、または Filter パラメーターのいずれも使用しない場合、<strong>Get-CsNetworkInterface</strong> コマンドレットは、Lync Server サービスまたはサーバーの役割を実行しているコンピューターで現在使用されている、すべてのネットワーク インターフェイスに関する情報を戻します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsNetworkInterface** コマンドレットはパイプライン処理された入力を受け入れません。

## 戻り値の種類

**Get-CsNetworkInterface** コマンドレットを実行すると、Microsoft.Rtc.Management.Xds.DisplayNetworkInterface オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Get-CsComputer](get-cscomputer.md)

