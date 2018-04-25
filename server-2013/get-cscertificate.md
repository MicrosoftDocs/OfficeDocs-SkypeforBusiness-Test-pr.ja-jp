---
title: Get-CsCertificate
TOCTitle: Get-CsCertificate
ms:assetid: 15b8f019-1d00-4389-9abe-18deb8cbf2ea
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398227(v=OCS.15)
ms:contentKeyID: 48271369
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCertificate

 

_**トピックの最終更新日:** 2015-03-09_

Lync Server での使用に構成されているローカル コンピューターの証明書に関する情報を戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsCertificate [-Identity <XdsIdentity>] [-Report <String>] [-Type <CertType[]>]

## 例

## 例 1

例 1 のコマンドは、Lync Server コンポーネントに現在割り当てられている証明書に関する情報を戻します。追加パラメーターを指定せずに **Get-CsCertificate** コマンドレットを呼び出すことで、これを行っています。

    Get-CsCertificate

## 例 2

例 2 では、内部 Web サービスに使用されているすべての Lync Server 証明書を取得します。これを行うために、Type パラメーターを使用してパラメーター値 WebServicesInternal を指定します。

    Get-CsCertificate -Type WebServicesInternal

## 例 3

例 3 は、2012 年 9 月 1 日より前に有効期限が切れるすべての Lync Server 証明書を返します。このタスクを実行するために、コマンドでは、まず **Get-CsCertificate** コマンドレットを使用して、現在使用されているすべての Lync Server 証明書のコレクションを返します。そのコレクションは **Where-Object** コマンドレットにパイプ処理され、これにより 2012 年 9 月 1 日より前に有効期限が切れる証明書のみが選択されます。この例に指定している日付 (9/1/2012) は、英語 (米国) の日付と時刻の形式を使用しています。日付は、使用する地域および言語のオプションに合わせた形式を使用して指定する必要があります。

    Get-CsCertificate | Where-Object {$_.NotAfter -lt "9/1/2012"}

## 例 4

例 4 では、証明機関 (CA) MyCa によって発行されたすべての Lync Server 証明書に関する情報を戻します。これを行うために、現在使用されているすべての証明書のコレクションを戻すよう、コマンドでまず、パラメーターを指定せずに **Get-CsCertificate** コマンドレットを呼び出します。このコレクションを **Where-Object** コマンドレットにパイプ処理し、Issuer プロパティが "Cn=MyCa" と等しい (-eq) すべての証明書を取得します。

    Get-CsCertificate | Where-Object {$_.Issuer -eq "Cn=MyCa"}

## 例 5

例 5 のコマンドは、Subject プロパティが CN=atl-cs-001.litwareinc.com に設定されているすべての Lync Server 証明書を戻します。これを行うために、**Get-CsCertificate** コマンドレットを使用してすべての Lync Server 証明書のコレクションを戻し、そのコレクションを **Where-Object** コマンドレットにパイプ処理します。今回は、**Where-Object** コマンドレットにより、Subject プロパティが "CN=atl-cs-001.litwareinc.com" に等しい証明書のみが選択されます。

    Get-CsCertificate | Where-Object {$_.Subject -eq "CN=atl-cs-001.litwareinc.com"}

## 解説

Lync Server は、サーバーとサーバーの役割がそれぞれの ID を検証できるようにするために、証明書を使用します。たとえば、エッジ サーバーは、証明書を使用して、通信しているコンピューターが実際にフロント エンド サーバーであることを確認します。また、逆の場合も同様です。Lync Server を完全に実装するために、適切な証明書を該当するサーバーの役割に割り当てる必要があります。

**Get-CsCertificate** コマンドレットを実行すると、Lync Server での使用に構成されている証明書に関する詳細な情報を取得できます。このコマンドレットを実行すると、Lync Server 証明書に関する情報のみ戻されます。Lync Server で使用するために (**Set-CsCertificate** コマンドレットを使用して) 証明書が構成されていない場合、**Get-CsCertificate** コマンドレットを実行しても証明書は戻されません。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Get-CsCertificate** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。

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
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>グローバル スコープで構成されている証明書を取得できます (グローバル証明書はコピーされ適切なコンピューターに配布されます)。グローバル証明書に関する情報を戻すには、次の構文を使用します。</p>
<p>Get-CsCertificate –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p><strong>Get-CsCertificate</strong> コマンドレットによって実行される手順に関する詳細な情報を記録できます。パラメーター値は、生成される HTML ファイルへの完全なパスである必要があります。次に例を示します。-Report C:\Logs\Certificates.html。指定したファイルが既に存在する場合、新しい情報で自動的に上書きされます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>要求する証明書の型。たとえば、次のような証明書の型があります。</p>
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
<p>たとえば、次の構文は Default 証明書に関する情報を戻します。-Type Default。</p>
<p>次のように証明書の型をコンマで区切ると、1 つのコマンドで複数の型を指定できます。</p>
<p>-Type Internal,External,Default</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsCertificate** コマンドレットはパイプライン処理された入力を受け入れません。

## 戻り値の種類

**Get-CsCertificate** コマンドレットを実行すると、Microsoft.Rtc.Management.Deployment.CertificateReference オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

