---
title: Exchange ユニファイド メッセージングとホスト ボイスメールの管理
TOCTitle: Exchange ユニファイド メッセージングとホスト ボイスメールの管理
ms:assetid: 844bf8d5-e093-4dcd-abcf-48dc70e8c73c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362822(v=OCS.15)
ms:contentKeyID: 56270107
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Exchange ユニファイド メッセージングとホスト ボイスメールの管理

 

_**トピックの最終更新日:** 2015-06-22_

次のコマンドレットを使用して、Exchange Unified Messaging (UM) とホスト ボイス メール ポリシーを管理できます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンドレット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="get-csexumcontact.md">Get-CsExUmContact</a></p>
<p><a href="new-csexumcontact.md">New-CsExUmContact</a></p>
<p><a href="remove-csexumcontact.md">Remove-CsExUmContact</a></p>
<p><a href="set-csexumcontact.md">Set-CsExUmContact</a></p></td>
<td><p>Exchange UM がホスト サービスである場合に、自動応答とサブスクライバー アクセス サービスで使用される連絡先オブジェクトを作成、管理します。</p>
<p>Skype for Business Online は Exchange UM と連携して、音声関連の機能 (自動応答やサブスクライバー アクセスなど) を提供します。自動応答は、呼び出しへの自動応答や適切な人への転送を行うための機能です。サブスクライバー アクセスは、Exchange UM への接続や、メール、音声メッセージ、連絡先、予定表の情報の取得を行うための機能です。</p>
<p>Exchange UM がホスト型サービスとして提供される場合、Windows PowerShell を使用して自動応答サービスやサブスクライバー アクセス サービスの連絡先オブジェクトを作成する必要があります。これらのオブジェクトは、CsExUmContact コマンドレットを使用して作成、管理されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cshostedvoicemailpolicy.md">Get-CsHostedVoicemailPolicy</a></p>
<p><a href="grant-cshostedvoicemailpolicy.md">Grant-CsHostedVoicemailPolicy</a></p></td>
<td><p>組織で使用するホスト型ボイスメールのポリシーを管理します。ホスト型ボイスメールのポリシーでは、Exchange UM サービスへの不在着信の転送方法を指定します。これらのポリシーは、Exchange UM ホスト型ボイスメールが有効なユーザーのみに影響します。ユーザーでホスト型ボイスメールが有効であるかどうかを確認するには、Windows PowerShell プロンプトから次のようなコマンドを実行します。</p>
<pre><code>Get-CsOnlineUser -Identity &quot;kenmyer@litwareinc.com&quot; | Select-Object HostedVoiceMail</code></pre></td>
</tr>
</tbody>
</table>


Skype for Business Online 管理センターを使用して Exchange UM の設定やホスト型ボイスメールのポリシーを管理することはできません。

## 関連項目

#### 概念

[Lync Online のコマンドレット](the-skype-for-business-online-cmdlets.md)  
[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

