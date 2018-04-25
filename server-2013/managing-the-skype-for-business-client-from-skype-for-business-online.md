---
title: Lync クライアントの管理
TOCTitle: Lync クライアントの管理
ms:assetid: d1ccc7b6-99ff-4ffd-bd29-9088fb8fe837
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362847(v=OCS.15)
ms:contentKeyID: 56270135
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync クライアントの管理

 

_**トピックの最終更新日:** 2015-06-22_

次のコマンドレットで Lync クライアントを管理します。


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
<td><p><a href="get-csimfilterconfiguration.md">Get-CsImFilterConfiguration</a></p></td>
<td><p>組織で使用している URI の制限事項に関する情報を取得します。</p>
<p>インスタント メッセージの送信時にメッセージのテキストに URI を埋め込んで、会話の他の参加者が特定の Web サイトの参照や共有を行えるようにします。Skype for Business Online を構成して、特定のプレフィックスを含むハイパーリンクを禁止したり、非アクティブにしたりすることができます。このように構成すると、参加者はリンクをクリックして URI の参照先のサイトを表示できないため、リンクを手動でブラウザーにコピーして貼り付ける必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cspresencepolicy.md">Get-CsPresencePolicy</a></p></td>
<td><p>プレゼンス サブスクリプションの 2 つの重要な面 (要求されたサブスクライバーとカテゴリ サブスクリプション) に関する情報が返されます。</p>
<p>他のユーザーの連絡先リストに追加されると、既定の動作では、リストに追加されたユーザーにそのことを知らせるポップアップ通知が表示されます。ポップアップを閉じるまで、各通知は要求されたサブスクライバーとしてカウントされます。</p>
<p>カテゴリ サブスクリプションは、特定カテゴリの情報の要求 (予定表データを要求するアプリケーションなど) を示します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csprivacyconfiguration.md">Get-CsPrivacyConfiguration</a><br />
<a href="set-csprivacyconfiguration.md">Set-CsPrivacyConfiguration</a></p></td>
<td><p>Skype for Business Online で既定のプライバシー値を構成する一方、ユーザーがこれらの値を変更できるようにします。</p>
<p>Skype for Business Online では、多くのプレゼンス情報を他のユーザーと共有できます。自分の写真を公開し、詳しい場所情報を提供し、(連絡先リストのユーザーだけでなく) 組織のすべてのユーザーがプレゼンス情報を自動的に使用できるようにします。管理者は <strong>CsPrivacyConfiguration</strong> コマンドレットを使用して Skype for Business Online で既定のプライバシー値を構成する一方、ユーザーにこれらの値の変更を許可することができます。</p></td>
</tr>
</tbody>
</table>


また、Skype for Business Online 管理センターでプライバシー構成設定のサブセットを管理することもできます。

![Lync 管理センター、プレゼンス プライバシー モードの設定](images/Dn362847.eb206b74-844d-4a7b-b1b3-0cfcb6e3614b(OCS.15).png "Lync 管理センター、プレゼンス プライバシー モードの設定")

## 関連項目

#### 概念

[Lync Online のコマンドレット](the-skype-for-business-online-cmdlets.md)  
[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

