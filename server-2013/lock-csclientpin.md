---
title: Lock-CsClientPin
TOCTitle: Lock-CsClientPin
ms:assetid: 81a9895f-96e3-43c9-9dac-8129358e446a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398650(v=OCS.15)
ms:contentKeyID: 48272687
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lock-CsClientPin

 

_**トピックの最終更新日:** 2015-03-09_

管理者が、ユーザーの暗証番号 (PIN) 認証の使用を禁止できるようにします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Lock-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、**Lock-CsClientPin** コマンドレットを使用して kenmyer@litwareinc.com というユーザーに属する PIN をロックします。

    Lock-CsClientPin -Identity "kenmyer@litwareinc.com"

## 例 2

例 2 では、**Lock-CsClientPin** コマンドレットを使用して、現在 PIN が割り当てられているすべてのユーザーの PIN をロックします。この操作を実行するため、**Get-CsUser** コマンドレットを使用して、Lync Server が有効になっているすべてのユーザーのコレクションを戻します。このコレクションは **Get-CsClientPinInfo** コマンドレットにパイプ処理され、**Where-Object** コマンドレットと併用して、IsPinSet プロパティが True と等しいユーザーのコレクションを戻します。次に、フィルター処理されたコレクションは **Lock-CsClientPin** コマンドレットにパイプ処理され、その結果、コレクション内の各ユーザーの PIN がロックされます。

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsPinSet -eq $True} | Lock-CsClientPin

## 例 3

例 3 では、**Lock-CsClientPin** コマンドレットを使用して期限切れの PIN を持つすべてのユーザーの PIN をロックします。このタスクを実行するため、まず **Get-CsUser** コマンドレットを呼び出して Lync Server が有効になっているすべてのユーザーのコレクションを戻します。次にこのコレクションは **Get-CsClientPinInfo** コマンドレットにパイプ処理され、**Where-Object** コマンドレットと併用して、期限切れの PIN を持つユーザーのコレクションに限定します。**Where-Object** コマンドレットでは、期限切れの PIN を持つユーザーを特定するため、(PIN が期限切れとなる日付を示す) PinExpirationTime プロパティが現在の日付より前であるアカウントをチェックします (現在の日付は、**Get-Date** コマンドレットを使用して取得します)。有効期限日 (2010 年 9 月 1 日など) が、現在の日付 (2010 年 9 月 2 日など) より前である場合は、PIN が期限切れであるということです。その後、**Lock-CsClientPin** コマンドレットを使用して期限切れの PIN をそれぞれロックします。

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.PinExpirationTime -lt (Get-Date)} | Lock-CsClientPin

## 解説

Lync Server では、ユーザーは、電話を使用してシステムに接続したり、公衆交換電話網 (PSTN) 会議に参加したりできます。通常、システムにログオンしたり会議に参加したりするには、ユーザーはユーザー名やパスワードの入力を要求されます。しかし、英数字キーパッドがない電話機を使用している場合は、ユーザー名とパスワードの入力が問題となります。そのため、Lync Server では、数値のみの PIN をユーザーに提供できるようにしています。入力が求められた場合、ユーザーは、ユーザー名とパスワードの代わりに PIN を入力することで、システムにログオンしたり会議に参加したりできます。

Lync Server では、セキュリティ対策として、ユーザーの PIN をロックできます。PIN がロックされると、ユーザーはその PIN を使用してシステムにアクセスしたり会議に参加したりできなくなります (ただし、このような場合でも、Lync 2013 のようなアプリケーションの使用や、ユーザー名とパスワードの入力によって、システムにアクセスしたり会議に参加したりすることはできます)。PIN がロックされてしまった後に、この PIN (およびユーザーのアクセス権限) を復元する唯一の方法は、管理者が PIN のロックを解除することです。**Unlock-CsClientPin** コマンドレットを使用して、PIN のロックを解除できます。

管理者は **Lock-CsClientPin** コマンドレットを使用して、ユーザーの PIN 認証を使用したシステムへのアクセスを一時的に無効にできます。PIN がシステムによってロックされる場合もあります。ユーザーがシステムへのログオンに何回も失敗すると、その PIN が自動的にロックされ、この場合も、管理者がロック解除する必要があります。

Lync Server Standard Edition のインストール時は、既定では、SQL Server Express のファイアウォール例外が有効ではないことに注意してください。つまり、Windows PowerShell のリモート インスタンスから **Lock-CsClientPin** コマンドレットを実行することはできません。これは、コマンドがファイアウォールを通過して SQL Server Express データベースにアクセスできないからです (ただし、Standard Edition サーバー自体では、コマンドレットをローカルで実行できます)。**Lock-CsClientPin** コマンドレットをリモートで実行するには、SQL Server Express のファイアウォール例外を手動で有効にする必要があります。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Lock-CsClientPin** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Lock-CsClientPin"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>PIN をロックする必要があるユーザー アカウントの Identity です。ユーザーの Identity は、以下の 4 つの形式のうちの 1 つを使用して指定できます。1) ユーザーの SIP アドレス、2) ユーザーのユーザー プリンシパル名 (UPN)、3) ドメイン\ログオン形式 (たとえば、litwareinc\kenmyer) のユーザーのドメイン名とログオン名、および 4) ユーザーの Active Directory 表示名 (たとえば、Ken Myer)。ユーザーの Identity は、ユーザーの Active Directory 識別名を参照して指定することもできます。</p>
<p>また、表示名をユーザーの Identity として使用する場合は、アスタリスク (*) ワイルドカード文字を使用できます。たとえば、&quot;* Smith&quot; という Identity は、末尾が &quot; Smith&quot; という文字列値の表示名を持つすべてのユーザーを戻します。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

文字列値または Microsoft.Rtc.Management.ADConnect.Schema.ADUser オブジェクト。**Lock-CsClientPin** コマンドレットは、ユーザー アカウントの Identity を表す、パイプライン処理された文字列値の入力を受け入れます。このコマンドレットは、ユーザー オブジェクトのパイプライン処理された入力も受け入れます。

## 戻り値の種類

**Lock-CsClientPin** コマンドレットは、値またはオブジェクトを戻しません。代わりに、Microsoft.Rtc.Management.UserPinService.PinInfoDetails オブジェクトの 1 つまたは複数のインスタンスを構成します。

## 関連項目

#### その他のリソース

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Set-CsClientPin](set-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)

