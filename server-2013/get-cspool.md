---
title: Get-CsPool
TOCTitle: Get-CsPool
ms:assetid: e0911c68-9a0a-461a-88d6-c610c6cd996c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398992(v=OCS.15)
ms:contentKeyID: 48273892
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPool

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server の展開で使用されるプールに関する情報を戻します。プールはサイト内のコンピューターのコレクションで、これらのコンピューターはすべて、同じ Lync Server サービス群を実行します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsPool [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPool [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Site <String>]

## 例

## 例 1

例 1 では、Lync Server の展開で見つかったすべてのプールを戻します。

    Get-CsPool

## 例 2

例 2 では、各プールの中で見つかったコンピューターに関する詳細情報が表示されます。これを実行するには、**Get-CsPool** コマンドレットを呼び出し、次に戻されたデータを **Select-Object** コマンドレットにパイプ処理します。ExpandProperty パラメーターを使用して、Computers プロパティの値を "展開" します。Computers プロパティは、プール内にある各コンピューターを表すオブジェクトの配列です。Computers プロパティを展開すると、それらのコンピューターのそれぞれに関する詳細情報が戻ります。

    Get-CsPool | Select-Object -ExpandProperty Computers

## 例 3

例 3 では、Identity パラメーターを使用して、返されるデータを、atl-cs-001.litwareinc.com という ID を持つプールに限定しています。

    Get-CsPool -Identity atl-cs-001.litwareinc.com

## 例 4

例 4 では、Redmond サイトで見つかったすべてのプールを戻します。これを実行するには、コマンドでは Site パラメーターを使用します。パラメーター値 "Redmond" は、戻りデータを、Site プロパティが Redmond に等しいプールのみに制限します。

    Get-CsPool -Site "Redmond"

## 例 5

例 5 のコマンドを実行すると、どの Lync Server サービスもインストールされていないすべてのプールのコレクションが戻されます。このタスクを実行するには、最初にパラメーターなしで **Get-CsPool** コマンドレットを呼び出します。この結果、組織内で現在使用されているすべてのプールのコレクションが戻されます。次に、このコレクションが **Where-Object** コマンドレットにパイプ処理されます。このコマンドレットでは、Services.Count プロパティ が 0 に等しいすべてのプールを選択します。Count が 0 に等しい場合は、どの Lync Server サービスもそのプールで構成されていないことを意味します。

    Get-CsPool | Where-Object {$_.Services.Count -eq 0}

## 解説

Lync Server におけるプールとは、同じサービス群を実行している、同一サイト内の 1 台以上のコンピューターです。たとえば、1 台のサーバーが仲介サーバー サービスを Redmond サイトで実行している場合は、この 1 台のコンピューターから成る仲介サーバー プールが存在することになります。2 台のコンピューターが仲介サーバーを Redmond サイトで実行している場合は、2 台のコンピューターから成る仲介サーバー プールが存在することになります。組織で使用されているプールの数は、所有しているサーバーの数と、それらのサーバーによって実行されているさまざまなサービスによって決まります。

**Get-CsPool** コマンドレットを使用すると、各プールで実行されているサービスに関する情報を含め、組織内で使用されている各プールに関する情報を取得できます。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが **Get-CsPool** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPool"}

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
<td><p>戻そうとするプールの Identity を指定するときに、ワイルドカードを使用できるようにします。たとえば、次の構文は、末尾が &quot;.fabrikam.com&quot; という文字列値の Identity を持つすべてのプールを返します。-Filter &quot;*.fabrikam.com&quot;。</p>
<p>Filter パラメーターと Identity パラメーターは、同じコマンドで同時に使用できないことに注意してください。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>戻すプールの完全修飾ドメイン名 (FQDN) です。次に例を示します。-Identity atl-cs-001.litwareinc.com。</p>
<p>このパラメーターを指定しないと、組織内にあるすべてのプールが戻されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Site</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>指定したサイトで見つかったすべてのプールを戻します。該当するサイトは、サイトの Identity (たとえば、site:Redmond) ではなく、サイトの表示名 (たとえば、Redmond) を使用して参照する必要があります。次に例を示します。-Site &quot;Redmond&quot;。次のコマンドを実行して、サイトの表示名を取得できます。</p>
<p>Get-CsSite | Select-Object Identity, DisplayName</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsPool** コマンドレットはパイプライン入力を受け付けません。

## 戻り値の種類

**Get-CsPool** コマンドレットを実行すると、Microsoft.Rtc.Management.Deploy.Internal.Cluster オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Get-CsSite](get-cssite.md)  
[Get-CsTopology](get-cstopology.md)

