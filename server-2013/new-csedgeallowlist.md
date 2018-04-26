---
title: New-CsEdgeAllowList
TOCTitle: New-CsEdgeAllowList
ms:assetid: 21a6d546-9e03-485c-b7ec-9deb778f2b01
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994023(v=OCS.15)
ms:contentKeyID: 52056556
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowList

 

_**トピックの最終更新日:** 2015-03-09_

ユーザーが通信できるドメインを、管理者が指定できます。**New-CsEdgeAllowList** コマンドレットは、Microsoft Lync Online のみで使用でき、また **New-CsEdgeDomainPattern** コマンドレットおよび **Set-CsTenantFederationConfiguration** コマンドレットと共に使用する必要があります。

## 構文

    New-CsEdgeAllowList [-AllowedDomain <PSListModifier>] [-Verbose]

## 例

## 例 1

例 1 に示すコマンドは、ドメイン fabrikam.com を、TenantId が "bf19b7db-6960-41e5-a139-2aa373474354" であるテナントの許可ドメインの一覧に割り当てます。これを実行するため、この例の最初のコマンドでは **New-CsEdgeDomainPattern** コマンドレットを使用して fabrikam.com 用のドメイン オブジェクトを作成します。このオブジェクトは変数 $x に格納されます。ドメイン オブジェクトが作成された後、**New-CsEdgeAllowList** コマンドレットを使用して、ドメイン fabrikam.com のみが含まれる新しい許可の一覧を作成します。

作成された許可ドメインの一覧により、この例の最後のコマンドでは **Set-CsTenantFederationConfiguration** コマンドレットを使用して、fabrikam.com を、指定したテナントの許可ドメインの一覧上の唯一のドメインとして構成できます。

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

Tenant パラメーターはハイブリッド展開のみで必要であることに注意してください。Skype for Business Online のみに接続されている場合、Tenant パラメーターは省略できます。

## 例 2

例 2 では、許可ドメインの一覧に複数のドメインを追加できます。これを行うには、(一覧に追加するドメインに 1 つずつ) **New-CsEdgeDomainPattern** コマンドレットを複数回呼び出し、別々の変数に結果のドメイン オブジェクトを格納します。AllowedDomain パラメーターを使用して、カンマで変数名を区切ることにより、**New-CsEdgeAllowList** コマンドレットによって作成された許可の一覧にこれらの各変数を追加できます。

$newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y

    $x = New-CsEdgeDomainPattern -Domain "contoso.com"
    $y = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## 例 3

例 3 では、許可ドメインの一覧からすべてのドメインを削除します。これを行うには、この例の最初のコマンドで **New-CsEdgeAllowList** コマンドレットを使用して許可ドメインの空白の一覧を作成します。これを行うには、AllowedDomain プロパティを null 値 ($Null) に設定します。**Set-CsTenantFederationConfiguration** コマンドレットと共に結果のオブジェクト参照 ($newAllowList) を使用して、TenantId が "bf19b7db-6960-41e5-a139-2aa373474354" であるテナントの許可ドメインの一覧からすべてのドメインを削除します。

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $Null
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## 解説

フェデレーションとは、他のドメインのユーザーと IM およびプレゼンスの情報を交換できるようにするサービスです。Lync Online では、フェデレーション構成設定を使用して次の制御を行うことができます。

  - 他のドメインのユーザーと通信できるかどうか、また通信できる場合は、どのドメインとの通信が許可されているか

  - Windows Live、AOL、および Yahoo などのパブリック IM およびプレゼンスのプロバイダー上にアカウントを持つユーザーと通信できるかどうか

フェデレーションは、部分的には、許可ドメインの一覧と禁止ドメインの一覧を使用して管理します。許可ドメインの一覧は、ユーザーが通信を許可されているドメインを指定します。禁止ドメインの一覧は、ユーザーが通信を許可されていないドメインを指定します。既定では、ユーザーは禁止の一覧にないすべてのドメインと通信できます。ただし、管理者はこの既定の設定を変更したり、許可ドメインの一覧にあるドメインへの接続を制限したりすることができます。

Lync Online では、許可の一覧または禁止の一覧を直接変更することはできません。たとえば、ドメイン名を表す文字列値を許可ドメインの一覧に渡す、次のようなコマンドを使用することはできません。

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

代わりに、**New-CsEdgeAllowAllKnownDomains** コマンドレットと **New-CsEdgeAllowList** コマンドレットのいずれかを使用してドメイン オブジェクトを作成し、そのドメイン オブジェクトを **Set-CsTenantFederationConfiguration** コマンドレットに渡す必要があります。禁止ドメインの一覧で明示的に指定されているドメインを除くすべてのドメインとの通信をユーザーに許可する場合、**New-CsEdgeAllowAllKnownDomains** コマンドレットを使用します。指定のドメインのコレクションへのユーザー通信を制限する場合は、**New-CsEdgeAllowList** コマンドレットを使用します。その場合、ユーザーは、許可ドメインの一覧にあるドメインとの通信のみが許可されます。

許可ドメインの一覧に 1 つのドメイン (fabrikam.com) を追加するには、次のような一連のコマンドを使用する必要があります。

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

このコマンドで実行が完了した時点で、ユーザーは、fabrikam.com ドメインのユーザーとの通信のみが許可されます。

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
<td><p><em>AllowedDomain</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>許可ドメインの一覧に追加する新しいドメイン (または一連のドメイン) へのオブジェクト参照です。ドメイン オブジェクト参照は、<strong>New-CsEdgeDomainPattern</strong> コマンドレットを使用して作成する必要があります。オブジェクト参照をカンマで区切ることにより、複数のドメイン オブジェクトを追加することができます。次に例を示します。</p>
<p>-AllowedDomain $x,$y</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**New-CsEdgeAllowList** コマンドレットはパイプライン処理された入力を受け入れません。

## 戻り値の種類

**New-CsEdgeAllowList** コマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowList オブジェクトの新しいインスタンスが作成されます。

## 関連項目

#### その他のリソース

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

