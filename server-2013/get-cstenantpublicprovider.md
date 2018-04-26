---
title: Get-CsTenantPublicProvider
TOCTitle: Get-CsTenantPublicProvider
ms:assetid: 0d949ec2-206d-4979-a3be-a5578ae93ed3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994016(v=OCS.15)
ms:contentKeyID: 52056536
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantPublicProvider

 

_**トピックの最終更新日:** 2015-03-09_

Microsoft Lync Online のユーザーがサードパーティの IM やプレゼンス プロバイダー (Windows Live、AOL、Yahoo) のアカウントを持つユーザーと通信できるかどうかを示す情報を返します。

このコマンドレットは、Skype for Business Online でのみ使用できます。

## 構文

    Get-CsTenantPublicProvider -Tenant <String> [-Verbose]

## 例

## 例 1

例 1 に示すコマンドは、テナント ID "bf19b7db-6960-41e5-a139-2aa373474354" のテナントのパブリック プロバイダー情報を返します。

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Tenant パラメーターは省略可能です。次の構文を使用して、Get-CsTenantPublicProvider を呼び出すこともできます。

    Get-CsTenantPublicProvider

## 例 2

上記のコマンドは、テナント bf19b7db-6960-41e5-a139-2aa373474354 に割り当てられているすべてのパブリック プロバイダーの状態に関する詳細情報を返します。これを実行するために、まず **Get-CsTenantPublicProvider** コマンドレットを使用して、指定したテナントのパブリック プロバイダー情報を返します。次に、この情報を **Select-Object** コマンドレットにパイプ処理し、ExpandProperty パラメーターを使用して DomainPICStatus プロパティの値を "展開" します。プロパティを展開すると、そのプロパティに格納されているすべての値が読みやすい形式で画面に表示されます。

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

このようなコマンドは、Lync Server 2013 のハイブリッド展開で使用されます。

## 例 3

例 3 のコマンドは、例 2 のコマンドの変形です。ただし、例 3 では、DomainPICStatus プロパティの値の "展開" によって返されたパブリック プロバイダー情報を **Where-Object** コマンドレットにパイプ処理します。その後、**Where-Object** コマンドレットは、Status プロパティが Enabled に設定されているパブリック プロバイダーのみを選択します。その結果、使用可能なパブリック プロバイダーのみが表示されます。

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus | Where-Object {$_.Status -eq "Enabled"}

## 解説

パブリック プロバイダーとは、一般公衆向けの SIP 通信サービスを提供する組織のことです。パブリック プロバイダーとフェデレー ション関係を確立すると、そのプロバイダーがホストするアカウントを持つすべてのユーザーと、効率よくフェデレーションを確立でき ます。たとえば、Windows Live とフェデレーションを確立すると、組織のユーザーが、Windows Live のインスタント メッセージ アカ ウントを持つすべてのユーザーと、インスタント メッセージやプレゼンス情報を交換できるようになります。

Lync Online では、管理者が次のパブリック IM プロバイダーおよびプレゼンス プロバイダーの 1 つ以上とのフェデレーションを構成することができます。

  - Windows Live

  - AOL

  - Yahoo\!

管理者は、**Get-CsTenantPublicProvider** コマンドレットを使用して、それらのプロバイダー (存在する場合) のいずれでフェデレーションが有効になっているかを判断します。**Get-CsTenantPublicProvider** コマンドレットを呼び出すと、次のような情報が返されます。

    PublicProviderSet     DomainPicStatus
    ------------------    ------------------------
    True                  {Microsoft.Rtc.Management.Hosted.DomainPICStatus}

PublicProviderSet プロパティは、フェデレーションが 1 つ以上のパブリック プロバイダーで有効になっているかどうかを示します。PublicProviderSet が True である場合は、フェデレーションが少なくとも 1 つのプロバイダーで有効になっていることを意味します。PublicProviderSet が False である場合は、フェデレーションが 3 つのすべてのパブリック プロバイダー (Windows Live、AOL、Yahoo) で無効になっていることを示します。各プロバイダーの実際の状態を判断するには、次のコマンドを使用します。

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

パブリック プロバイダーの状態を有効にするだけでは、ユーザーはそのプロバイダーでアカウントを持つユーザーとインスタント メッセージやプレゼンス情報を交換できないことに注意してください。プロバイダー自体とのフェデレーションを有効にするだけでなく、管 理者はフェデレーション構成設定の AllowPublicUsers プロパティを True に設定する必要もあります。このプロパティを False に設定した場合、パブリック プロバイダー構成設定に関係なく、パブリック プロバイダーと通信することはできません。

詳しくは、 **Set-CsTenantFederationConfiguration** コマンドレットのヘルプ トピックをご覧ください。

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
<th>必須</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>パブリック プロバイダー設定が返されているテナント アカウントのグローバル一意識別子 (GUID) です。次に例を示します。</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を返すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Windows PowerShell のリモート セッションを使用していて、 Skype for Business Online のみに接続している場合、Tenant パラメーターを含める必要はありません。代わりに、接続情報に基づいてテナント ID が自動的に入力されます。Tenant パラメーターはハイブリッド展開で主に使用されます。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsTenantPublicProvider** コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

**Get-CsTenantPublicProvider** コマンドレットを実行すると、Microsoft.Rtc.Management.Hosted.TenantPICStatus オブジェクトのインスタンスが返されます。

## 関連項目

#### その他のリソース

[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md)

