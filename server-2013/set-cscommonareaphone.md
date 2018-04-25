---
title: Set-CsCommonAreaPhone
TOCTitle: Set-CsCommonAreaPhone
ms:assetid: 765ab74c-33ca-4b17-ba15-edb2fe559ebb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398579(v=OCS.15)
ms:contentKeyID: 48272510
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCommonAreaPhone

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server によって管理される共通領域電話のプロパティ値を変更します。共通領域電話とは、建物のロビー、従業員休憩室など、多数の異なる人々によってさまざまな目的で使用される可能性がある電話のことです。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsCommonAreaPhone -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 を実行すると、電話番号が 1-425-555-6710 の共通領域電話の Active Directory 表示名が変更されます。これを行うために、最初に Filter パラメーターを指定して **Get-CsCommonAreaPhone** コマンドレットを呼び出しています。フィルター値 {LineUri -eq "tel:+14255556710"} は、戻されるデータを、LineUri プロパティが tel:+14255556710 に等しい共通領域電話に制限します。次に、戻されたオブジェクトを **Set-CsCommonAreaPhone** コマンドレットにパイプ処理し、DisplayName プロパティの値を "Employee Lounge" に設定しています。

    Get-CsCommonAreaPhone -Filter {LineUri -eq "tel:+14255556710"} | Set-CsCommonAreaPhone -DisplayName "Employee Lounge"

## 例 2

例 2 に示すコマンドを実行すると、現在組織で使用するように構成されている、すべての共通領域電話が有効化されます。このタスクを実行するために、このコマンドではパラメーターを指定せずに **Get-CsCommonAreaPhone** コマンドレットを呼び出して、すべての共通領域電話のコレクションを取得しています。次に、このコレクションを **Set-CsCommonAreaPhone** コマンドレットにパイプ処理し、コレクション内の各項目に対して、Enabled プロパティを True に設定します。

    Get-CsCommonAreaPhone | Set-CsCommonAreaPhone -Enabled $True

## 例 3

例 3 では、Description プロパティに値が割り当てられていないすべての共通領域電話に、一般的な説明が追加されます。これを実行するため、Filter パラメーターを指定して **Get-CsCommonAreaPhone** コマンドレットが呼び出されています。フィルター値 {Description -eq $Null} によって、戻される項目は、Description プロパティが Null 値に等しい共通領域電話に制限されるようにしています。次に、このフィルター処理済みコレクションを **Set-CsCommonAreaPhone** コマンドレットにパイプ処理し、一般的な説明 "Common area phone" をコレクション内の各項目に割り当てています。

    Get-CsCommonAreaPhone -Filter {Description -eq $Null} | Set-CsCommonAreaPhone -Description "Common area phone"

## 解説

共通領域電話とは、個別のユーザーに関連付けられていない IP 電話のことです。共通領域電話は、通常、個人のオフィスにあるのではなく、建物のロビー、カフェテリア、従業員休憩室、会議室のほか、多数の人が集まる可能性のある場所に置かれています。このことは、管理者にとって管理上の課題になります。Lync Server で使用される電話は、通常、個別のユーザーに割り当てた音声ポリシーとダイヤル プランを使用して管理するからです。共通領域電話に対して、個別のユーザーは割り当てられていません。

この課題の 1 つの解決策は、すべての共通領域電話に対して Active Directory の連絡先オブジェクトを作成することです (この連絡先オブジェクトは、**New-CsCommonAreaPhone** コマンドレットを使用して作成できます)。ユーザー アカウントと同様、この連絡先オブジェクトはポリシーとボイス計画に割り当てることができます。これにより、共通領域電話が個々のユーザーに関連付けられていない場合でも、これらの電話に対する管理機能を保持することができます。たとえば、ユーザーが共通領域電話からの着信を転送または保留できないようにする場合は、着信の転送および通話の保留を禁止する音声ポリシーを作成し、そのポリシーを共通領域電話 (より正確には、共通領域電話を表す連絡先オブジェクト) に割り当てます。次のコマンドにより、音声ポリシー CommonAreaPhoneVoicePolicy をすべての共通領域電話に割り当てます。

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

**Set-CsCommonAreaPhone** コマンドレットを使用すると、共通領域電話に関連付けられた、連絡先オブジェクトの各種プロパティを変更できます。特に、連絡先の Active Directory 表示名や、電話に関連付けられた回線 URL (Uniform Resource Identifier) を変更できます。Enabled パラメーターを使用して、Lync Server で使用するアカウントを有効または無効にすることもできます。

