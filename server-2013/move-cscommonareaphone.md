---
title: Move-CsCommonAreaPhone
TOCTitle: Move-CsCommonAreaPhone
ms:assetid: af5f832c-1be9-4495-ba1a-c10ca50d7b29
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412837(v=OCS.15)
ms:contentKeyID: 48273276
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsCommonAreaPhone

 

_**トピックの最終更新日:** 2015-04-02_

1 台または複数の共通領域電話を新しいレジストラー プールに移動します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Move-CsCommonAreaPhone -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドを実行すると、CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com to the Registrar pool atl-cs-001.litwareinc.com という Identity を持つ共通領域電話が移動されます。

    Move-CsCommonAreaPhone -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -Target atl-cs-001.litwareinc.com

## 例 2

例 2 では、"Building 31 Cafeteria" という Active Directory 表示名を持つ共通領域電話が、atl-cs-001.litwareinc.com というレジストラー プールに移動されます。これを実行するには、最初にパラメーターなしで **Get-CsCommonAreaPhone** コマンドレットを呼び出します。この結果、組織で現在使用されているすべての共通領域電話のコレクションが戻されます。次にこのコレクションが **Where-Object** コマンドレットにパイプ処理され、DisplayName 属性が "Building 31 Cafeteria" と等しい電話のみが選び出されます。続いてこのフィルター処理されたコレクションが **Move-CsCommonAreaPhone** コマンドレットにパイプ処理され、コレクション内の各電話が atl-cs-001.litwareinc.com に移動されます。

    Get-CsCommonAreaPhone | Where-Object {$_.DisplayName -eq "Building 31 Cafeteria"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## 例 3

例 3 では、dublin-cs-001.litwareinc.com というレジストラー プールに現在所属しているすべての共通領域電話が、atl-cs-001.litwareinc.com というレジストラー プールに移動されます。このタスクを実行するには、まず、このコマンドはパラメーターを指定せずに **Get-CsCommonAreaPhone** コマンドレットを呼び出します。これにより、組織で使用するように設定されているすべての共通領域電話のコレクションが戻されます。次にこのコレクションが **Where-Object** コマンドレットにパイプ処理され、RegistrarPool が dublin-cs-001.litwareinc.com に等しいすべての共通領域電話が選び出されます。続いてこのコレクションが **Move-CsCommonAreaPhone** コマンドレットにパイプ処理され、コレクション内の各電話が atl-cs-001.litwareinc.com という新しいレジストラー プールに移動されます。

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## 例 4

例 4 は、例 3 に示したコマンドの変化形です。ただし、この例では、共通領域電話が新しいレジストラー プールに移動されるだけでなく、ユーザーごとの新しい音声ポリシーが割り当てられます。これを実行するには、**Move-CsCommonAreaPhone** コマンドレットの呼び出し時に PassThru パラメーターを指定しています。これは、パイプラインを介して共通領域電話オブジェクトを渡すために必要です (既定では、**Move-CsCommonAreaPhone** コマンドレットはパイプラインを介してオブジェクトを渡しません)。電話の移動後、電話オブジェクトが **Grant-CsVoicePolicy** コマンドレットにパイプ処理され、AtlantaVoicePolicy という音声ポリシーが新しく移動された電話ごとに割り当てられます。

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com -PassThru | Grant-CsVoicePolicy -PolicyName AtlantaVoicePolicy

## 解説

共通領域電話は個々のユーザーに割り当てられていない IP 電話です。共通領域電話は、通常、個人のオフィスにあるのではなく、建物のロビー、カフェテリア、従業員休憩室、会議室のほか、多数の人が集まる可能性のある場所に置かれています。このことは、管理者にとって管理上の課題となります。Lync Server における電話の使用は、通常、個々のユーザーに割り当てられる音声ポリシーとダイヤル プランを使用して管理されるからです。共通領域電話には、割り当てられる個々のユーザーがありません。

この課題の解決策は、すべての共通領域電話に対して Active Directory の連絡先オブジェクトを作成することです (この連絡先オブジェクトは、**New-CsCommonAreaPhone** コマンドレットを使用することで作成できます)。ユーザー アカウントと同様、この連絡先オブジェクトはポリシーとボイス計画に割り当てることができます。これにより、共通領域電話が個々のユーザーに関連付けられていない場合でも、これらの電話に対する管理機能を保持することができます。たとえば、ユーザーが共通領域電話からの通話を転送または保留できないようにする場合、通話の転送および通話の保留を禁止する音声ポリシーを作成してから、そのポリシーを共通領域電話 (より正確には、共通領域電話を表す連絡先オブジェクト) に割り当てます。

**Move-CsCommonAreaPhone** コマンドレットを使用すると、既存の共通領域電話を新しいレジストラー プールに移動できます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Move-CsCommonAreaPhone** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins。特定のサイトや特定の Active Directory 組織単位 (OU) に対してこのコマンドレットを実行する許可は、**Grant-CsOUPermission** コマンドレットを使用すると割り当てられます。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsCommonAreaPhone"}

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
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>共通領域電話の一意の識別子。共通領域電話は、関連付けられている連絡先オブジェクトの Active Directory 識別名を使用して識別されます。既定では、共通領域電話はグローバル一意識別子 (GUID) を共通名として使用します。つまり、これらの電話の Identity は、通常、以下のようになっています。CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>共通領域電話が移動するレジストラー プールの完全修飾ドメイン名 (FQDN)。たとえば、atl-cs-001.litwareinc.com。Target には、レジストラー プール以外に、ホスティング プロバイダーの FQDN も指定できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>共通領域電話を移動するために、指定したドメイン コントローラーに接続できるようにします。特定のドメイン コントローラーに接続するには、DomainController パラメーターの後に、コンピューター名 (たとえば、atl-cs-001 など) またはその FQDN (たとえば、atl-cs-001.litwareinc.com など) を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>このパラメーターが存在する場合は、共通領域電話の関連データ (デバイスに割り当てられているポリシーなど) を削除して、この共通領域電話を移動します。存在しない場合、電話は関連データと一緒に移動されます。</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定した場合、コンピューターは、バックエンド データベースに関して発生するすべてのエラーを無視し、そうしたエラーにかかわらず共通領域電話の移動を試みるように指示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>ユーザー オブジェクトを、移動するユーザー アカウントを表すパイプラインを介して、渡せるようにします。既定では、<strong>Move-CsCommonAreaPhone</strong> コマンドレットはパイプラインを介してオブジェクトを渡しません。</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>このパラメーターは Lync Online でのみ使用します。このパラメーターを Lync Server の社内実装で使用しないでください。</p></td>
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

文字列。**Move-CsCommonAreaPhone** コマンドレットは、共通領域電話の Identity を表すパイプライン処理された文字列値を受け入れます。

## 戻り値の種類

既定では、**Move-CsCommonAreaPhone** コマンドレットは、値もオブジェクトも戻しません。ただし、PassThru パラメーターを指定した場合、このコマンドレットは Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

