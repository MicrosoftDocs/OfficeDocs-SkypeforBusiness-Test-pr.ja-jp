---
title: Get-CsTenant
TOCTitle: Get-CsTenant
ms:assetid: 7b642117-5ca7-4a5b-bca7-16b0ae694ae2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994044(v=OCS.15)
ms:contentKeyID: 52056627
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenant

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用するために構成されているSkype for Business Online テナントに関する情報を戻します。テナントとは、オンライン ユーザーのグループを表します。多くの場合、必要なテナントは 1 つだけです。ただし、さまざまなユーザー グループで管理ニーズが異なる場合、Skype for Business Online では、複数のテナントがある 1 つの組織をサポートします。

Get-CsTenant は、Skype for Business Online でのみ使用できます。

## 構文

    Get-CsTenant [[-Identity] <OUIdParameter>] [-Filter <String>] [-ResultSize <Unlimited`1>] [-Verbose]

## 例

## 例 1

例 1 に示すコマンドは、組織で使用するために構成されているすべてのテナントに関する情報を戻します。

    Get-CsTenant

## 例 2

例 2 では、1 つのテナント (Identity が "bf19b7db-6960-41e5-a139-2aa373474354" のテナント) に関する情報が戻されます。

    Get-CsTenant -Identity "bf19b7db-6960-41e5-a139-2aa373474354"

## 例 3

上記のコマンドは、1 つのテナントに関する情報を戻すための別の方法を示しています。例では、これを実行するために、Filter パラメーターとフィルター値 {DisplayName –eq "Fabrikam"} を指定します。次の構文は、表示名が Fabrikam のテナントに関する情報のみを戻します。

    Get-CsTenant -Filter {DisplayName -eq "Fabrikam"}

## 例 4

例 4 に示すコマンドは、ServiceInstance が "LitwareincCommunicationsOnline/San Antonio" と等しいすべてのテナントに関する情報を戻します。これを行うために、このコマンドでは、Filter パラメーターとフィルター値 {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"} が指定されています。そのフィルター値により、戻されるデータが、ServiceInstance プロパティが "LitwareincCommunicationsOnline/San Antonio" と等しい (-eq) テナントに制限されます。

    Get-CsTenant -Filter {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}

## 例 5

例 5 では、国または地域の表示名が Australia と等しいすべてのテナントに関する情報を戻します。これを行うために、Filter パラメーターとパラメーター値 {CountryOrRegionDisplayName -eq "Australia"} を使用します。

    Get-CsTenant -Filter {CountryOrRegionDisplayName -eq "Australia"}

## 解説

Skype for Business Online では、テナントは、サービスに属するアカウントを持つユーザーのグループを表します。多くの組織では、組織のすべてのユーザー アカウントを保持するために必要なテナントは 1 つだけです。ただし、多くの場合、Skype for Business Online の管理はテナントに応じて実行されます。つまり、同じテナント内のすべてのユーザーには、同じ音声ポリシー、フェデレーション構成設定などが割り当てられます。ユーザーの管理に複数の方法を使用する必要がある場合、複数のテナントを使用して、それぞれに独自のポリシーおよび設定のコレクションを割り当てることもできます。

作成するテナント数に関係なく、**Get-CsTenant** コマンドレットを使用してこれらのテナントに関する情報を戻すことができます。

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
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>Active Directory 属性を使用して、完全な Active Directory 識別名を指定しなくても、データを戻すことができます。たとえば、テナント表示名を使用してテナントを取得するには、次のような構文を使用します。</p>
<p>Get-CsTenant –Filter {DisplayName –eq &quot;FabrikamTenant&quot;}</p>
<p>Fabrikam ドメインを使用するすべてのテナントを戻すには、次の構文を使用します。</p>
<p>Get-CsTenant –Filter {Domains –like &quot;*fabrikam*&quot;}</p>
<p>Filter パラメーターでは、Where-Object コマンドレットによって使用されるのと同じ Windows PowerShell フィルター処理構文を使用します。</p>
<p>Identity パラメーターと Filter パラメーターの両方を同じコマンド内で使用することはできません。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>テナントの Active Directory 識別名です。次に例を示します。</p>
<p>-Identity &quot;OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=litwareinc,dc=com&quot;</p>
<p>Identity パラメーターまたは Filter パラメーターを使用しない場合、<strong>Get-CsTenant</strong> コマンドレットは、すべてのテナントに関する情報を戻します。</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited`1</p></td>
<td><p>このコマンドレットによって戻されるレコード数を制限できます。たとえば、7つのテナントを戻すには (フォレスト内のテナント数に関わらず)、ResultSize パラメーターを追加してパラメーター値を 7 に設定します。ただし、どの 7 つのテナントを戻すかを指定する方法はありません。</p>
<p>結果サイズは、0 ～ 2147483647 の範囲の整数に設定できます。 0 に設定すると、コマンドは実行されますが、データは戻りません。テナントを 7 に設定しても、フォレスト内に 3 つのテナントしかない場合、コマンドはその 3 つのテナントを戻し、エラーなしで完了します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

**Get-CsTenant** コマンドレットは、Microsoft.Rtc.Management.ADConnect.Schema.TenantObject オブジェクトのパイプライン処理されたインスタンスと、Skype for Business Online テナント (たとえば、"OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=vdomain,dc=com") の ID を表す文字列値を受け入れます。

## 戻り値の種類

**Get-CsTenant** コマンドレットは、Microsoft.Rtc.Management.ADConnect.Schema.TenantObject オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Get-CsOnlineUser](get-csonlineuser.md)

