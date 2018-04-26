---
title: New-CsEdgeDomainPattern
TOCTitle: New-CsEdgeDomainPattern
ms:assetid: 653bc148-c22b-4ad4-afdd-17aaeaa299d2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994040(v=OCS.15)
ms:contentKeyID: 52056623
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeDomainPattern

 

_**トピックの最終更新日:** 2015-03-09_

このコマンドレットを使用して、フェデレーションで有効になっている一連のドメインやフェデレーションで無効になっている一連のドメインに対して追加または削除するドメインを指定します。許可ドメイン リストまたは禁止ドメイン リストを変更するときに、**New-CsEdgeDomainPattern** コマンドレットを使用する必要があります。これらのリストのいずれかの管理に使用するコマンドレットに、文字列値 ("fabrikam.com" など) を直接渡すことはできません。

**New-CsEdgeDomainPattern** コマンドレットは、Skype for Business Online でのみ使用できます。

## 構文

    New-CsEdgeDomainPattern -Domain <String> [-Verbose]

## 例

## 例 1

例 1 は、指定したテナントの禁止ドメインに 1 つのドメインを割り当てる方法を示しています。これを行うために、例の 1 番目のコマンドでは、ドメイン fabrikam.com のドメイン オブジェクトを作成します。これを実行するため、**New-CsEdgeDomainPattern** コマンドレットを呼び出して、得られたドメイン オブジェクトを変数 $x に格納します。2 番目のコマンドでは、**Set-CsTenantFederationConfiguration** コマンドレットと BlockedDomains パラメーターを使用して、TenantId が "bf19b7db-6960-41e5-a139-2aa373474354" のテナントによって禁止される唯一のドメインとして fabrikam.com を構成します。

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

## 解説

フェデレーションは、ユーザーが他のドメインのユーザーと IM およびプレゼンス情報を交換できるようにするサービスです。Skype for Business Online では、管理者はフェデレーション構成設定を使用して以下を管理することができます。

  - ユーザーが他のドメインのユーザーと通信できるかどうか、また通信できる場合は通信先として可能なドメイン。

  - ユーザーが Windows Live、AOL、Yahoo などのパブリック IM プロバイダーおよびプレゼンス プロバイダーのアカウントを持つユーザーと通信できるかどうか。

フェデレーションは、一部分においては、許可ドメインと禁止ドメインを使用して管理されます。許可ドメイン リストでは、ユーザーが通信できるドメインが指定され、禁止ドメイン リストでは、ユーザーが通信できないドメインが指定されます。既定では、ユーザーは禁止リストにないドメインと通信することができます。ただし、管理者はこの既定の設定を変更して、通信を許可ドメイン リストにあるドメインに制限することができます。

Skype for Business Online では、許可リストまたは禁止リストを直接変更することはできません。たとえば、次のようなコマンドを使用して、ドメイン名を表す文字列値を禁止ドメイン リストに渡すことはできません。

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains "fabrikam.com"

代わりに、**New-CsEdgeDomainPattern** コマンドレットを使用してドメイン オブジェクトを作成し、そのドメイン オブジェクトを変数 (この例では、$x) に格納してから、その変数名を禁止ドメイン リストに渡す必要があります。

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

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
<td><p><em>Domain</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>許可リストに追加されるドメインの完全修飾ドメイン名です。次に例を示します。</p>
<p>-Domain &quot;fabrikam.com&quot;</p>
<p>ドメイン名を指定する際、ワイルドカードを使用することはできません。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**New-CsEdgeDomainPattern** コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

**New-CsEdgeDomainPattern** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DomainPattern オブジェクトの新しいインスタンスを作成します。

## 関連項目

#### その他のリソース

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

