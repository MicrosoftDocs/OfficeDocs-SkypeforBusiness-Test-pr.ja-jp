---
title: Set-CsTenantPublicProvider
TOCTitle: Set-CsTenantPublicProvider
ms:assetid: 8341d801-bfa1-4c5b-9b80-5d503deebaf7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994047(v=OCS.15)
ms:contentKeyID: 52056631
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantPublicProvider

 

_**トピックの最終更新日:** 2015-03-09_

サードパーティの IM やプレゼンス プロバイダー (Windows Live、AOL、Yahoo) との通信を有効または無効にします。有効にすると、Microsoft Lync Online ユーザーは、指定したパブリック プロバイダーのアカウントを持つユーザーと IM やプレゼンス情報を交換できるようになります。

**Set-CsTenantPublicProvider** コマンドレットは、Skype for Business Online でのみ使用できます。

## 構文

    Set-CsTenantPublicProvider -Tenant <String> [-Provider <String[]>] [-Verbose] [-WhatIf] [-Confirm]

## 例

## 例 1

例 1 に示すコマンドは、テナント ID bf19b7db-6960-41e5-a139-2aa373474354 のテナントに対して Windows Live とのフェデレーションを有効にします。Windows Live が指定された唯一のプロバイダーであるため、このコマンドの実行後、AOL と Yahoo の両プロバイダーは無効になります。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

## 例 2

例 2 では、Windows Live と AOL の 2 つのパブリック プロバイダーが有効になります。つまり、指定したテナントに対して無効になるパブリック プロバイダーは Yahoo だけです。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive","AOL"

## 例 3

例 3 は、指定したテナントに対してすべてのパブリック プロバイダーを無効にする方法を示しています。このために、Provider プロパティを空の文字列 ("") に設定します。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

## 例 4

例 4 に示すコマンドは、すべての Lync Online テナントに対してすべてのパブリック プロバイダーを無効にします。このタスクを実行するために、コマンドは最初に **Get-CsTenant** コマンドレットを使用して、すべてのテナントのコレクションを返します。次に、このコレクションを **ForEach-Object** コマンドレットにパイプ処理し、コレクション内の各テナントを取得して、各テナントに対して **Set-CsTenantPublicProvider** コマンドレットを呼び出し、すべてのパブリック プロバイダーを無効にします。最後のタスクは、Provider プロパティを空の文字列 ("") に設定すると実行されます。

    Get-CsTenant | ForEach-Object {Set-CsTenantPublicProvider -Tenant $_.TenantId -Provider ""}

## 解説

パブリック プロバイダーとは、一般公衆向けの SIP 通信サービスを提供する組織のことです。パブリック プロバイダーとフェデレーション関係を確立すると、そのプロバイダーがホストするアカウントを持つすべてのユーザーと、効率よくフェデレーションを確立できます。たとえば、Windows Live とフェデレーションを確立すると、組織のユーザーが、Windows Live のインスタント メッセージ アカウントを持つすべてのユーザーと、インスタント メッセージやプレゼンス情報を交換できるようになります

Lync Online では、管理者が次のパブリック IM プロバイダーおよびプレゼンス プロバイダーの 1 つ以上とのフェデレーションを構成することができます。

  -   
    Windows Live

  -   
    AOL

  -   
    Yahoo\!

**Set-CsTenantPublicProvider** コマンドレットを使用して、これらのパブリック プロバイダーのいずれかとのフェデレーションを有効または無効にすることができます。このコマンドレットを使用する際、**Set-CsTenantPublicProvider** コマンドレットを実行するたびに、有効にするすべてのプロバイダーを指定する必要があることに注意してください。たとえば、3 つのプロバイダーがすべて無効になっている場合に次のコマンドを実行する場合を考えます。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

これにより、Windows Live が有効になりますが、AOL と Yahoo は無効のままです。

さらに、次のコマンドを実行する場合を考えます。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL"

このコマンドにより、AOL が有効になります。ただし、Windows Live が無効になります。これは、Provider パラメーターに指定されたパラメーター値の一部として Windows Live が指定されなかったためです。AOL を有効にし、Windows Live も有効のままにする場合は、Set-CsTenantPublicProvider を呼び出すときに次のように AOL と Windows Live の両方を指定する必要があります。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

3 つのプロバイダーすべてに対してフェデレーションを無効にするには、次のように Provider プロパティを空の文字列 ("") に設定します。

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

パブリック プロバイダーの状態を有効にするだけでは、ユーザーはそのプロバイダーでアカウントを持つユーザーとインスタント メッセージやプレゼンス情報を交換できないことに注意してください。プロバイダー自体とのフェデレーションを有効にするだけでなく、管理者はフェデレーション構成設定の AllowPublicUsers プロパティを True に設定する必要もあります。このプロパティを False に設定した場合、パブリック プロバイダー構成設定に関係なく、パブリック プロバイダーと通信することはできません。

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
<td><p>System.Guid</p></td>
<td><p>パブリック プロバイダー設定が変更されるテナント アカウントのグローバル一意識別子 (GUID) です。次に例を示します。</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行して、各テナントのテナント ID を返すことができます。</p>
<pre><code>Get-CsTenant | Select-Object DisplayName, TenantID</code></pre>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String[]</p></td>
<td><p>ユーザーが通信できるパブリック プロバイダー (またはプロバイダー) を指定します。有効な値は次のとおりです。</p>
<p>* AOL</p>
<p>* WindowsLive</p>
<p>* Yahoo</p>
<p>パブリック プロバイダーを構成する際、Provider パラメーター値で指定されるプロバイダーが有効になりますが、このパラメーター値で指定されないプロバイダーは無効になることに注意してください。たとえば、次の構文によって、Yahoo のみが有効になり、Windows Live と AOL は無効になります。</p>
<p>-Provider &quot;AOL&quot;</p>
<p>複数のプロバイダーを有効にするには、次のようにコンマを使用してプロバイダー名を区切ります。</p>
<p>-Provider &quot;AOL&quot;,&quot;WindowsLive&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

**Set-CsTenantPublicProvider** コマンドレットは、Microsoft.Rtc.Management.Hosted.TenantPICStatus オブジェクトのパイプ処理されたインスタンスを受け入れます。

## 戻り値の種類

なし。代わりに、**Set-CsTenantPublicProvider** コマンドレットは、Microsoft.Rtc.Management.Hosted.TenantPICStatus オブジェクトの既存のインスタンスを変更します。

## 関連項目

#### その他のリソース

[Get-CsTenantPublicProvider](get-cstenantpublicprovider.md)

