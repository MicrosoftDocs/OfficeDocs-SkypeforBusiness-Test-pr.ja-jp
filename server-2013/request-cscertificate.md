---
title: Request-CsCertificate
TOCTitle: Request-CsCertificate
ms:assetid: 24e8ba6f-6023-4c03-a594-5b40784fd16a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425723(v=OCS.15)
ms:contentKeyID: 48271504
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Request-CsCertificate

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server を実行するサーバーとサーバーの役割で使用する証明書を要求することができます。また、既存の証明書要求のステータスをチェックしたり、必要な場合にはそれらの要求のいずれか (またはすべて) を取り消すことができます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Request-CsCertificate -New <SwitchParameter> -Type <CertType[]> [-AllSipDomain <SwitchParameter>] [-CA <String>] [-CaAccount <String>] [-CaPassword <String>] [-City <String>] [-ClientEKU <$true | $false>] [-ComputerFqdn <Fqdn>] [-Country <String>] [-DomainName <String>] [-FriendlyName <String>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-KeyAlg <RSA | ECDH_P256 | ECDH_P384 | ECDH_P521>] [-KeySize <Int32>] [-Organization <String>] [-OU <String>] [-Output <String>] [-PrivateKeyExportable <$true | $false>] [-State <String>] [-Template <String>] <COMMON PARAMETERS>

    Request-CsCertificate -List <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Retrieve <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Clear <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 のコマンドにより、atl-ca-001.litwareinc.com\\myca という CA に接続し、新しい WebServicesExternal 証明書を要求する、新しい証明書要求が作成されます。

    Request-CsCertificate -New -Type WebServicesExternal -CA "atl-ca-001.litwareinc.com\myca"

## 例 2

例 2 では、**Request-CsCertificate** コマンドレットを使用して行われたすべての保留中の証明書要求を一覧表示します。

    Request-CsCertificate -List

## 例 3

例 3 では、Output パラメーターを使用してオフライン証明書要求を作成します。

    Request-CsCertificate -New -Type WebServicesExternal -Output C:\Certificates\WebServicesExternal.cer

## 例 4

例 4 は、Request-CsCertificate コマンドレットの使用方法に関するより詳細な (しかも現実的な) 例です。この例では、Lync Server の Standard Edition で使用する証明書を要求します。

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Standard Edition Certficate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-cs-001.litwareinc.com,atl-ext.litwareinc.com"

## 例 5

例 5 では、Lync Server の Enterprise Edition で使用するプール証明書を要求します。

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Enterprise Edition Pool Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "pool1.litwareinc.com,pool1int.litwareinc.com,pool1ext.litwareinc.com"

## 例 6

例 6 は、内部エッジ サーバーの証明書を要求する方法を示しています。

    Request-CsCertificate -New -Type Internal -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Internal Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com, ap.litwareinc.com"

## 例 7

例 7 は、例 6 のコマンドの変化形です。ただし、この場合、要求は外部 エッジ サーバー に対するものです。

    Request-CsCertificate -New -Type AccessEdgeExternal,DataEdgeExternal,AudioVideoAuthentication -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "External Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com,ap.litwareinc.com,dp.litwareinc.com,atl-edge-001"

## 解説

Lync Server では、サーバーとサーバーの役割がそれぞれの身元を確認するための手段として証明書を使用します。たとえば、エッジ サーバーは証明書を使用して、通信相手のコンピューターが本当にフロント エンド サーバーかどうかを確認します。また、逆の場合も同様です。Lync Server を完全に実装するには、適切な証明書が適切なサーバーの役割に割り当てられるようにする必要があります。

Lync Server で使用する証明書を要求する方法の 1 つは、**Request-CsCertificate** コマンドレットを呼び出すことです。 他の標準 Windows ツールを使用して Lync Server で使用する証明書を要求することも可能ですが、**Request-CsCertificate** コマンドレットを使用することには、このコマンドレットによって証明機関 (CA) に接続する前にトポロジーを分析できるという大きな利点があります。 **Request-CsCertificate** コマンドレットは、その分析結果に基づいて、適切なサブジェクト名フィールドとサブジェクト代替名フィールドを持つ証明書を自動的に要求します。

**Request-CsCertificate** コマンドレットは、特に Lync Server で使用する証明書を要求するように設計されています。 多目的の証明書管理ツールとして設計されているわけではありません。

