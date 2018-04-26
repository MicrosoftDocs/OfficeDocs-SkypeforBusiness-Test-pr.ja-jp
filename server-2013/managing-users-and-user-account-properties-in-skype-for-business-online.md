---
title: ユーザーおよびユーザー アカウント プロパティの管理
TOCTitle: ユーザーおよびユーザー アカウント プロパティの管理
ms:assetid: 5d13ab15-0e12-4bd0-a970-f130de980404
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362790(v=OCS.15)
ms:contentKeyID: 56270083
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ユーザーおよびユーザー アカウント プロパティの管理

 

_**トピックの最終更新日:** 2015-06-22_

次のコマンドレットで Skype for Business Online のユーザー アカウントを管理します。


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
<td><p><a href="get-csonlineuser.md">Get-CsOnlineUser</a></p></td>
<td><p>Skype for Business Online テナントに所属するアカウントを所有するユーザーについての情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csuseracp.md">Get-CsUserAcp</a><br />
<a href="remove-csuseracp.md">Remove-CsUserAcp</a><br />
<a href="set-csuseracp.md">Set-CsUserAcp</a></p></td>
<td><p>個々のユーザーに対して、電話会議プロバイダーの割り当て、変更、または割り当て解除を行うことができます。</p>
<p>電話会議プロバイダーはサードパーティの企業で、リアルタイム通訳、トランスクリプション、オペレーターによる各電話会議のリアルタイム サポートなど、高度なサービスが含まれる会議サービスを組織に提供します。</p>
<p>これらのコマンドレットは、ユーザーに割り当てられ利用可能である電話会議プロバイダーに関する情報を返しません。その情報を取得するには、代わりに次のコマンドを実行します。</p>
<pre><code>Get-CsAudioConferencingProvider</code></pre></td>
</tr>
</tbody>
</table>



> [!WARNING]
> Set-CsUser コマンドレットは、Skype for Business Online の管理者が使用できる一連のコマンドレットにも含まれています。ただし、現時点では、AudioVideoDisabled パラメーターの設定を除き、Set-CsUser を使用して Skype for Business Onlineを管理することはできません。それ以外のパラメーターを使用してコマンドレットを実行しようとすると、エラーになり次のようなエラー メッセージが表示されます。<BR>"SipAddress" を設定できません。このパラメーターは Remote Tenant PowerShell 内では制限されています。



また、Skype for Business Online 管理センターを使用して、ユーザー アカウントに音声会議プロバイダーを割り当てる (またはユーザー アカウントから割り当てを解除する) こともできます。

![Lync 管理センターのダイヤルイン会議のプロパティ](images/Dn362790.0c61f0c2-8aef-4020-a0a8-02580d43092a(OCS.15).png "Lync 管理センターのダイヤルイン会議のプロパティ")

## 関連項目

#### 概念

[Lync Online のコマンドレット](the-skype-for-business-online-cmdlets.md)  
[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

