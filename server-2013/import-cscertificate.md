---
title: Import-CsCertificate
TOCTitle: Import-CsCertificate
ms:assetid: 87bdafce-f4b9-4c44-ad8f-86c2deb680a4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398688(v=OCS.15)
ms:contentKeyID: 48272742
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsCertificate

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server で使用する証明書をインポートします。**Request-CsCertificate** コマンドレットを使用しても証明書を取得できない場合、証明書を Lync Server のサーバーの役割に割り当てるには、この証明書をインポートする必要があります。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Import-CsCertificate -Identity <XdsIdentity> -Type <CertType[]> <COMMON PARAMETERS>

    Import-CsCertificate [-PrivateKeyExportable <$true | $false>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Path <String> [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Password <String>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 のコマンドでは、C:\\Certificates\\WebServer.pfx という証明書をインポートします。コマンドが完了すると、証明書をサーバーの役割に割り当てることができるようになります。

    Import-CsCertificate -Path "C:\Certificates\WebServer.pfx" -PrivateKeyExportable $True

## 解説

Lync Server は、サーバーとサーバーの役割がそれぞれの ID を検証できるようにするために、証明書を使用します。たとえば、エッジ サーバーは、証明書を使用して、通信しているコンピューターが実際に フロント エンド サーバーであることを確認します。また、逆の場合も同様です。Lync Server を完全に実装するには、適切な証明書を適切なサーバーの役割に割り当てることが必要です。

証明書を Lync Server の役割に割り当てるには、これらの証明書が Lync Server で認識されている必要があります。**Request-CsCertificate** コマンドレットによって、新しい証明書要求をオンラインでもオフラインでも行うことができます。オンライン要求を行うと、証明書は自動的にダウンロードされてローカルの証明書ストアに保存されます。同じく重要となるのは、その証明書は Lync Server ですぐ使用できるようになることです。オフライン要求を行うと、証明書ファイルが送信されてきます。その時点で、**Import-CsCertificate** コマンドレットを使用して証明書をインポートできます。このプロセスにより、証明書を Lync Server のサーバーの役割に割り当てることができます。

このコマンドレットを実行できるユーザー: **Import-CsCertificate** コマンドレットをローカルで実行するため、ローカル管理者である必要があります。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsCertificate"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Global に設定されている場合、証明書がグローバル スコープで動作します。グローバル証明書は、適切なコンピューターに自動的にコピーおよび配布されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Path</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>インポートする証明書ファイルの完全なパスです。次に例を示します。–Path &quot;C:\Certificates\WebServer.cer&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>要求する証明書の型。たとえば、次のような証明書の型があります。</p>
<p>* AccessEdgeExternal</p>
<p>* AudioVideoAuthentication</p>
<p>* DataEdgeExternal</p>
<p>* Default</p>
<p>* External</p>
<p>* Internal</p>
<p>* iPadAPNService</p>
<p></p>
<p>* iPhoneAPNService</p>
<p>* LogRetentionService</p>
<p>* MPNService</p>
<p>* OAuthTokenIssuer</p>
<p>* PICWebService</p>
<p>* ProvisionService</p>
<p>* SMPDNSWebService</p>
<p>* TenantAdmin</p>
<p>* UpgradeEngineService</p>
<p>* WebServicesExternal</p>
<p>* WebServicesInternal</p>
<p>* WsFedTokenTransfer</p>
<p>* XMPPServer</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>EffectiveDate</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.DateTime</p></td>
<td><p>証明書を初めて使用できる日時。たとえば、2012 年 7 月 31 日の午前 8 時に初めて使用される証明書を構成するには、英語 (米国) の地域および言語設定の下で実行されているサーバー上で、次の構文を使用します。</p>
<p>-EffectiveTime &quot;7/31/2012 8:00 AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Password</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>証明書ファイルに関連付けられているパスワードです。</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True に設定されている場合は、ネットワーク サービス アカウントで証明書の秘密キーの部分を読み取ることができます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレット実行時に作成されるログ ファイルのファイル パスを指定できるようにします。次に例を示します。-Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Roll</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>EffectiveDate パラメーターで指定された日時に、指定された証明書を更新できます。これにより、新しい証明書が主要な証明書になる日時を指定できます。EffectiveDate パラメーターを指定しないで Roll パラメーターを指定すると、コマンドが失敗することに注意してください。</p></td>
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

なし。**Import-CsCertificate** コマンドレットは、パイプ処理による入力を受け入れません。

## 戻り値の種類

なし。

## 関連項目

#### その他のリソース

[Get-CsCertificate](get-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

