---
title: Remove-CsPrivacyConfiguration
TOCTitle: Remove-CsPrivacyConfiguration
ms:assetid: 32052c51-953d-4278-9425-306245d297ed
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425821(v=OCS.15)
ms:contentKeyID: 48271679
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPrivacyConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

プライバシー構成設定の既存のコレクションを削除します。プライバシー構成設定を使用すると、ユーザーは他のユーザーにどの程度の情報を表示するかを指定できます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsPrivacyConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 は、Redmond サイトに割り当てられたプライバシー構成設定を戻します。これらの設定が削除されると、Redmond サイト内のユーザーはグローバル プライバシー構成設定を自動的に継承します。

    Remove-CsPrivacyConfiguration -Identity site:Redmond

## 例 2

例 2 では、サイト スコープで割り当てられたすべてのプライバシー構成設定が削除されます。これを行うには、まず、このコマンドは Filter パラメーターを指定して **Get-CsPrivacyConfiguration** コマンドレットを呼び出します。フィルター値 "site:\*" により、ID が "site" という文字で始まる設定のみが戻されます。次に、このフィルター処理されたコレクションは **Remove-CsPrivacyConfiguration** コマンドレットにパイプ処理され、コレクション内の各項目が削除されます。

    Get-CsPrivacyConfiguration -Filter "site:*" | Remove-CsPrivacyConfiguration

## 例 3

例 3 に示すコマンドは、プライバシー モードが無効になっているすべてのプライバシー構成設定を削除します。このタスクを実行するには、まず、このコマンドはパラメーターを指定せずに **Get-CsPrivacyConfiguration** コマンドレットを呼び出します。これにより、組織で使用中のすべてのプライバシー構成設定のコレクションが戻されます。次に、このコレクションは **Where-Object** コマンドレットにパイプ処理され、EnablePrivacyMode プロパティが False と等しい設定のみを選択します。このフィルター処理されたコレクションを **Remove-CsPrivacyConfiguration** コマンドレットにパイプ処理し、コレクション内の各項目を削除します。

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $False} | Remove-CsPrivacyConfiguration

## 解説

Lync Server では、豊富なプレゼンス情報を他のユーザーと共有できます。自分の写真を公開したり、詳細な場所情報を提供したり、プレゼンス情報を (自分の連絡先リスト上のユーザーだけに表示するのではなく) 組織の全員に自動的に表示したりできます。

一部のユーザーは喜んでこの情報を同僚に提供したいと思いますが、このデータを共有することに慎重なユーザーもいます (たとえば、多くのユーザーは、プレゼンス データに写真を含めることを躊躇するかもしれません)。原則として、ユーザーはどの情報を共有する (またはしない) かを制御できます。たとえば、自分の場所情報を他のユーザーと共有するかどうかを制御するため、チェック ボックスをオンまたはオフにすることができます。また、プライバシー構成コマンドレットによって、管理者はユーザーのプライバシー設定を管理できます。場合によっては、管理者が設定を有効または無効にすることができます。たとえば、プロパティ AutoInitiateContacts を True に設定すると、チーム メンバーが各ユーザーの連絡先リストに自動的に追加されます。False に設定すると、チームメンバーが各ユーザーの連絡先リストに自動的に追加されることはありません。

また、管理者は Lync Server 内の既定値を設定しつつ、ユーザーにそれらの値を変更する権限を付与できます。たとえば、場所データを既定でユーザーに公開して、場所の公開を中止する権限をユーザーに付与できます。PublishLocationDataByDefault プロパティを False に設定することで、管理者はこの動作を変更できます。その場合、場所データは既定で公開されませんが、ユーザーには自身が選択すればこのデータを公開できる権限があります。

プライバシー構成設定はグローバル スコープ、サイト スコープ、およびサービス スコープで適用できます (ただし、ユーザー サーバー サービスのみに対して)。**Remove-CsPrivacyConfiguration** コマンドレットにより、サイト スコープまたはサービス スコープのいずれかで構成された設定を削除することができます。たとえば、サイト スコープで構成された設定に対してこのコマンドレットを実行すると、それらの設定は削除され、そのサイトのユーザーのプライバシー設定はグローバル コレクションによって制御されます。**Remove-CsPrivacyConfiguration** コマンドレットは、グローバル コレクションに対しても実行できますが、グローバル コレクションは削除されません。代わりに、そのコレクションのすべてのプロパティが既定値にリセットされます。たとえば、以前に EnablePrivacyMode プロパティの値を True に変更したとします。ここでグローバル コレクションを "削除" すると、EnablePrivacyMode は既定値である False に戻されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Remove-CsPrivacyConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPrivacyConfiguration"}

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
<th>必須かどうか</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>削除するプライバシー構成設定の一意の識別子。サイト スコープで構成された設定を削除するには、次のような構文を使用します。-Identity site:Redmond。サービス レベルで設定を削除するには、次のような構文を使用します。-Identity service:UserServer:atl-cs-001.litwareinc.com。</p>
<p><strong>Remove-CsPrivacyConfiguration</strong> コマンドレットは、設定のグローバル コレクションに対しても実行できます。ただし、その場合、グローバル設定は削除されません。代わりに、そのコレクションのすべてのプロパティが既定値にリセットされます。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Guid</p></td>
<td><p>プライバシー構成設定を削除する Skype for Business Online テナント アカウントのグローバル一意識別子 (GUID)。次に例を示します。</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を戻すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration オブジェクト。**Remove-CsPrivacyConfiguration** コマンドレットは、プライバシー構成オブジェクトのパイプライン処理された入力を受け入れます。

## 戻り値の種類

なし。代わりに、**Remove-CsPrivacyConfiguration** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration オブジェクトの既存のインスタンスを削除します。

## 関連項目

#### その他のリソース

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

