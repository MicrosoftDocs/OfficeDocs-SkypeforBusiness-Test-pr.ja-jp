---
title: Remove-CsCertificate
TOCTitle: Remove-CsCertificate
ms:assetid: b7a83a58-9d3f-458a-867e-44466c9817dc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412895(v=OCS.15)
ms:contentKeyID: 48273351
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCertificate

 

_**トピックの最終更新日:** 2015-03-09_

以前に Lync Server での使用が可能としてマークした証明書を削除します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsCertificate -Type <CertType[]> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsIdentity>] [-Previous <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドを実行すると、Lync Server で使用可能なすべての WebServicesExternal 証明書が削除されます。これらの証明書のうちいずれかが現在使用中の場合、**Remove-CsCertificate** コマンドレットによってその証明書を本当に削除するのか確認メッセージが表示されます。コマンドを完了させるには、この確認メッセージに応答する必要があります。確認メッセージを表示しないようにするには、次のように Force パラメーターを使用します。

Remove-CsCertificate –Type WebServicesExternal -Force

    Remove-CsCertificate -Type WebServicesExternal

## 解説

Lync Server は、サーバーとサーバーの役割がそれぞれの ID を検証できるようにするために、証明書を使用します。たとえば、エッジ サーバーは、証明書を使用して、通信しているコンピューターが実際にフロント エンド サーバーであることを確認します。また、逆の場合も同様です。Lync Server を完全に実装するには、適切な証明書が適切なサーバーの役割に割り当てられるようにする必要があります。

**Remove-CsCertificate** コマンドレットを使用すると、現在 Lync Server によって使用されている証明書を削除できます。**Remove-CsCertificate** コマンドレットでは、証明書そのものを実際には削除しません。代わりに、その証明書を Lync Server ではこれ以上使用できないものとしてマークし、証明書のすべてのバインドを削除して、証明書に対するアクセス許可を失効させます (他のサービスがその証明書を使用できないようにするため)。これは特に、**Get-CsCertificate** コマンドレット実行時に、その証明書が表示されなくなることを意味します。

証明書を再度 Lync Server で使用するには、**Set-CsCertificate** コマンドレットを使用してその証明書を Lync Server に再割り当てする必要があります。

現在使用中の証明書を削除しようとすると、**Remove-CsCertificate** コマンドレットによって、その証明書を本当に削除するのか確認メッセージが表示されます。その確認メッセージに応答するまで、証明書は削除できません。この確認メッセージを表示せず、証明書が現在使用中であってもそのまま削除するには、次のようにコマンドに Force パラメーターを追加します。

Remove-CsCertificate –Type WebServicesExternal -Force

このコマンドレットを実行できるユーザー: **Remove-CsCertificate** コマンドレットをローカルに実行するためには、ローカルの管理者であるか、ドメインのメンバーである必要があります。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCertificate"}

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
<td><p><em>Type</em></p></td>
<td><p>必須かどうか</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>削除する証明書の型。たとえば、次のような証明書の型があります。</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>PICWebService (Microsoft Lync Online 2010 のみ)</p>
<p>ProvisionService (Microsoft Lync Online 2010 のみ)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>たとえば、次の構文は Default 証明書を削除します。-Type Default。</p>
<p>次のように証明書の型をコンマで区切ると、1 つのコマンドで複数の型を削除できます。</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>現在使用中の証明書を削除しようとした場合に、通常表示される確認メッセージを表示しません。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Global に設定すると、グローバル スコープから証明書が削除されます。指定しないと、ローカル コンピューターから証明書が削除されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Previous</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定された場合、現在割り当てられている証明書ではなく以前に割り当てられた証明書が削除されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p><strong>Remove-CsCertificate</strong> コマンドレットの実行手順に関する詳細情報を記録できるようにします。パラメーター値は、生成される HTML ファイルへの完全パスにする必要があります。例: -Report C:\Logs\Certificates.html。指定したファイルが既に存在する場合、新しい情報で自動的に上書きされます。</p></td>
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

なし。Remove-CsCertificate コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

なし。代わりに、**Remove-CsCertificate** コマンドレットは、Microsoft.Rtc.Management.Deployment.CertificateReference オブジェクトのインスタンスを削除します。

## 関連項目

#### その他のリソース

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

