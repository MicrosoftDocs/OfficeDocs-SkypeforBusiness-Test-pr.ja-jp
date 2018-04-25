---
title: Update-CsTenantMeetingUrl
TOCTitle: Update-CsTenantMeetingUrl
ms:assetid: 9aed3ede-bbd3-405a-997f-f7553e66aecd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn424754(v=OCS.15)
ms:contentKeyID: 59602762
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsTenantMeetingUrl

 

_**トピックの最終更新日:** 2015-03-09_

指定した Skype for Business Online テナントの会議 URL を更新します。更新された URL の形式はより簡単で標準的であるため、クライアントは簡単に会議を見つけて接続できます。

このコマンドレットは Skype for Business Online 専用です。

## 構文

    Update-CsTenantMeetingUrl [-Tenant] <guid> [-Force] [-WhatIf] [-Confirm]

## 例

## 例 1

例 1 のコマンドでは、テナント ID 38aad667-af54-4397-aaa7-e94c79ec2308 のテナントの会議 URL を更新します (このコマンドの完了にはテナント ID の入力が必要です)。Enter キーを押してコマンドを実行すると、会議 URL を更新してよいかどうかの確認を求められます。Update-CsTenantMeetingUrl で実際に Skype for Business Online の構成設定を変更するには、このプロンプトで「はい」を選ぶ必要があります。

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308"

## 例 2

例 2 でも、テナント ID 38aad667-af54-4397-aaa7-e94c79ec2308 のテナントの会議 URL を更新します。ただしこの場合、Force パラメーターが含まれているため、Update-CsTenantMeetingUrl の実行時に通常は表示される確認プロンプトが省略されます。この場合、Enter キーを押すとすぐにコマンドが実行され、Skype for Business Online の構成設定が変更されます。

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308" -Force

## 解説

Update-CsTenantMeetingUrl によって、Skype for Business Online の会議 URL がより簡単で標準的な形式になり、元の会議 URL で発生することのあった問題が解消されます。たとえば、組織で contoso.onmicrosoft.com という名前の Office 365 ドメインを設定すると、会議 URL は次のようになります。

https://meet.lync.com/onmicrosoft/contoso/user1/45GZFH99

ここで、組織が変更を行って onmicrosoft.com という URL の代わりに “バニティ” URL である adatum.com を使うことにしたとします。組織のユーザーのメール アドレスは、adatum.com ドメインを使用するように変更されます。ただし、会議 URL では引き続き前のドメイン名が使用されます。

https://meet.lync.com/contoso/user1/45GZFH99

この問題を解決するには、管理者が Update-CsTenantMeetingUrl コマンドレットを実行する必要があります。こうすると前の会議 URL がバニティ URL である新しい会議 URL に置き換えられます。

https://meet.lync.com/adatum.com/user1/37JYLP71

この変更を行う唯一の方法は、Update-CsTenantMeetingUrl コマンドレットを実行することです。

Update-CsTenantMeetingUrl を実行すると、Skype for Business Online テナントは短い同期遅延の後、新しい URL に切り替えられます。このために今後スケジュールされる新しい会議に問題が起こることはありません。新しい会議は、新しい URL で自動的にスケジュールされるためです。ただし、前にスケジュールした会議には問題が起こります。前の、使われなくなった会議 URL でスケジュールされているためです。この問題を解決する唯一の方法は、会議を再スケジュールしてもらうことです。

これは、一部の組織 (特に多くの会議をスケジュール済みの組織) で問題を引き起こす可能性があるため、既定では Update-CsTenantMeetingUrl で実際に会議 URL が更新される前に次のプロンプトが表示されます。

警告: これは、このテナント内のユーザーに対する重大な変更です。会議 URL 構成が更新されます\! 古い会議 URL は機能しなくなります。この変更は元に戻せません。  
このまま続けますか?  
\[Y\] はい \[A\] すべてはい \[N\] いいえ \[L\] すべていいえ \[S\] 中断 \[?\] ヘルプ (既定は “Y”):

コマンドが実際に実行されるには、“はい” または “すべてはい” を選ぶ必要があります。“いいえ” を選ぶとコマンドはキャンセルされ、会議 URL は更新されません。いったん会議 URL を変更すると、元の URL には戻せないので注意してください。いったんコマンドを実行すると URL が変更され、前にスケジュールした会議は再スケジュールする必要があります。つまりこのコマンドは、テナントごとに 1 回実行すれば済むということでもあります。コマンドを定期的に実行して、会議 URL を再更新する必要はありません。

確認プロンプトなしでコマンドを実行したい場合は、Force パラメーターを含めます。こうすれば、Update-CsTenantMeetingUrl が次の確認プロンプトなしで実行されます。

警告: これは、このテナント内のユーザーに対する重大な変更です。会議 URL 構成が更新されます\!

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
<td><p><strong>Tenant</strong></p></td>
<td><p>必須</p></td>
<td><p>System.Guid</p></td>
<td><p>フェデレーション設定が返されているテナント アカウントのグローバル一意識別子 (GUID) です。次に例を示します。</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を返すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Tenant パラメーターを含めないと、Update-CsMeetingUrl でパラメーターの入力を求められます。続けるにはこのパラメーターの入力が必要です。</p></td>
</tr>
<tr class="even">
<td><p><strong>Confirm</strong></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p>
<p>Update-CsMeetingUrl の既定の動作では、更新の実行前に確認プロンプトが表示されます。つまり確認プロンプトを表示したい場合、Confirm パラメーターを含める必要はありません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Force</strong></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>確認プロンプトが表示されないようにします。このパラメーターを入力しないと、Update-CsMeetingUrl で更新前に確認プロンプトが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>WhatIf</strong></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。Update-CsMeetingUrl では、パイプライン処理された入力は受け付けられません。

## 戻り値の種類

なし。

## 関連項目

#### その他のリソース

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)

