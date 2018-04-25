---
title: Get-CsConferencingConfiguration
TOCTitle: Get-CsConferencingConfiguration
ms:assetid: db4ab3bc-071c-4f73-a3a0-62dc8aed48a1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398965(v=OCS.15)
ms:contentKeyID: 48273819
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferencingConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

組織用の会議の構成設定に関する情報を戻します。会議設定は、会議コンテンツや配布資料の最大許容サイズ、コンテンツの猶予期間 (コンテンツが削除されるまでに保存される期間)、サポートされているクライアントの内部および外部ダウンロード用 URL などを決定します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferencingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 では、組織内で現在使用しているすべての会議構成設定に関する情報を戻します。これを実行するために、パラメーターを何も指定しない **Get-CsConferencingConfiguration** コマンドレットを呼び出します。

    Get-CsConferencingConfiguration

## 例 2

例 2 では、Redmond サイト (-Identity site:Redmond) に関する会議構成情報を戻します。Identity は一意である必要があるため、このコマンドが戻す項目は最大でも、会議構成設定の 1 つのコレクションです。

    Get-CsConferencingConfiguration -Identity site:Redmond

## 例 3

例 3 のコマンドでは、サイト スコープで既に適用されたすべての会議構成設定に関する情報が戻されます。これを実行するには、Filter パラメーターとともに **Get-CsConferencingConfiguration** コマンドレットを呼び出します。フィルター値 "site:\*" によって、Identity が "site:" という文字列値で始まる設定のみが返されます。

    Get-CsConferencingConfiguration -Filter "site:*"

## 例 4

例 4 では、組織が Litwareinc に設定されていないすべての会議構成設定に関する情報が返されます。このタスクを実行するために、このコマンドは、最初にパラメーターを指定せずに **Get-CsConferencingConfiguration** コマンドレットを呼び出します。これにより、組織で使用されているすべての会議構成設定のコレクションが返されます。次に、結果として得られたコレクションは、**Where-Object** コマンドレットにパイプ処理され、Organization プロパティが Litwareinc に等しくない設定のみが選択されます。

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"}

## 例 5

例 5 では、最大コンテンツ記憶域が 100 MB より大きい会議構成設定のみに関する情報が返されます。そのために、このコマンドは最初に、パラメーターを指定せずに **Get-CsConferencingConfiguration** コマンドレットを呼び出して、すべての会議構成設定のコレクションを返しています。次に、このコレクションは **Where-Object** コマンドレットにパイプ処理され、コンテンツ記憶域が 100 MB を超えている設定のみが抽出されます。

    Get-CsConferencingConfiguration | Where-Object {$_.MaxContentStorageMB -gt 100}

## 解説

会議に関しては、管理と運用管理を行うコマンドレットは、2 つのセットに分かれています。ユーザーが実行できることと実行できないこと (たとえば、ユーザーが匿名の参加者を会議に参加するように招待できるか、ユーザーは会議内でアプリケーションの共有やファイルの転送を許可されているか) を管理する場合は、**CsConferencingPolicy** コマンドレットを使用する必要があります。

ユーザー アクティビティに加えて、管理者は Lync ServerWeb 会議サービス も管理する必要があります。たとえば、1 つの会議に割り当てるコンテンツ記憶域の最大容量の指定、会議資料を自動的に削除する前の猶予期間の指定などは、管理者が設定できる必要があります。また管理者は、アプリケーション共有、ファイル転送などのアクティビティで使用するポートも指定できる必要があります。

**CsConferencingConfiguration** コマンドレットを使用すると、このうち後者のアクティビティを管理できます。このコマンドレット群を使用すると、実際のサーバーそのものを管理できます。**CsConferencingConfiguration** コマンドレット群はグローバル スコープにもサイト スコープにもサービス スコープにも適用できますが、あるユーザーが会議中にアプリケーションを共有できるかどうかを指定するのには使用できません。ただし、アプリケーション共有が許可されている場合は、このコマンド群でそのアクティビティに使用するポートを指定できます。同様に、このコマンドレット群では記憶域の上限、有効期限、およびユーザーが会議のヘルプやリソースを取得できる内部 URL と外部 URL も指定できます。

**Get-CsConferencingConfiguration** コマンドレットは、組織で現在使用されているすべての Web 会議の構成設定に関する情報を戻す方法を管理者に提供します。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが **Get-CsConferencingConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferencingConfiguration"}

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
<td><p>戻される会議構成設定の ID を指定する際に、ワイルドカードを使用できます。たとえば、次の構文は、サイト スコープで構成されているすべての設定を戻します。-Filter &quot;site:*&quot;。次の構文を使用すると、サービス スコープで構成されたすべての設定が戻されます。-Filter &quot;service:*&quot;。</p>
<p>Identity パラメーターと Filter パラメーターは、同じコマンドで同時に使用できないことに注意してください。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>取得する会議構成設定のコレクションに対応する一意識別子です。グローバル設定を取得するには、次の構文を使用します。-Identity global。サイト スコープで構成された設定を取得するには、次のような構文を使用します。-Identity &quot;site:Redmond&quot;。サービス スコープで構成されている設定を取得するには、次のような構文を使用します。-Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;。</p>
<p>このパラメーターを指定しない場合は、<strong>Get-CsConferencingConfiguration</strong> コマンドレットによって、組織内で現在使用されているすべての会議構成設定が戻されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体からではなく、中央管理ストア のローカル レプリカから会議構成データを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsConferencingConfiguration** コマンドレットはパイプライン入力を受け付けません。

## 戻り値の種類

**Get-CsConferencingConfiguration** コマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Remove-CsConferencingConfiguration](remove-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