さらに、CsClientPolicy コマンドレットを使用して、共通領域電話に対して "ホットデスク機能" を構成できます。ユーザーは、ホットデスク機能が構成された電話に Lync Server 資格情報を使用してログオンできます。これにより、ユーザーが簡単に連絡先にアクセスできます。詳細については、[Set-CsClientPolicy](set-csclientpolicy.md) コマンドレットのヘルプ トピックを参照してください。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsCommonAreaPhone** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins。特定のサイトまたは特定の Active Directory の組織単位 (OU) でこのコマンドレットを実行するためのアクセス許可は、**Grant-CsOUPermission** コマンドレットを使用して割り当てることができます。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCommonAreaPhone"}

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
<td><p>UserIdParameter</p></td>
<td><p>共通領域電話の一意の識別子です。共通領域電話は、関連付けられている連絡先オブジェクトの Active Directory 識別名を使用して識別されます。既定では、共通領域電話は、グローバル一意識別子 (GUID) を共通名として使用します。つまり、共通領域電話の Identity は、通常、次のようになります。CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。このため、<strong>Get-CsCommonAreaPhone</strong> コマンドレットを使用して共通領域電話を取得し、取得したオブジェクトを <strong>Set-CsCommonAreaPhone</strong> コマンドレットにパイプ処理するほうが容易な場合もあります。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>共通領域電話の Active Directory の説明属性を変更できるようにします。これにより、電話に関する追加情報を入力できます。たとえば、電話に問題が生じた場合の連絡先に関する詳細を追加できます。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>共通領域電話の Active Directory の表示名を変更できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>Lync に表示する電話番号です。DisplayNumber プロパティは、たとえば 1-800-555-1234、1-(800)-555-1234、1.800.555.1234 など、任意の書式で設定できます。表示番号を選択する場合は、その番号を正規化することが可能な場合にのみ、共通領域電話の表示画面に表示されることに留意してください (正規化とは、番号文字列を標準の電話番号形式に変換するプロセスのことです)。表示番号の構成時に使用する電話番号形式の正規化ルールが存在しない場合、共通領域電話の表示画面には、DisplayNumber プロパティの値ではなく LineUri プロパティの値が表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Fqdn</p></td>
<td><p>連絡先情報を変更するために、指定したドメイン コントローラーに接続できるようにします。特定のドメイン コントローラーに接続するには、DomainController パラメーターの後に、コンピューター名 (たとえば、atl-mcs-001 など) またはその完全修飾ドメイン名 (FQDN) (たとえば、atl-mcs-001.litwareinc.com など) を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>共通領域電話の連絡先オブジェクトが、Lync Server で有効かどうかを指定します。</p>
<p>Enabled パラメーターを使用して連絡先を無効にしている場合は、そのアカウントに関連する情報 (割り当てられているポリシー、エンタープライズ VoIP 、リモート通話コントロール、およびボイス メール統合に対して連絡先が有効になっているかどうかなど) は保持されます。後で Enabled パラメーターを使用してアカウントを再度有効にすると、関連するアカウント情報が復元されます。</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>共通領域電話の連絡先オブジェクトが、エンタープライズ VoIP (Microsoft が提供するボイス オーバー IP (VoIP) ソリューション) で有効かどうかを指定します。エンタープライズ VoIP を使用すると、標準の電話ネットワークでなくインターネットを使用して電話をかけることができます。</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>省略可能</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>連絡先のインスタント メッセージング セッションのアーカイブ先を指定します。有効な値は次のとおりです。</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>LineURI</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>共通領域電話の電話番号。回線 URI (Uniform Resource Identifier) は E.164 形式で指定し、先頭に &quot;TEL:&quot; というプレフィックスを付ける必要があります。次に例を示します。TEL: +14255551297。内線番号は回線 URI の末尾に追加する必要があります。次に例を示します。TEL: +14255551297; ext=51297。</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>共通領域電話を表すオブジェクトを戻します。</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>共通領域電話が Lync などの SIP デバイスと通信できるようにする、一意の識別子です。SIP アドレスの先頭には、プレフィックス &quot;sip:&quot; を付け、有効な SIP ドメインを含める必要があります。次に例を示します。sip:bldg14lobby@litwareinc.com。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact オブジェクト。

## 戻り値の種類

既定では、**Set-CsCommonAreaPhone** コマンドレットは、値やオブジェクトを戻しません。ただし、このコマンドレットで PassThru パラメーターを指定すると、Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact のインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)

