---
title: Set-CsExUmContact
TOCTitle: Set-CsExUmContact
ms:assetid: c0fe0fdc-6fea-4334-8645-24ffd494db07
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412944(v=OCS.15)
ms:contentKeyID: 48273455
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsExUmContact

 

_**トピックの最終更新日:** 2015-03-09_

ホストされた Exchange ユニファイド メッセージング (UM) の既存の自動応答またはサブスクライバー アクセスの連絡先オブジェクトを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsExUmContact -Identity <UserIdParameter> [-AutoAttendant <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、SIP アドレス exumsa4@fabrikam.com を持つ Exchange UM の連絡先の AutoAttendant プロパティを True に設定します。最初に、**Get-CsExUmContact** コマンドレットを呼び出して、連絡先オブジェクトを取得します (連絡先の Active Directory 表示名、連絡先のユーザー プリンシパル名、または連絡先のログオン名も使用できます)。このコマンドは、指定された ID の連絡先を 1 つ取得します。次に、この連絡先は **Set-CsExUmContact** コマンドレットに渡され、ここで、AutoAttendant パラメーターを True に設定します。

    Get-CsExUmContact -Identity sip:exumsa4@fabrikam.com | Set-CsExUmContact -AutoAttendant $True

## 例 2

この例は、例 1 と似ていますが、**Get-CsExUmContact** コマンドレットを呼び出して連絡先を取得し、このオブジェクトを **Set-CsExUmContact** コマンドレットにパイプ処理する代わりに、**Set-CsExUmContact** コマンドレットを、変更する連絡先の ID を指定した状態で使用します。ID の形式に注意してください。この場合、自動生成された GUID (連絡先の作成時に生成されたもの) を含む、連絡先オブジェクトの完全識別名を使用しています。次に、連絡先の AutoAttendant パラメーターを True に設定します。

    Set-CsExUmContact -Identity "CN={1bf6208d-2847-45d0-828f-636f14da858b},OU=ExUmContacts,DC=litwareinc,DC=com" -AutoAttendant $True

## 解説

Lync Server は Exchange UM と連携して、自動応答やサブスクライバー アクセスなどのいくつかの音声関連の機能を提供します。Exchange UM が (社内サービスではなく) ホスト サービスとして提供されている場合は、Windows PowerShell を使用して連絡先オブジェクトを作成し、自動応答やサブスクライバー アクセスの機能を適用する必要があります。これらのオブジェクトは、**New-CsExUmContact** コマンドレットを呼び出して作成し、後で **Set-CsExUmContact** コマンドレットを使用して変更することができます。

このコマンドレットを最も簡単に使用するには、多くの場合まず、**Get-CsExUmContact** コマンドレットを呼び出して、変更する連絡先オブジェクトのインスタンスを取得します。**Get-CsExUmContact** コマンドレット コマンドの出力をそのまま **Set-CsExUmContact** コマンドレットにパイプ処理して、変更するプロパティのパラメーターに値を割り当てます (詳細については、このトピックの例のセクションを参照してください)。または、**Set-CsExUmContact** コマンドレットを呼び出して、変更する連絡先オブジェクトの ID を渡すこともできます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Set-CsExUmContact** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsExUmContact"}

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
<td><p>変更する連絡先オブジェクトの一意の識別子です。連絡先 ID は、以下の 4 つの形式のうちの 1 つを使用して指定できます。1) 連絡先の SIP アドレス、2) 連絡先のユーザー プリンシパル名 (UPN)、3) ドメイン\ログオン形式 (litwareinc\exum1 など) の連絡先のドメイン名とログオン名、および 4) 連絡先の Active Directory 表示名 (Team Auto Attendant など)。</p>
<p>完全なデータ型:Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>AutoAttendant</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>連絡先オブジェクトが自動応答の場合は、このパラメーターを True に設定します。このパラメーターは、既定では False にされています。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>この連絡先の説明です。この説明は、管理者が連絡先の種類 (自動応答やサブスクライバー アクセスなど)、場所、プロバイダー、Exchange UM の各連絡先の目的に関するその他情報を識別するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>連絡先の電話番号です。各連絡先の表示番号は、一意である必要があります (Exchange UM の 2 つの連絡先が同じ表示番号を持つことはできません)。この値を変更すると、LineURI プロパティの値も変更されます。</p>
<p>この値には最初に正符号 (+) が付き、任意の複数の数字が含まれます。最初の数字はゼロ以外である必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Fqdn</p></td>
<td><p>ドメイン コントローラーを指定できます。ドメイン コントローラーを指定しない場合は、最初に使用可能なものが使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>連絡先が Lync Server に対して有効になっているかどうかを示します。このパラメーターを False に設定すると、連絡先が無効になり、この連絡先に関連付けられた自動応答またはサブスクライバー アクセスは機能しなくなります。</p>
<p>Enabled パラメーターを使用してアカウントを無効にした場合、そのアカウントに関連付けられた情報 (割り当てられたホスト ボイスメール ポリシーを含む) は保持されます。後で、Enable パラメーターを使用してアカウントを再び有効にすると、関連付けられたアカウントの情報が復元されます。</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>連絡先がエンタープライズ VoIP に対して有効になっているかどうかを示します。この値が False に設定されている場合、この連絡先に関連付けられた自動応答またはサブスクライバー アクセス機能は使用できなくなります。</p></td>
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
<td><p><em>PassThru</em></p></td>
<td><p>省略可能</p></td>
<td><p>witchParameter</p></td>
<td><p>コマンドの結果を戻します。既定では、このコマンドレットによる出力はありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>連絡先の SIP アドレスです。このアドレスは、Active Directory ドメイン サービス にユーザーまたは連絡先として存在していない新しいアドレスである必要があります。</p>
<p>この値を変更すると、OtherIpPhone プロパティに保存されている SIP アドレスも変更されます。</p>
<p>SipAddress は、特定の連絡先を取得するために、<strong>Get-CsExUmContact</strong> コマンドレット コマンドの ID 値として使用することができます。このコマンドレットを呼び出すときに、新しい SipAddress が使用されます。古い SIP アドレスのクエリはオブジェクトを戻しません。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact オブジェクト。Exchange UM 連絡先オブジェクトのパイプライン入力を受け入れます。

## 戻り値の種類

このコマンドレットは、Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact 型のオブジェクトを変更します。PassThru パラメーターを使用した場合も、この型のオブジェクトを戻します。

## 関連項目

#### その他のリソース

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

