---
title: Set-CsTenantFederationConfiguration
TOCTitle: Set-CsTenantFederationConfiguration
ms:assetid: e13c2f55-7a68-4174-a0da-5eec8c65f64c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994080(v=OCS.15)
ms:contentKeyID: 52056734
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantFederationConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

Microsoft Lync Online テナントのフェデレーション構成設定を管理します。これらの設定を使用して、ユーザーが通信できるドメイン (ある場合) を決定します。

**Set-CsTenantFederationConfiguration** コマンドレットは、Skype for Business Online のみで使用できます。

## 構文

    Set-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Force] [-Verbose] [-WhatIf] [-Confirm]Set-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Instance <PSObject>] [-Force] [-Verbose] [-WhatIf] [-Confirm]

## 例

## 例 1

例 1 のコマンドを実行すると、TenantId が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントのパブリック プロバイダーとの通信が無効になります。

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowPublicUsers $False

Tenant パラメーターはオプションです。このパラメーターを設定しないと、Windows PowerShell によって、接続情報に基づく正しいテナント ID が自動的に挿入されます。

## 例 2

例 2 は、組織のすべてのテナントで、パブリック プロバイダーの通信を無効にする方法を示しています。この操作を実行するには、まずコマンドで **Get-CsTenant** コマンドレットを呼び出し、すべての使用可能なテナントのコレクションを返します。次にこのコレクションを **Select-Object** コマンドレットにパイプ処理し、コレクション内の各項目の TenantId プロパティのみを抽出します。次に、テナント ID のコレクションを **ForEach-Object** コマンドレットにパイプ処理します。F**orEach-Object** コマンドレットを実行して各テナント ID を取得し、その ID に対して **Set-CsTenantFederationConfiguration** コマンドレットを実行し、各テナントの AllowPublicUsers プロパティを False ($False) に設定します。

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantId -AllowPublicUsers $False}

## 例 3

例 3 では、TenantId が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントの禁止ドメイン リストに、fabrikam.com というドメインが唯一のドメインとして割り当てられています。この操作を実行するため、例の最初のコマンドで **New-CsEdgeDomainPattern** コマンドレットを使用して fabrikam.com の新しいドメイン オブジェクトを作成しています。このドメイン オブジェクトは $x という名前の変数に保存されます。

次に例の 2 番目のコマンドで、**Set-CsTenantFederationConfiguration** コマンドレットを使用して禁止ドメイン リストを更新します。Replace メソッドを使用すると、既存の禁止ドメイン リストが (fabrikam.com というドメインのみを含む) 新しいリストに置き換えられます。

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Replace=$x}

## 例 4

例 4 のコマンドでは、TenantID が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントの禁止ドメイン リストから、fabrikam.com を削除しています。この操作を実行するため、例の最初のコマンドでは、**New-CsEdgeDomainPattern** コマンドレットを使用して fabrikam.com の新しいドメイン オブジェクトを作成します。作成されたドメイン オブジェクトは $x という名前の変数に保存されます。

次に例の 2 番目のコマンドで、**Set-CsTenantFederationConfiguration** コマンドレットと Remove メソッドを使用して、指定したテナントの禁止ドメイン リストから fabrikam.com を削除します。

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Remove=$x}

## 例 5

例 5 のコマンドでは、TenantId が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントの禁止ドメイン リストに fabrikam.com を追加しています。禁止ドメインを新しく追加するため、例の最初のコマンドで **New-CsEdgeDomainPattern** コマンドレットを使用して fabrikam.com のドメイン オブジェクトを作成します。このオブジェクトは $x という名前の変数に保存されます。

ドメイン オブジェクトの作成後に、2 番目のコマンドで **Set-CsTenantFederationConfiguration** コマンドレットと Add メソッドを使用して、禁止ドメイン リストのいずれかの既存ドメインに fabrikam.com を追加します。

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Add=$x}

## 例 6

例 6 は、所定のテナントの禁止ドメイン リストに割り当てられているすべてのドメインを削除する方法を示しています。この操作を実行するには、BlockedDomains パラメーターを含めてパラメーター値を NULL ($Null) に設定するだけです。このコマンドが完了すると、TenantID が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントの禁止ドメイン リストが消去されます。

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $Null

## 解説

