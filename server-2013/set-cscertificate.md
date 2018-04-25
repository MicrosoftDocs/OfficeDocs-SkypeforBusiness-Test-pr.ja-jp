---
title: Set-CsCertificate
TOCTitle: Set-CsCertificate
ms:assetid: 6da0be05-b257-4258-9d6d-7ddf283f1038
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398518(v=OCS.15)
ms:contentKeyID: 48272405
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCertificate

 

_**トピックの最終更新日:** 2015-03-09_

証明書を Lync Server サーバーまたはサーバーの役割に割り当てることができます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsCertificate -Reference <CertificateReference> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCertificate -Identity <XdsIdentity> -Path <String> -Type <CertType[]> [-Password <String>] <COMMON PARAMETERS>

    Set-CsCertificate -Thumbprint <String> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドは、拇印が B142918E463981A76503828BB1278391B716280987B の証明書を、ローカル コンピューター上の WebServicesExternal の役割に割り当てます。

    Set-CsCertificate -Type WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## 例 2

例 2 では、拇印が B142918E463981A76503828BB1278391B716280987B の証明書を、ローカル コンピューター上の 3 種類の役割 (Default、WebServicesInternal、および WebServicesExternal) に割り当てます。

    Set-CsCertificate -Type Default, WebServicesInternal, WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## 解説

Lync Server は、サーバーとサーバーの役割がそれぞれの ID を検証するための手段として証明書を使用します。たとえば、エッジ サーバーは、証明書を使用して、通信先のコンピューターが実際にフロント エンド サーバーであることを確認します。また、逆の場合も同様です。Lync Server を完全に実装するには、適切な証明書が適切なサーバーの役割に割り当てられるようにする必要があります。

**Set-CsCertificate** コマンドレットを使用すると、管理者は証明書をサーバーまたはサーバーの役割に割り当てることができます。Lync Server で使用できるよう構成済みの証明書のみを割り当てることができる点に留意してください。割り当てることができる証明書を特定するには、**Get-CsCertificate** コマンドレットを使用します。

このコマンドレットを実行できるユーザー:**Set-CsCertificate** コマンドレットをローカルで実行するには、ローカル管理者である必要があります。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCertificate"}

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
<td><p>.PFX 証明書ファイルの完全なパス。</p></td>
</tr>
<tr class="odd">
<td><p><em>Reference</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertificateReference</p></td>
<td><p>Lync Server での使用向けに構成された証明書へのオブジェクト参照。以下のコマンドは拇印が B142918E463981A76503828BB1278391B716280987B の証明書を表すオブジェクト参照 (変数 $x) を戻します。</p>
<p>$x = Get-CsCertificate | Where-Object {$_.Thumbprint –eq &quot;B142918E463981A76503828BB1278391B716280987B&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Thumbprint</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>証明書の一意の識別子。証明書の拇印は、B142918E463981A76503828BB1278391B716280987B のようになります。</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>割り当てられる証明書の種類です。次のような証明書の種類があります (ただし、これらに限定されません)。</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (Microsoft Lync Online 2010 のみ)</p>
<p>ProvisionService (Microsoft Lync Online 2010 のみ)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>たとえば、次の構文によって既定の証明書を割り当てます。 -Type Default。</p>
<p>証明書の種類をコンマで区切ることにより、1 つのコマンドで複数の種類を割り当てることができます。</p>
<p>-Type Internal,External,Default</p></td>
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
<td><p>証明書のパスワード。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p><strong>Set-CsCertificate</strong> コマンドレットで実行される手順に関する詳細を記録できます。パラメーター値は、生成される HTML ファイルへの完全なパス (-Report C:\Logs\Certificates.html など) を指定する必要があります。-Report C:\Logs\Certificates.html。指定したファイルが既に存在する場合、新しい情報で自動的に上書きされます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Roll</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定した証明書を、EffectiveDate パラメーターで指定された日時に更新できます。これにより、新しい証明書がプライマリ証明書になる日時を指定することができます。EffectiveDate パラメーターを指定せずに Roll パラメーターを指定すると、コマンドが失敗することに注意してください。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.Deployment.CertificateReference。

## 戻り値の種類

**Set-CsCertificate** コマンドレットは値やオブジェクトを戻しません。

## 関連項目

#### その他のリソース

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)

