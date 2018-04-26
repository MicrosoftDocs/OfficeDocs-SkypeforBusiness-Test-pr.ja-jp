---
title: Get-CsTenantFederationConfiguration
TOCTitle: Get-CsTenantFederationConfiguration
ms:assetid: e5f836d0-6066-4c23-9594-6e3f1cbd39ef
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994072(v=OCS.15)
ms:contentKeyID: 52056723
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantFederationConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

Microsoft Lync Online テナントのフェデレーション構成設定に関する情報を返します。フェデレーション構成設定は、ユーザーが通信できるドメイン (存在する場合) を決定するために使用されます。

**Get-CsTenantFederationConfiguration** コマンドレットは、Skype for Business Online でのみ使用できます。

## 構文

    Get-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-LocalStore] [-Verbose] Get-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-Filter <String>] [-LocalStore] [-Verbose]

## 例

## 例 1

例 1 に示すコマンドは、テナント ID "bf19b7db-6960-41e5-a139-2aa373474354" のテナントのフェデレーション構成設定情報を返します。テナント ID は、次のようなコマンドを使用して取得できます。

Get-CsTenant | Select-Object TenantID

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Tenant パラメーターは省略可能です。次の構文を使用して Get-CsTenantFederationConfiguration を呼び出すこともできます。

    Get-CsTenantFederationConfiguration

## 例 2

例 2 では、テナント bf19b7db-6960-41e5-a139-2aa373474354 のフェデレーション許可リストで見つかったすべてのドメインに関する情報が返されます (許可リストは、テナントがフェデレーションを行うことができるすべてのドメインを表します)。これを行うために、コマンドはまず、**Get-CsTenantFederationConfiguration** コマンドレットを呼び出して、指定したテナントに関するフェデレーション情報を返します。次に、この情報を **Select-Object** コマンドレットにパイプ処理し、ExpandProperty を使用してプロパティ AllowedList を "展開" します。プロパティを展開すると、そのプロパティに格納されているすべての情報が読みやすい形式で画面に表示されます。

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty AllowedList

## 例 3

上記のコマンドは、組織で現在使用されているすべてのテナントのフェデレーション構成を返します。このタスクを実行するために、コマンドはまず、パラメーターを指定せずに **Get-CsTenant** コマンドレットを呼び出します。これにより、使用可能なすべてのテナントが返されます。次に、このコレクションを **ForEach-Object** コマンドレットにパイプ処理します。ForEach-Object は、コレクション内の各テナントを取得して **Get-CsTenantFederationConfiguration** コマンドレットを呼び出し、プロパティ値 TenantID (**Get-CsTenant** コマンドレットによって返されます) を使用してテナント ID を表します。

    Get-CsTenant | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId}

## 例 4

例 4 では、パブリック ユーザーとのフェデレーションが許可されてないテナントに関するフェデレーション構成情報のみが返されます。これを行うために、コマンドはまず、パラメーターを指定せずに **Get-CsTenant** コマンドレットを呼び出して、組織で使用するように構成されているすべてのテナントのコレクションを返します。このコレクションを **ForEach-Object** コマンドレットにパイプ処理し、コレクション内の各テナントを取得してから、**Get-CsTenantFederationConfiguration** コマンドレットを使用してフェデレーション構成情報を返します。次に、一連のフェデレーション構成情報全体を **Where-Object** コマンドレットにパイプ処理し、AllowPublicUsers プロパティが $False に等しい (-eq) テナントのみを選択します。

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId} | Where-Object {$_.AllowPublicUsers -eq $False}

## 解説

フェデレーションは、ユーザーが他のドメインのユーザーと IM およびプレゼンス情報を交換できるようにするサービスです。Lync Online では、管理者はフェデレーション構成設定を使用して以下を管理することができます。

  - ユーザーが他のドメインのユーザーと通信できるかどうか、また通信できる場合は通信先として可能なドメイン。

  - ユーザーが Windows Live、AOL、Yahoo などのパブリック IM プロバイダーおよびプレゼンス プロバイダーのアカウントを持つユーザーと通信できるかどうか。

**Get-CsTenantFederationConfiguration** コマンドレットを使用すると、管理者は Lync Online テナントのフェデレーション情報を返すことができます。このコマンドレットを使用して、許可リストおよび禁止リスト (ユーザーが通信できるドメイン、または通信できないドメインを指定するリスト) を確認することもできます。ただし、ユーザーが通信できるパブリック IM プロバイダーやプレゼンス プロバイダーを確認するには、管理者は **Get-CsTenantPublicProvider** コマンドレットを使用する必要があります。

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
<td><p>テナントのフェデレーション構成設定のコレクションを返すために、ワイルドカード文字を使用することができます。各テナントでは、フェデレーション構成設定のグローバル コレクションは 1 つに制限されるため、Filter パラメーターを使用する必要はありません。ただし、次の構文は <strong>Get-CsTenantFederationConfiguration</strong> コマンドレットに有効です。</p>
<p>Get-CsTenantFederationConfiguration –Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>返されるテナントのフェデレーション構成設定のコレクションを指定します。各テナントでは、フェデレーション構成設定のコレクションは 1 つに制限されるため、 <strong>Get-CsTenantFederationConfiguration</strong> コマンドレットを呼び出すときにこのパラメーターを指定する必要はありません。Identity パラメーターを使用しない場合、Tenant パラメーターも指定する必要があります。次に例を示します。</p>
<p>Get-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア自体からではなく、中央管理ストアのローカル レプリカからテナントのフェデレーション構成データを取得します。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Guid</p></td>
<td><p>フェデレーション設定が返されているテナント アカウントのグローバル一意識別子 (GUID) です。次に例を示します。</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を返すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Windows PowerShell のリモート セッションを使用していて、 Skype for Business Online のみに接続している場合、Tenant パラメーターを含める必要はありません。代わりに、接続情報に基づいてテナント ID が自動的に入力されます。Tenant パラメーターはハイブリッド展開で主に使用されます。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsTenantFederationConfiguration** コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

**Get-CsTenantFederationConfiguration** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings オブジェクトのインスタンスを返します。

## 関連項目

#### その他のリソース

[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

