---
title: New-CsEdgeAllowAllKnownDomains
TOCTitle: New-CsEdgeAllowAllKnownDomains
ms:assetid: f9416909-c328-41b3-9215-7ebd091b0ca0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994088(v=OCS.15)
ms:contentKeyID: 52056754
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowAllKnownDomains

 

_**トピックの最終更新日:** 2015-03-09_

禁止ドメイン リストに含まれているドメインを除く、すべてのドメインとの Microsoft Lync Online フェデレーションを有効にします。

このコマンドレットは、Skype for Business Online でのみ使用できます。

## 構文

    New-CsEdgeAllowAllKnownDomains [-Verbose]

## 例

## 例 1

例 1 に示す 2 つのコマンドは、Identity が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントに対してフェデレーション設定を構成し、既知のドメインすべてを許可します。これを行うために、例の最初のコマンドは、**New-CsEdgeAllowAllKnownDomains** コマンドレットを使用して Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains オブジェクトのインスタンスを作成します。このインスタンスは、変数 $x に格納されます。2 番目のコマンドでは、**Set-CsTenantFederationConfiguration** コマンドレットと AllowedDomains パラメーターを呼び出します。$x をパラメーター値として使用すると、既知のドメインすべてを許可するようにフェデレーション設定が構成されます。

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

## 例 2

例 2 は、禁止ドメイン リストで明示的に指定されていないすべてのドメインとの通信を許可するようにすべてのテナントを構成する方法を示しています。これを行うために、例の最初のコマンドは、**New-CsEdgeAllowAllKnownDomains** コマンドレットを使用して AllowAllKnownDomains オブジェクトのインスタンスを作成します。オブジェクトは変数 $x に格納されます。

例の 2 番目のコマンドは、**Get-CsTenant** コマンドレットを使用して使用可能なすべてのテナントのコレクションを返します。次に、このコレクションを **ForEach-Object** コマンドレットにパイプ処理します。その後、**ForEach-Object** コマンドレットは、コレクション内の各テナントに対して **Set-CsTenantFederationConfiguration** コマンドレットを実行し、既知のドメインすべてを許可するように AllowedDomains プロパティを構成します。

    $x = New-CsEdgeAllowAllKnownDomains
    Get-CsTenant | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantID -AllowedDomains $x}

## 解説

フェデレーションは、ユーザーが他のドメインのユーザーと IM およびプレゼンス情報を交換できるようにするサービスです。Lync Online では、管理者はフェデレーション構成設定を使用して以下を管理することができます。

  - ユーザーが他のドメインのユーザーと通信できるかどうか、また通信できる場合は通信先として可能なドメイン。

  - ユーザーが Windows Live、AOL、Yahoo などのパブリック IM プロバイダーおよびプレゼンス プロバイダーのアカウントを持つユーザーと通信できるかどうか。

フェデレーションは、一部分においては、許可ドメイン リストと禁止ドメイン リストを使用して管理されます。許可ドメイン リストでは、ユーザーが通信できるドメインが指定され、禁止ドメイン リストでは、ユーザーが通信できないドメインが指定されます。既定では、ユーザーは禁止リストにないドメインと通信することができます。ただし、管理者はこの既定の設定を変更して、通信を許可ドメイン リストにあるドメインに制限することができます。

Lync Online では、許可リストまたは禁止リストを直接変更できません。たとえば、ドメイン名を表す文字列値を許可ドメイン リストに渡す次のようなコマンドは使用できません。

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

代わりに、**New-CsEdgeAllowAllKnownDomains** コマンドレットまたは **New-CsEdgeAllowList** コマンドレットを使用してドメイン オブジェクトを作成し、そのドメイン オブジェクトを **Set-CsTenantFederationConfiguration** コマンドレットに渡す必要があります。禁止ドメイン リストで明示的に指定されているドメインを除く、すべてのドメインと通信できるようにする場合には、**New-CsEdgeAllowAllKnownDomains** コマンドレットを使用します。ユーザー通信を、指定したドメインのコレクションに制限する場合には、N**ew-CsEdgeAllowList** コマンドレットを使用します。この場合、ユーザーは、許可ドメイン リストに示されているドメインと通信することができます。

既知のドメインすべてとのフェデレーションを構成するには、次のような一連のコマンドを使用します。

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

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
<td><p>このコマンドレットで使用できるのは、一般的な Windows PowerShell パラメーターのみです。</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**New-CsEdgeAllowAllKnownDomains** コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

**New-CsEdgeAllowAllKnownDomains** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains オブジェクトの新しいインスタンスを作成します。

## 関連項目

#### その他のリソース

[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

