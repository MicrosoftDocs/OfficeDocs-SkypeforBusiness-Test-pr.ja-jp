---
title: Get-CsOnlineUser
TOCTitle: Get-CsOnlineUser
ms:assetid: 2bfafd70-a7d9-4308-a353-5ecf44249b53
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994026(v=OCS.15)
ms:contentKeyID: 52056565
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOnlineUser

 

_**トピックの最終更新日:** 2015-03-09_

Microsoft Lync Online に属するアカウントを持つユーザーに関する情報を戻します。このコマンドレットは、Skype for Business Online でのみ使用できます。

## 構文

    Get-CsOnlineUser [[-Identity] <UserIdParameter>] [-Filter <String>] [-LdapFilter <String>] [-OnOfficeCommunicationServer] [-OnLyncServer] [-UnAssignedUser] [-OU <OUIdParameter>] [-DomainController <Fqdn>] [-Credential <PSCredential>] [-ResultSize <Unlimited`1>] [-Verbose]

## 例

## 例 1

例 1 に示すコマンドは、オンライン ユーザーとして構成されているすべてのユーザーに関する情報を戻します。

    Get-CsOnlineUser

## 例 2

例 2 では、1 人のオンライン ユーザー (SIP アドレスが "sip: kenmyer@litwareinc.com" であるユーザー) に関する情報が戻されます。

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

## 例 3

例 3 に示すコマンドは、Lync Online で有効になっていても、レジストラー プールが現在割り当てられていないすべてのオンライン ユーザーに関する情報を戻します。

    Get-CsOnlineUser -UnassignedUser

## 例 4

例 4 では、Filter パラメーターを使用して、戻されるデータをユーザーごとのアーカイブ ポリシー RedmondArchiving が割り当てられているオンライン ユーザーに制限します。このために、フィルター値 {ArchivingPolicy -eq "RedmondArchiving"} を使用します。この構文は、戻されるデータが、ArchivingPolicy プロパティが "RedmondArchiving" と等しい (-eq) ユーザーに制限されます。

    Get-CsOnlineUser -Filter {ArchivingPolicy -eq "RedmondArchiving"}

## 例 5

例 5 では、Microsoft Exchange のアドレス一覧で非表示になるように構成されているユーザー アカウント (つまり、Active Directory の属性 msExchHideFromAddressLists が True である) のみに関する情報を戻します。このタスクを実行するために、Filter パラメーターとフィルター値 {HideFromAddressLists -eq $True} が指定されています。

    Get-CsOnlineUser -Filter {HideFromAddressLists -eq $True}

## 例 6

例 6 に示すコマンドは、TenantID が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントに割り当てられているすべてのオンライン ユーザーに関する情報を戻します。このタスクを実行するために、コマンドでは、Filter パラメーターとフィルター値 {TenantId –eq "bf19b7db-6960-41e5-a139-2aa373474354"} が指定されています。このフィルターにより、戻されるデータが、テナント "bf19b7db-6960-41e5-a139-2aa373474354" に割り当てられているオンライン ユーザーに制限されます。

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

## 解説

**Get-CsOnlineUser** コマンドレットは、Microsoft Lync Online に属するアカウントを持つユーザーに関する情報を戻します。戻される情報には、標準の Active Directory アカウント情報 (ユーザーの所属する部署、住所、電話番号など) と Lync Server 固有の情報が含まれます。つまり、**Get-CsOnlineUser** コマンドレットによって、ユーザーがエンタープライズ VoIP で有効になっているかどうか、ユーザーに割り当てられているユーザーごとのポリシー (存在する場合) などの情報が戻されます。

**Get-CsOnlineUser** コマンドレットには TenantId パラメーターがないことに注意してください。つまり、次のようなコマンドを使用して、戻されるデータを特定の Lync Online テナントがあるアカウントを持つユーザーに制限することはできません。

    Get-CsOnlineUser -TenantId "bf19b7db-6960-41e5-a139-2aa373474354"

ただし、複数の Lync Online テナントがある場合には、Filter パラメーターと次のようなコマンドを使用して、指定したテナントのユーザーを戻すことができます。

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

このコマンドにより、戻されるデータが、TenantId が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントに属するユーザー アカウントに制限されます。テナント ID が不明な場合は、次のコマンドを使用してテナント情報を戻すことができます。

    Get-CsTenant

ハイブリッド展開または "分割ドメイン" 展開 (つまり、Lync Online に属するアカウントを持つユーザーだけでなく、Lync Server の社内バージョンのアカウントを持つユーザーも存在する展開) がある場合には、**Get-CsOnlineUser** コマンドレットによって、Lync Online ユーザーに関する情報のみが戻されることに注意してください。ただし、[Get-CsUser](get-csuser.md) コマンドレットを使用すると、Lync Online のユーザーと Lync Server の社内バージョンのユーザーの両方に関する情報が戻されます。**Get-CsUser** コマンドレットによって戻されるデータから Lync Online のユーザーを除外する場合には、次のコマンドを使用します。

    Get-CsUser -Filter {TenantId -eq "00000000-0000-0000-0000-000000000000"}

定義上、Lync Server の社内バージョンに属するユーザーの TenantId は常に、00000000-0000-0000-0000-000000000000 になります。 Lync Online に属するユーザーの TenantId は、00000000-0000-0000-0000-000000000000 以外の値になります。

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
<th>必須</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>別の資格情報で <strong>Get-CsOnlineUser</strong> コマンドレットを実行できます。これは、Windows へのログオン時に使用したアカウントが、ユーザー オブジェクトの使用に必要な権限を持たない場合に、必要となる可能性があります。</p>
<p>Credential パラメーターを使用するには、まず、 <strong>Get-Credential</strong> コマンドレットを使用して、PSCredential オブジェクトを作成する必要があります。詳細については、 <strong>Get-Credential</strong> コマンドレットのヘルプ トピックを参照してください。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>指定したドメイン コントローラーに接続して、ユーザー情報を取得できます。特定のドメイン コントローラーに接続するには、DomainController パラメーターの後に、完全修飾ドメイン名 (FQDN) (たとえば、atl-cs-001.litwareinc.com) を追加します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>Lync Server 固有の属性をフィルター処理して、戻されるデータを制限することができます。たとえば、戻されるデータを、特定の音声ポリシーに割り当てられている (または割り当てられていない) ユーザーに制限できます。</p>
<p>Filter パラメーターは、Where-Object コマンドレットと同じ Windows PowerShell フィルター処理構文を使用します。たとえば、エンタープライズ VoIP が有効なユーザーのみを戻すフィルターは次のようになります。ここで、EnterpriseVoiceEnabled は Active Directory 属性を、-eq は比較演算子 (等号) を、$True (組み込みの Windows PowerShell 変数) はフィルター値を表します。</p>
<p>{EnterpriseVoiceEnabled -eq $True}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>取得するユーザー アカウントの Identity を指定します。ユーザーの Identity は、以下の 4 つの形式のうちの 1 つを使用して指定できます。1) ユーザーの SIP アドレス、2) ユーザーのユーザー プリンシパル名 (UPN)、3) ドメイン\ログオン形式 (たとえば、litwareinc\kenmyer) のユーザーのドメイン名とログオン名、および 4) ユーザーの Active Directory 表示名 (たとえば、Ken Myer)。ユーザー アカウントは、ユーザーの Active Directory 識別名を使用して参照することもできます。</p>
<p>表示名をユーザーの Identity として使用する場合は、アスタリスク (*) ワイルドカード文字を使用できます。たとえば、&quot;* Smith&quot; という Identity は、末尾が &quot; Smith&quot; という文字列値の表示名を持つすべてのユーザーを戻します。</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>一般的な Active Directory 属性 (つまり、 Lync Server 固有ではない属性) をフィルター処理することで、戻りデータを制限できます。たとえば、特定の部署に勤務していたり、指定したマネージャーや役職を持っていたりするユーザーのみに、返りデータを制限できます。</p>
<p>LdapFilter パラメーターは、フィルターの作成時に LDAP クエリ言語を使用します。たとえば、Redmond 市内で勤務しているユーザーだけを戻すフィルターは次のようになります。&quot;l=Redmond&quot; では、&quot;l&quot; (L の小文字) は Active Directory の属性 (ローカリティ)、&quot;=&quot; は比較演算子 (等しい)、&quot;Redmond&quot; はフィルター値をそれぞれ表します。</p></td>
</tr>
<tr class="even">
<td><p><em>OnLyncServer</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Lync Server に所属しているユーザーのコレクションが戻されます。このパラメーターを使用する場合、以前のバージョンのソフトウェアでアカウントを持つユーザーは戻されません。</p></td>
</tr>
<tr class="odd">
<td><p><em>OnOfficeCommunicationServer</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>以前のバージョンの Lync Server ( Microsoft Office Communications Server 2007 R2 など) に所属しているユーザーのコレクションが戻されます。このパラメーターを使用する場合、現在のバージョンのソフトウェアでアカウントを持つユーザーは戻されません。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>特定の組織単位 (OU) またはコンテナー内のユーザー アカウントに関する情報を戻すことができます。OU パラメーターにより、指定の OU およびそのすべての子 OU からデータが戻されます。たとえば、財務 OU に AccountsPayable と AccountsReceivable という 2 つの子 OU がある場合、これら 3 つの OU のデータがそれぞれ戻されます。</p>
<p>OU 指定時には、該当コンテナーの識別名 (DN) を使用します。次に例を示します。-OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;。Users コンテナーからユーザー アカウントを戻すには、次の構文を使用します。</p>
<p>-OU &quot;cn=Users,dc=litwareinc,dc=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>このコマンドレットによって戻されるレコード数を制限できます。たとえば (フォレスト内のユーザー数に関わらず) 7 ユーザーを戻すには、ResultSize パラメーターを追加してパラメーター値を 7 に設定します。必ずしも 7 ユーザーが戻されるわけではないことに注意してください。</p>
<p>結果サイズは、0 ～ 2147483647 の範囲の整数に設定できます。0 に設定すると、コマンドは実行されますが、データは戻りません。フォレスト内に 3 ユーザーしかいない場合は、ResultSize を 7 に設定しても、その 3 ユーザーが戻され、エラーなしでコマンドが完了します。</p></td>
</tr>
<tr class="even">
<td><p><em>UnassignedUser</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Lync Online で有効になっていても、レジストラー プールに現在割り当てられていないすべてのユーザーのコレクションを戻すことができます。レジストラー プールに割り当てられていない場合、ユーザーはログオンできません。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

**Get-CsOnlineUser** コマンドレットは、Microsoft.Rtc.Management.ADConnect.Schema.OCSADUser オブジェクトのパイプライン処理されたインスタンス、および有効なユーザー アカウント ID を表す文字列値 (たとえば、"sip:kenmyer@litwareinc.com") を受け入れます。

## 戻り値の種類

**Get-CsOnlineUser** コマンドレットは、Microsoft.Rtc.Management.ADConnect.Schema.ADOCOnlineUser オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Get-CsUser](get-csuser.md)