新しい証明書を要求することに加えて、保留中の証明書要求が **Request-CsCertificate** コマンドレットを使用して作成されたものでれば、このコマンドレットを使用してそれらの要求を確認することができます。 **Request-CsCertificate** コマンドレットは、保留中の証明書要求がそのコマンドレットを使用して作成されたものである限り、それらの要求を削除するときにも使用できます。

失効した要求がある場合、証明書要求を取得しようとすると、エラー メッセージが表示される場合があります。現在、**Request-CsCertificate** コマンドレットでは、次の種類の要求のみサポートしています。 発行済み、拒否、保留中。 失効した要求のために問題が発生した場合は、次のようなコマンドを使用して失効した要求をクリアします (ここで、224 は失効した証明書要求の RequestID です)。

Request-CsCertificate –Clear –RequestID 224

その後で、証明書要求を取得できるようになります。

このコマンドレットを実行できるメンバー。 **Request-CsCertificate** コマンドレットをローカルで実行するためには、ローカル管理者であり、指定の証明機関に対する権限を持っている必要があります。 このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Request-CsCertificate"}

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
<td><p><em>Clear</em></p></td>
<td><p>必須</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定すると、<strong>Request-CsCertificate</strong> コマンドレットを使用して作成された保留中の証明書要求がすべて削除されます。</p></td>
</tr>
<tr class="even">
<td><p><em>List</em></p></td>
<td><p>必須</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定すると、<strong>Request-CsCertificate</strong> コマンドレットを使用して作成された保留中の証明書要求がすべて一覧表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>New</em></p></td>
<td><p>必須</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定すると、新しい証明書を要求することを示します。</p></td>
</tr>
<tr class="even">
<td><p><em>Retrieve</em></p></td>
<td><p>必須</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定すると、<strong>Request-CsCertificate</strong> コマンドレットを使用して作成された保留中の証明書要求すべてを取得し、操作の完了を試み、要求された証明書をインポートします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>要求する証明書のタイプ。 次のようなタイプの証明書があります (これらに限定されるわけではありません)。</p>
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
<p>たとえば、次の構文によって新しい Default 証明書を要求します。 -Type Default。</p>
<p>次のように、証明書の種類をコンマで区切ることにより、1 つのコマンドで複数の種類を指定できます。</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>AllSipDomain</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定すると、すべての SIP ドメインが証明書のサブジェクト代替名フィールドに自動的に追加されます。指定しない場合、既定では、プライマリ SIP ドメインのみが追加されます。ただし、DomainName パラメーターを指定すると、追加ドメインを指定できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>CA</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>CA を指す完全修飾ドメイン名 (FQDN)。 次に例を示します。 -CA &quot;atl-ca-001.litwareinc.com\myca&quot;。 既知の CA の一覧を表示するには、Windows PowerShell プロンプトで次のように入力して Enter キーを押します。</p>
<p>certutil</p>
<p>Certutil によって戻される Config プロパティは、CA の場所を示します。</p></td>
</tr>
<tr class="even">
<td><p><em>CaAccount</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>ドメイン\ユーザー名の形式を使用して新しい資格情報を要求するユーザーのアカウント名。 次に例を示します。 -CaAccount &quot;litwareinc\kenmyer&quot;。 指定しない場合、<strong>Request-CsCertificate</strong> コマンドレットは、新しい資格情報を要求するときにログオン ユーザーの資格情報を使用します。</p></td>
</tr>
<tr class="odd">
<td><p><em>CaPassword</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>新しい証明書を要求するユーザーのパスワード (CaAccount パラメーターを使用して指定)。</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>証明書が展開される市区町村。</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientEKU</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>証明書をクライアント認証で使用する場合は、このパラメーターを True に設定します。 この方式の認証は、ユーザーが、AOL のアカウントを持つ人々とインスタント メッセージを交換できるようにする場合に必要になります。 パラメーター名の EKU 部分は、拡張キー使用法の短縮形です。拡張キー使用法フィールドには、その証明書で有効な使用法の一覧が表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>ComputerFqdn</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>証明書を要求するコンピューターの FQDN。 指定すると、指定したコンピューターの場所を検出するために、中央管理ストア に接続するよう <strong>Request-CsCertificate</strong> コマンドレットが強制的に実行されます。 プール証明書を要求する場合でも、証明書を要求する場合は常にコンピューター名を使用する必要があります。 <strong>Request-CsCertificate</strong> コマンドレットを実行すると、このコマンドレットを使用して取得される証明書のサブジェクト名にプール名が自動的に追加されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Country</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>証明書が展開される国/地域。</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainName</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>証明書のサブジェクトの別名フィールドに追加する必要のある完全修飾ドメイン名のコンマ区切り一覧。次に例を示します。</p>
<p>-DomainName &quot;atl-cs-001.litwareinc.com, atl-cs-002.litwareinc.com,atl-cs-003.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>FriendlyName</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>証明書の識別を容易にするユーザー割り当ての名前。</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>ドメイン内のグローバル カタログ サーバーの FQDN。 属するドメイン内のアカウントを使用して、コンピューターで <strong>Request-CsCertificate</strong> コマンドレットを実行する場合、このパラメーターは不要です。</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>グローバル設定が保存されているドメイン コントローラーの FQDN。グローバル設定が Active Directory ドメイン サービス のシステム コンテナーに保存されている場合は、このパラメーターでルート ドメイン コントローラーを指定する必要があります。 グローバル設定が構成コンテナーに保存されている場合は、すべてのドメイン コントローラーが使用でき、このパラメーターを省略できます。</p></td>
</tr>
<tr class="even">
<td><p><em>KeyAlg</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.X509Certificates.KeyAlgorithmIdentifier</p></td>
<td><p>新しい証明書の公開キーと秘密キーを生成するときに使用する暗号化アルゴリズムのタイプを示します。 次のような有効なキー アルゴリズムがあります。</p>
<p>RSA</p>
<p>ECDH_P256</p>
<p>ECDH_P384</p>
<p>ECDH_P521</p></td>
</tr>
<tr class="odd">
<td><p><em>KeySize</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Int32</p></td>
<td><p>証明書で使用する秘密キーのサイズ (ビット単位) を指定します。 キーのサイズが大きいほど安全性が高くなりますが、復号化するためには処理のオーバーヘッドが大きくなります。</p>
<p>有効なキーのサイズは、1024、2048、および 4096 です。たとえば、次のようになります。 -KeySize 2048。</p></td>
</tr>
<tr class="even">
<td><p><em>Organization</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>新しい証明書を要求している組織の名前。 次に例を示します。 -Organization &quot;Litwareinc&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>新しい証明書を割り当てるコンピューターの Active Directory 組織単位。</p></td>
</tr>
<tr class="even">
<td><p><em>Output</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>証明書ファイルへのパス。 オフライン証明書要求を作成する場合、Output パラメーターを使用して、証明書要求へのファイル パスを指定します。たとえば、次のように指定します。 -Output C:\Certificates\NewCertificate.pfx。これにより、処理のために証明機関に電子メールで送付することができる、証明書要求ファイルが作成されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>証明書の秘密キーをエクスポート可能にする場合は、このパラメーターを True に設定します。 秘密キーがエクスポート可能な場合は、証明書をコピーして複数のコンピューターで使用することができます。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレット実行時に作成されるログ ファイルのファイル パスを指定できるようにします。 次に例を示します。 -Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>RequestId</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Int32</p></td>
<td><p>証明書要求に関連付けられた識別番号。 RequestID パラメーターを使用することにより、個々の証明書を一覧表示、取得、またはクリアすることができます。</p></td>
</tr>
<tr class="even">
<td><p><em>State</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>証明書が展開される都道府県。 次に例を示します。 -State WA。</p></td>
</tr>
<tr class="odd">
<td><p><em>Template</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>新しい証明書を生成するときに使用する証明書テンプレートを指定します。たとえば-Template &quot;WebServer&quot; のようになります。 要求されたテンプレートは、CA にインストールされている必要があります。 入力する値は、テンプレートの表示名でなく、テンプレート名である必要があります。</p></td>
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

なし。 **Request-CsCertificate** コマンドレットは、パイプ処理された入力を受け入れません。

## 戻り値の種類

なし。 代わりに、**Request-CsCertificate** コマンドレットは、Microsoft.Rtc.Management.Deployment.CertificateReference オブジェクトのインスタンスの管理に役立ちます。

## 関連項目

#### その他のリソース

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

