---
title: 外部のユーザーや組織との通信の管理
TOCTitle: 外部のユーザーや組織との通信の管理
ms:assetid: 8a64f0fe-1e79-47d8-835e-548d7ac0757e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362813(v=OCS.15)
ms:contentKeyID: 56270112
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 外部のユーザーや組織との通信の管理

 

_**トピックの最終更新日:** 2015-06-22_

次のコマンドレットを使用して、外部ドメインやパブリック インスタント メッセージング (IM) プロバイダーとのフェデレーションを管理できます。


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
<td><p><a href="new-csedgeallowallknowndomains.md">New-CsEdgeAllowAllKnownDomains</a></p></td>
<td><p>ユーザーは、禁止ドメイン リストで指定されているドメイン以外のすべてのドメインと通信できます。</p>
<p>フェデレーションは、IM やプレゼンス情報を他のドメインのユーザーとやり取りできるサービスです。通常は、管理者が許可リストと禁止リストを使用して、ユーザーが通信できる外部ドメインを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="new-csedgeallowlist.md">New-CsEdgeAllowList</a></p></td>
<td><p>ユーザーの通信を指定したドメインのコレクションに限定します。</p>
<p>ユーザーは、許可されたドメイン リストに表示されるドメインのみと通信できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="new-csedgedomainpattern.md">New-CsEdgeDomainPattern</a></p></td>
<td><p>ドメインの許可リストや禁止リストを変更します。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantfederationconfiguration.md">Get-CsTenantFederationConfiguration</a><br />
<a href="set-cstenantfederationconfiguration.md">Set-CsTenantFederationConfiguration</a></p></td>
<td><p>他のドメインや、パブリック プロバイダーとのフェデレーションを有効、無効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-cstenanthybridconfiguration.md">Get-CsTenantHybridConfiguration</a><br />
<a href="set-cstenanthybridconfiguration.md">Set-CsTenantHybridConfiguration</a></p></td>
<td><p>ハイブリッド構成設定に適切な値を割り当てます。</p>
<p>ハイブリッドまたは &quot;分割ドメイン&quot; の展開では、組織の一部のユーザー アカウントが Skype for Business Online にあり、同時にその他のユーザー アカウントが Lync Server 2013 にあります。既定では、Skype for Business Online に所属するユーザーはエンタープライズ VoIP の機能をすべて使用することはできません。Skype for Business Online ユーザーがこのようなエンタープライズ VoIP 機能を使用できるようにするには、管理者がハイブリッド構成値に適切な値を割り当てる必要があります。これらの値は、<strong>CsTenantHybridConfiguration</strong> コマンドレットでのみ管理できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantpublicprovider.md">Get-CsTenantPublicProvider</a><br />
<a href="set-cstenantpublicprovider.md">Set-CsTenantPublicProvider</a></p></td>
<td><p>パブリック プロバイダーとのフェデレーションを管理します。</p>
<p>パブリック プロバイダーとは、一般の SIP 通信サービスを提供する組織です。パブリック プロバイダーとフェデレーション関係を確立すると、そのプロバイダーがホストするアカウントを持つすべてのユーザーと、効率的にフェデレーションを確立できます。</p></td>
</tr>
</tbody>
</table>


また Skype for Business Online 管理センターを使用して、フェデレーションされたドメインとパブリック プロバイダーのフェデレーション設定を管理できます。

![Lync Online 管理センター組織の設定](images/Dn362813.f860d03f-5906-49b0-bcc7-7634afe7005e(OCS.15).png "Lync Online 管理センター組織の設定")

## 関連項目

#### 概念

[Lync Online のコマンドレット](the-skype-for-business-online-cmdlets.md)  
[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

