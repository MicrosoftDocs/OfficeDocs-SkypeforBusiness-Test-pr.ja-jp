---
title: Set-CsAnalogDevice
TOCTitle: Set-CsAnalogDevice
ms:assetid: b05e729e-cdef-4c78-8ce7-b183c3208a93
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412843(v=OCS.15)
ms:contentKeyID: 48273284
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAnalogDevice

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server を使用して管理できるアナログ デバイスのコレクションに含まれる既存のデバイスを変更します。アナログ デバイスとは、公衆交換電話網 (PSTN) に接続されている電話などのデバイスのことです。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsAnalogDevice -Identity <UserIdParameter> [-AnalogFax <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-Gateway <Fqdn>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com という Identity を持つアナログ デバイスの LineUri プロパティの値を変更します。

    Set-CsAnalogDevice -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -LineUri "TEL:+14255551298"

## 例 2

例 2 のコマンドは、現在ゲートウェイ 192.168.0.240 を使用している各アナログ デバイスのゲートウェイを変更します。このタスクを実行するには、Filter パラメーターを指定して **Get-CsAnalogDevice** コマンドレットを呼び出します。フィルター値 {Gateway -eq "192.168.0.240"} で、ゲートウェイが 192.168.0.240 と等しい (-eq) デバイスのみが戻されます。次に、このフィルター処理されたコレクションを **Set-CsAnalogDevice** コマンドレットにパイプ処理し、コレクション内の各項目を取得して Gateway プロパティの値を 192.168.1.100 に変更します。

    Get-CsAnalogDevice -Filter {Gateway -eq "192.168.0.240"} | Set-CsAnalogDevice -Gateway "192.168.1.100"

## 解説

アナログ デバイスには、公衆交換電話網 (PSTN) に接続される電話機、FAX 機器、モデム、およびテレタイプ/聴覚障碍者用文字電話デバイス (TTY/TTD) などがあります。エンタープライズ VoIP (Microsoft が提供するボイス オーバー IP (VoIP) ソリューションのこと) を利用するデバイスとは異なり、アナログ デバイスでは情報を送信するのにデジタル パケットは使用されません。代わりに、連続信号を使用して情報が送信されます。"アナログ デバイス" という用語は、この信号が一般にアナログ信号と呼ばれていることに由来します。

管理者がアナログ デバイスを管理できるようにするには、Lync Server を使用して、アナログ デバイスを Active Directory の連絡先オブジェクトに関連付けることができます。デバイスを連絡先オブジェクトに関連付けたら、ポリシーとダイヤル プランを連絡先に割り当てることによってそのアナログ デバイスを管理できます。

**Set-CsAnalogDevice** コマンドレットを実行すると、アナログ デバイスに関連付けられている連絡先オブジェクトのプロパティを変更することができます。たとえば、連絡先の Active Directory 表示名やそのデバイスに関連付けられている回線 Uniform Resource Identifier (URI) を変更できます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsAnalogDevice** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins。特定のサイトや特定の Active Directory 組織 (OU) に対してこのコマンドレットを実行する許可は、**Grant-CsOUPermission** コマンドレットを使用すると割り当てられます。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAnalogDevice"}

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
<td><p>変更するアナログ デバイスの一意識別子。アナログ デバイスは、関連付けられている連絡先オブジェクトの Active Directory 識別名 (DN) を使用して識別されます。既定では、アナログ デバイスでは、共通名として GUID (グローバル一意識別子) を使用します。したがって、デバイスは、通常、次のような Identity を持ちます。CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com。つまり、アナログ デバイスをより簡単に変更するには、<strong>Get-CsAnalogDevice</strong> コマンドレットを使用してアナログ デバイス オブジェクトを返し、次に <strong>Set-CsAnalogDevice</strong> コマンドレットにそれらのオブジェクトをパイプ処理します。</p></td>
</tr>
<tr class="even">
<td><p><em>AnalogFax</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>アナログ デバイスが FAX 機器の場合は True ($True) に設定します。デバイスが FAX 機器でない場合は False ($False) に設定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>アナログ デバイスの Active Directory 表示名を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>Lync に表示する電話番号。DisplayNumber プロパティは、希望する形式で設定できます。たとえば、1-800-555-1234、1-(800)-555-1234、1.800.555.1234 などの形式で設定できます。</p></td>
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
<td><p>True ($True) に設定すると、アナログ デバイスは Lync で使用できます。</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>アナログ デバイスの連絡先オブジェクトでエンタープライズ VoIP (Microsoft が提供する VoIP ソリューション) が有効にされているかどうかを示します。エンタープライズ VoIP を使用すると、標準の電話ネットワークでなくインターネットを使用して電話をかけることができます。</p></td>
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
<td><p><em>Gateway</em></p></td>
<td><p>省略可能</p></td>
<td><p>Fqdn</p></td>
<td><p>アナログ デバイスによって使用される PSTN ゲートウェイの IP アドレス。</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>アナログ デバイスの電話番号。回線 URI は、E.164 形式を使用し、先頭に &quot;TEL:&quot; というプレフィックスを付けて指定する必要があります。次に例を示します。TEL: +14255551297。内線番号は回線 URI の末尾に追加する必要があります。次に例を示します。TEL: +14255551297; ext=51297。</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>省略可能</p></td>
<td><p>witchParameter</p></td>
<td><p>共通領域電話を表すオブジェクトを戻します。</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>アナログ デバイスを使用して Lync 2013 などの SIP デバイスと通信するための一意識別子。SIP アドレスの先頭には、プレフィックス &quot;sip:&quot; を付ける必要があります (たとえば、sip:bldg14lobby@litwareinc.com)。</p></td>
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

Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact オブジェクト。**Set-CsAnalogDevice** コマンドレットは、パイプライン処理されたアナログ デバイス オブジェクトのインスタンスを受け入れます。

## 戻り値の種類

既定では、**Set-CsAnalogDevice** コマンドレットは、値もオブジェクトも戻しません。ただし、PassThru パラメーターを指定した場合、このコマンドレットは Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)

