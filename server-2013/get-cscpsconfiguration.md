---
title: Get-CsCpsConfiguration
TOCTitle: Get-CsCpsConfiguration
ms:assetid: d81ee8fe-d02b-4f60-a4d5-6aa84f65d156
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398948(v=OCS.15)
ms:contentKeyID: 48273715
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCpsConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

コール パーク サービスに関する情報を戻します。通話の保留は、ユーザーが着信通話を保留 (パーク) できるサービスです。コール パークを行うと、指定された範囲 (オービット) 内の番号に通話が転送され、その通話は直ちに保留状態になります。だれでも (最初の電話に出た人以外も) 正しい番号を入力することで、システム内の任意の電話から通話を再開できます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCpsConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 では、組織で使用するように定義されたすべてのコール パーク サービス構成のコレクションを取得します。

    Get-CsCpsConfiguration

## 例 2

例 2 では、site:Redmond1 という ID を持つコール パーク サービス構成のみを取得します。

    Get-CsCpsConfiguration -Identity site:Redmond1

## 例 3

例 3 では、Filter パラメーターを使用して、サイト スコープで構成されたすべてのコール パーク サービス構成を戻します。ワイルドカード文字列 site:\* は、ID が site: の文字列値で始まる設定のみを戻すように、**Get-CsCpsConfiguration** コマンドレットに指示します。

    Get-CsCpsConfiguration -Filter site:*

## 例 4

例 3 では、Filter パラメーターを使用して、定義済みのすべてのコール パーク サービス構成のサブセットを取得します。この場合、文字列 \*:re\* でフィルター処理を行います。これにより、Redmond1、Redmond2、および RemoteComputer など、re という文字で始まる名前を持つすべてのサイトのコール パーク構成が戻されます。

    Get-CsCpsConfiguration -Filter *:re*

## 例 5

例 5 では、発信者が保留中のときに保留音を再生しないすべてのコール パーク サービス設定を返します。そのために、このコマンドでは、最初に **Get-CsCpsConfiguration** コマンドレットを使用して、組織で使用するように構成されたすべてのコール パーク サービス設定を取得します。次に、このコレクションは **Where-Object** コマンドレットにパイプ処理されます。これにより、返されるデータを EnableMusicOnHold プロパティが False に等しい (-eq) 項目のみに制限するフィルターが適用されます。

    Get-CsCpsConfiguration | Where-Object {$_.EnableMusicOnHold -eq $False}

## 解説

1 つ以上のコール パーク サービス構成を取得する場合に、このコマンドレットを使用します。コール パーク サービス構成は、パークされた通話の処理方法を指定します。たとえば、パークされた通話がしばらくの間応答されない場合は、管理者または応答グループなど、別の人に自動的に転送されます。通話は、応答忘れを防ぐために、一定の時間が経過した後にかけ直すように構成することもできます。また、通話がパークされている間、発信者に対して保留音が再生されるようにコール パーク サービスを構成することもできます。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが **Get-CsCpsConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCpsConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>ワイルドカード文字列に一致する ID 値を持つ構成のみを取得できるように、ワイルドカード検索を実行できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>取得するコール パーク サービス構成の一意の識別子です。この識別子は Global または site:&lt;サイト名&gt; のいずれかになります。ここで、&lt;サイト名&gt; は、構成が適用されるサイトの名前です。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体からではなく、中央管理ストア のローカル レプリカからコール パーク サービス情報を取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings 型の 1 つ以上のオブジェクトを取得します。

## 関連項目

#### その他のリソース

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