フェデレーションとは、IM やプレゼンス情報を他のドメインのユーザーとやり取りできるようにするサービスです。Lync Online では、管理者がフェデレーション構成設定を使用して次の内容を管理できます。

  -   
    他のドメインのユーザーと通信できるか。通信できる場合、どのドメインのユーザーと通信できるか。

  -   
    Windows Live、AOL、Yahoo などの IM およびプレゼンスのパブリック プロバイダーのアカウントを持つユーザーと通信できるか。

管理者は **Set-CsTenantFederationConfiguration** コマンドレットを使用して、他のドメインやパブリック プロバイダーとのフェデレーションを有効または無効にすることができます。またこのコマンドレットを使用して、ユーザーが通信できる (または通信できない) ドメインを明示的に指定できます。ただし、ユーザーが通信できる (または通信できない) IM およびプレゼンスのパブリック プロバイダーを管理者が指定するには、**Set-CsTenantPublicProvider** コマンドレットを使用する必要があります。

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
<td><p><em>AllowedDomains</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.IAllowedDomainsChoice</p></td>
<td><p>ユーザーが通信できるドメインを示すドメイン オブジェクト (<strong>New-CsEdgeAllowList</strong> コマンドレットか <strong>New-CsEdgeAllowAllKnownDomains</strong> コマンドレットで作成) です。<strong>New-CsEdgeAllowAllKnownDomains</strong> コマンドレットを使用すると、禁止ドメイン リストに表示されていない任意のドメインと通信できます。<strong>New-CsEdgeAllowList</strong> コマンドレットを使用すると、許可ドメイン リストに追加されているドメインのみと通信できます。</p>
<p>文字列値を AllowedDomains パラメーターに直接渡すことはできません。代わりに <strong>New-CsEdgeAllowList</strong> コマンドレットか <strong>New-CsEdgeAllowAllKnownDomains</strong> コマンドレットを使用してオブジェクト参照を作成し、そのオブジェクト参照値をパラメーター値として使用します。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowFederatedUsers</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True (既定値) に設定すると、他のドメインのユーザーと通信できる可能性があります。このプロパティを False に設定すると、AllowedDomains プロパティや BlockedDomains プロパティに割り当てられている値に関係なく、他のドメインのユーザーと通信できません。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPublicUsers</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True (既定値) に設定すると、Windows Live、Yahoo、AOL などの IM およびプレゼンスのパブリック プロバイダーにアカウントを持つユーザーと通信できる可能性があります。ユーザーが実際に通信できるパブリック プロバイダーのコレクションは、Set-CsTenantPublicProvider コマンドレットで管理されます。</p></td>
</tr>
<tr class="even">
<td><p><em>BlockedDomains</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>AllowedDomains プロパティを AllowAllKnownDomains に設定すると、禁止ドメイン リストに表示されているドメイン以外の任意のドメインのユーザーと通信できます。AllowedDomains プロパティを AllowAllKnownDomains に設定していないと、禁止リストは無視され、許可ドメイン リストに明示的に追加されているドメインのみと通信できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>変更するテナント フェデレーション構成設定のコレクションを指定します。各テナントはフェデレーション設定の 1 つのグローバル コレクションに限定されるため、<strong>Set-CsTenantFederationConfiguration</strong> コマンドレットを呼び出す際にこのパラメーターを含める必要はありません。Identity パラメーターを使用する場合は、Tenant パラメーターも含める必要があります。次に例を示します。</p>
<p>Set-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。</p></td>
</tr>
<tr class="odd">
<td><p><em>SharedSipAddressSpace</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True に設定すると、Lync Online に所属するユーザーが Lync Server の社内版に所属するユーザーと同じ SIP ドメインを使用します。既定値は False です。つまり、これら 2 種類のユーザーの SIP ドメインは異なるということです。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Guid</p></td>
<td><p>フェデレーション設定が変更されているテナント アカウントのグローバル識別子 (GUID) です。次に例を示します。</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を返すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Windows PowerShell のリモート セッションを使用しており、Skype for Business Online だけに接続している場合は、Tenant パラメーターを含める必要はありません。代わりに、接続情報に基づいてテナント ID が自動的に入力されます。Tenant パラメーターは主にハイブリッド展開用です。</p></td>
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

**Set-CsTenantFederationConfiguration** コマンドレットでは、Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings オブジェクトのパイプライン処理されたインスタンスを使用できます。

## 戻り値の種類

なし。ただし **Set-CsTenantFederationConfiguration** コマンドレットを実行すると Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings オブジェクトの既存インスタンスが変更されます。

## 関連項目

#### その他のリソース

[Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md)

