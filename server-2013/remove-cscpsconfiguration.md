---
title: Remove-CsCpsConfiguration
TOCTitle: Remove-CsCpsConfiguration
ms:assetid: 546343e1-a2e4-4bc0-bf6d-c8ae9bb3e690
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398358(v=OCS.15)
ms:contentKeyID: 48272115
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCpsConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

既存のコール パーク サービス構成を削除します。通話のパークは、ユーザーが着信通話を "パーク" できるようにするためのサービスです。通話をパークすると、指定された範囲 (オービット) の番号に通話を転送し、次にその通話を直ちに保留にします。正しい番号を入力するだけで、だれでも (最初に電話に出た人以外も)、どの電話からでも通話を再開できます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsCpsConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、**Remove-CsCpsConfiguration** コマンドレットを使用して、ID が site:Redmond1 のコール パーク サービス構成を削除します。ID は一意であるため、このコマンドを実行して削除される構成は 1 つだけです。

    Remove-CsCpsConfiguration -Identity site:Redmond1

## 例 2

例 2 では、サイト スコープで定義されているすべてのコール パーク サービス構成を削除します。このタスクを実行するため、コマンドではまず、**Get-CsCpsConfiguration** コマンドレットと Filter パラメーターを使用して、サイト スコープで定義されているコール パーク サービス構成をすべて戻します。ワイルドカード site:\* を使用しているので、必ず ID が site: という文字列値で始まる設定のみが返されます。次に、フィルターされたコレクションを **Remove-CsCpsConfiguration** コマンドレットにパイプ処理し、コレクション内の各項目を削除しています。サイトからコール パーク サービスの設定を削除すると、サイトではいつでも、グローバル スコープで構成されたコール パーク サービスの設定を自動的に使用し始めることに注意してください。

    Get-CsCpsConfiguration -Filter site:* | Remove-CsCpsConfiguration

## 解説

このコマンドレットは、コール パーク サービス構成を削除する場合に使用します。コール パーク サービス構成により、パークされた後の通話の処理方法を指定します。たとえば、パークされた通話がしばらくの間応答されない場合は、管理者、応答グループなど、別の人に自動的に転送されます。通話は、応答忘れを防ぐために、一定の時間が経過した後にかけ直すように構成することができます。またコール パーク サービスは、通話がパークされている間、発信者に対して保留音が再生されるように構成することもできます。

このコマンドレットを使用して、グローバル構成を含むすべてのコール パークの構成を削除できます。ただし、グローバル構成の場合、構成は実際に削除されるのではなく、既定値にリセットされるだけです。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Remove-CsCpsConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCpsConfiguration"}

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
<td><p>削除するコール パーク サービス構成の一意の識別子です。この識別子は Global または site:&lt;サイト名&gt; のいずれかになります。ここで、&lt;サイト名&gt; は、構成が適用されるサイトの名前です。</p></td>
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
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings オブジェクト。パイプライン処理されたコール パーク サービス構成オブジェクトの入力を受け入れます。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 型のオブジェクトを削除します。

## 関連項目

#### その他のリソース

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

