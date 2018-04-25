---
title: Get-CsCommonAreaPhone
TOCTitle: Get-CsCommonAreaPhone
ms:assetid: bfb7927b-49a7-4637-a9ff-fd68897efb45
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412934(v=OCS.15)
ms:contentKeyID: 48273437
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCommonAreaPhone

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server を使用して管理されている共通領域電話に関する情報を戻します。共通領域電話は、建物のロビーや従業員休憩室のほか、多数の異なる人々が、多数の異なるユーザー宛てに電話を使用する可能性のある場所に置かれる電話です。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsCommonAreaPhone [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## 例

## 例 1

例 1 に示すコマンドを実行すると、組織で使用するように構成されている、すべての共通領域電話に関する情報が戻されます。これを行うには、パラメーターを指定せずに **Get-CsCommonAreaPhone** コマンドレットを呼び出します。

    Get-CsCommonAreaPhone

## 例 2

例 2 では、"Building 14 Lobby" という Active Directory 表示名を持つ共通領域電話が戻されます。このタスクを実行するには、Filter パラメーターとフィルター値 {DisplayName -eq "Building 14 Lobby"} を指定します。このフィルター値は戻されるオブジェクトを DisplayName プロパティが "Building 14 Lobby" と等しい共通領域電話に制限します。

    Get-CsCommonAreaPhone -Filter {DisplayName -eq "Building 14 Lobby"}

## 例 3

例 3 では、Active Directory 表示名が "Building 14" という文字列で始まる、すべての共通領域電話が戻されます。これを行うため、Filter パラメーターとフィルター値 {DisplayName -like "Building 14\*"} を指定して、**Get-CsCommonAreaPhone** コマンドレットを呼び出します。このフィルター値は、-like 演算子と "Building 14\*" というワイルドカード文字列を使用して、戻されるデータを DisplayName プロパティが "Building 14" で始まる電話 ("Building 14 Lobby"、"Building 14 Cafeteria" など) に制限しています。

    Get-CsCommonAreaPhone  -Filter {DisplayName -like "Building 14*"}

## 例 4

例 4 では、次の共通領域電話が 1 つ戻されます。"tel:+14255551234" と等しい LineUri プロパティを持つ電話。LineUris は一意である必要があるため、このコマンドによって複数の項目が戻されることはありません。

    Get-CsCommonAreaPhone  -Filter {LineUri -eq "tel:+14255551234"}

## 例 5

例 5 に示すコマンドを実行すると、ダイヤル プランが割り当てられていない、すべての共通領域電話に関する情報が戻されます。これを行うために、Filter パラメーターとフィルター値 {DialPlan -eq $Null} を使用しています。これにより、戻されるデータが DialPlan プロパティが null 値に等しい電話に制限されます。共通領域電話に明示的にダイヤル プランが割り当てられていない場合、グローバル ダイヤル プランか、存在する場合はサイトに割り当てられているダイヤル プランが自動的に使用されます。

    Get-CsCommonAreaPhone -Filter {DialPlan -eq $Null}

## 例 6

例 6 では、Active Directory ドメイン サービス の Telecommunications OU 内に連絡先オブジェクトを持つ、すべての共通領域電話のコレクションが戻されます。これを行うため、OU パラメーターを指定して **Get-CsCommonAreaPhone** コマンドレットを呼び出します。パラメーター値は、戻されるオブジェクトを識別名が ou=Telecommunications,dc=litwareinc,dc=com の OU 内に連絡先オブジェクトがある電話に制限しています。

    Get-CsCommonAreaPhone -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## 解説

共通領域電話は個々のユーザーに割り当てられていない IP 電話です。共通領域電話は、通常、個人のオフィスにあるのではなく、建物のロビー、カフェテリア、従業員休憩室、会議室のほか、多数の人が集まる可能性のある場所に置かれています。このことは、管理者にとって管理上の課題となります。Lync Server における電話の使用は、通常、個々のユーザーに割り当てられる音声ポリシーとダイヤル プランを使用して管理されるからです。共通領域電話には、割り当てられる個々のユーザーがありません。

この課題の解決策は、すべての共通領域電話に対して Active Directory の連絡先オブジェクトを作成することです (この連絡先オブジェクトは、**New-CsCommonAreaPhone** コマンドレットを使用することで作成できます)。ユーザー アカウントと同様、この連絡先オブジェクトはポリシーとボイス計画に割り当てることができます。これにより、共通領域電話が個々のユーザーに関連付けられていない場合でも、これらの電話に対する管理機能を保持することができます。たとえば、ユーザーが共通領域電話からの通話を転送または保留できないようにする場合、通話の転送および通話の保留を禁止する音声ポリシーを作成してから、そのポリシーを共通領域電話 (より正確には、共通領域電話を表す連絡先オブジェクト) に割り当てます。たとえば次のコマンドでは、音声ポリシー CommonAreaPhoneVoicePolicy をすべての共通領域電話に割り当てます。

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

**Get-CsCommonAreaPhone** コマンドレットを使用すると、組織で使用するように構成された共通領域電話に関する情報を取得できます。パラメーターを指定せずに **Get-CsCommonAreaPhone** コマンドレットを呼び出すと、このコマンドによって、すべての共通領域電話に関する情報が戻されます。省略可能なパラメーターを指定すると、異なる方法で情報をフィルター処理できます。たとえば、指定した組織単位 (OU) 内の連絡先オブジェクトを持つすべての共通領域電話や、指定した建物にあるすべての連絡先オブジェクトを戻せます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Get-CsCommonAreaPhone** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins、RTCUniversalReadOnlyAdmins。特定のサイトや特定の Active Directory OU に対してこのコマンドレットを実行する許可は、**Grant-CsOUPermission** コマンドレットを使用すると割り当てられます。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCommonAreaPhone"}

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
<td><p><em>Credential</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>別の資格情報で <strong>Get-CsCommonAreaPhone</strong> コマンドレットを実行できます。これは、Windows へのログオン時に使用したアカウントが、連絡先オブジェクトの使用に必要な権限を持たない場合に、必要となる可能性があります。</p>
<p>Credential パラメーターを使用するには、まず、<strong>Get-Credential</strong> コマンドレットを使用して、PSCredential オブジェクトを作成する必要があります。詳細については、<strong>Get-Credential</strong> コマンドレットのヘルプ トピックを参照してください。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>指定したドメイン コントローラーに接続して、連絡先情報を取得できます。特定のドメイン コントローラーに接続するには、DomainController パラメーターの後に、そのコンピューターの完全修飾ドメイン名 (FQDN) (たとえば、atl-cs-001.litwareinc.com) を追加します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>Lync Server 固有の属性をフィルター処理することで、戻されるデータを制限できます。たとえば、特定の音声ポリシーに割り当てられている (または割り当てられていない) 共通領域電話の連絡先オブジェクトに戻されるデータを制限できます。</p>
<p>Filter パラメーターは、<strong>Where-Object</strong> コマンドレットと同じ Windows PowerShell フィルター処理構文を使用します。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>共通領域電話の一意の識別子です。共通領域電話は、関連付けられている連絡先オブジェクトの Active Directory 識別名 (DN) を使用して識別されます。既定では、共通領域電話はグローバル一意識別子 (GUID) を共通名として使用します。つまり、これらの電話の Identity は、通常、以下のようになっています。CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>一般的な Active Directory 属性 (つまり、Lync Server 固有ではない属性) をフィルター処理することで、戻されるデータを制限できます。たとえば、特定の部門に割り当てられている連絡先オブジェクトや、特定の建物にある連絡先オブジェクトに、戻されるデータを制限できます。</p>
<p>LdapFilter パラメーターは、フィルターの作成時に LDAP クエリ言語を使用します。たとえば、Redmond 市にある共通領域電話を表す連絡先オブジェクトだけを戻すフィルターは、次のようになります。</p>
<p>-LDAPFilter &quot;l=Redmond&quot;</p>
<p>このフィルターでは、&quot;l&quot; (小文字の L) は Active Directory の属性 (ローカリティ)、&quot;=&quot; は比較演算子 (等しい)、&quot;Redmond&quot; はフィルター値をそれぞれ表します。</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>特定の Active Directory 組織単位 (OU) の連絡先オブジェクトを戻すことができます。OU パラメーターにより、指定の OU およびそのすべての子 OU からデータが戻されます。たとえば、財務 OU に AccountsPayable と AccountsReceivable という 2 つの子 OU がある場合、共通領域電話の情報はこれらの OU それぞれから戻されます。</p>
<p>OU 指定時には、該当コンテナーの識別名を使用します。次に例を示します。-OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>このコマンドによって戻されるレコード数を制限できます。たとえば、(フォレスト内にいくつの共通領域電話があるかに関係なく) 7 つの共通領域電話のみを戻す場合は、ResultSize パラメーターを指定して、パラメーターの値を 7 に設定します。どの 7 つの電話を戻すかは指定できないので注意してください。フォレスト内に共通領域電話が 3 台しかない場合は、ResultSize を 7 に設定しても、その 3 台の電話が戻され、エラーなしてコマンドが完了します。</p>
<p>結果サイズは、0 ～ 2147483647 の範囲の整数に設定できます。0 に設定すると、コマンドは実行されますが、データは戻りません。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

文字列。**Get-CsCommonAreaPhone** コマンドレットは、共通領域電話の Identity を表す、パイプライン処理された文字列値を受け入れます。

## 戻り値の種類

**Get-CsCommonAreaPhone** コマンドレットを実行すると、Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

