---
title: Test-CsCertificateConfiguration
TOCTitle: Test-CsCertificateConfiguration
ms:assetid: 8086bdf7-d283-4666-9f6c-0d5a3a31b3a6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398647(v=OCS.15)
ms:contentKeyID: 48272701
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsCertificateConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

ローカル コンピューターで使用中の Lync Server 証明書に関する情報を戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsCertificateConfiguration [-Report <String>]

## 例

## 例 1

例 1 に示すコマンドは、Lync Server が (ローカル コンピューター上で) 現在使用中の証明書に関する情報を戻します。

    Test-CsCertificateConfiguration

## 例 2

例 2 に示すコマンドは、例 1 に示すコマンドの変化形です。ただしこの場合、Report パラメーターを使用して **Test-CsCertificateConfiguration** コマンドレットの実行時に生成された出力ファイルのファイル パス (C:\\Logs\\Certificates.xml) を指定します。

    Test-CsCertificateConfiguration -Report "C:\Logs\Certificates.xml"

## 解説

**Test-CsCertificateConfiguration** コマンドレットは、"代理トランザクション" の一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信など、一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) のようなアプリケーションから自動で実行することもできます。

**Test-CsCertificateConfiguration** コマンドレットは、Lync Server で使用中の証明書に関する情報を戻します。**Test-CsCertificateConfiguration** コマンドレットは、主に証明書ウィザードで使用するよう意図されています。管理者は、**Get-CsCertificate** コマンドレットを使用して証明書情報を取得することをお勧めします。

このコマンドレットを実行できるユーザー: このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsCertificateConfiguration"}

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
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレット実行時に作成されるログ ファイルのファイル パスを指定できるようにします。次に例を示します。-Report &quot;C:\Logs\Certificates.html&quot;。このファイルが既に存在する場合は、コマンドレットの実行時に上書きされます。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsCertificateConfiguration** コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

**Test-CsCertificateConfiguration** コマンドレットを実行すると、Microsoft.Rtc.Management.Deployment,CertificateExists オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Get-CsCertificate](get-cscertificate.md)

