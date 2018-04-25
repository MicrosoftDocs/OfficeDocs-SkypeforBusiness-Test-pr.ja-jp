---
title: New-CsPrivacyConfiguration
TOCTitle: New-CsPrivacyConfiguration
ms:assetid: 9b7f02d7-93a5-4fa5-a74c-3fe4baf8bbfc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398807(v=OCS.15)
ms:contentKeyID: 48273009
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPrivacyConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

プライバシーの構成設定の新しいコレクションを作成します。プライバシーの構成設定は、ユーザーが他のユーザーに利用可能にする情報を決定するときに役立ちます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsPrivacyConfiguration -Identity <XdsIdentity> [-AutoInitiateContacts <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayPublishedPhotoDefault <$true | $false>] [-EnablePrivacyMode <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PublishLocationDataDefault <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドでは、Redmond サイト (-Identity site:Redmond) に適用されるプライバシーの構成設定の新しいコレクションを作成しています。新しい設定ではプライバシー モードを有効にします。これを行うため EnablePrivacyMode パラメーターを追加し、パラメーター値を True に設定しています。Redmond サイトに既にプライバシー設定のコレクションがある場合、このコマンドは失敗することに注意してください。

    New-CsPrivacyConfiguration -Identity site:Redmond -EnablePrivacyMode $True

## 例 2

例 2 では、InMemory パラメーターを使用して、最初にメモリ内のみに存在するプライバシーの構成設定の新しいコレクションを作成する方法を示しています。これを行うため、**New-CsPrivacyConfiguration** コマンドレットに、Identity パラメーターと InMemory パラメーターを指定して呼び出します。この結果のオブジェクトは、$x という名前の変数に格納されます。この時点では、プライバシー設定はメモリ内にのみ存在します。**Get-CsPrivacyConfiguration** コマンドレットを実行した場合、site:Redmond は一覧には表示されません。

2 番目のコマンドでは、EnablePrivacyMode プロパティの値を True に設定します。最後に、3 番目のコマンドでは **Set-CsPrivacyConfiguration** コマンドレットを使用し、この仮想のプライバシー設定コレクションを、Redmond サイトに適用される実際の設定コレクションに変換しています。**Set-CsPrivacyConfiguration** コマンドレットの呼び出しは非常に重要です。このコマンドレットが呼び出されなかった場合、Redmond サイトに新しいプライバシー設定が適用されません。この設定は、Windows PowerShell セッションを終了したとき、または変数 $x を削除したときに消滅します。

    $x = New-CsPrivacyConfiguration -Identity site:Redmond -InMemory
    $x.EnablePrivacyMode = $True
    Set-CsPrivacyConfiguration -Instance $x

## 解説

Lync Server では、他のユーザーと多くのプレゼンス情報を共有できます。自分の写真を公開したり、詳細な場所情報を提供したり、プレゼンス情報を (自分の連絡先リスト上のユーザーだけに表示するのではなく) 組織の全員に自動的に表示したりすることができます。

この情報を同僚が使用できることを歓迎するユーザーがいますが、このようなデータを共有することを嫌がるユーザーもいます (たとえば、自分のプレゼンス データに写真を載せることをためらう人は多いかもしれません)。原則として、ユーザーはどの情報を共有する (またはしない) かを制御できます。たとえば、自分の場所情報を他のユーザーと共有するかどうかを制御するため、チェック ボックスをオンまたはオフにすることができます。また、管理者はプライバシー構成コマンドレットを使用して、ユーザーのプライバシー設定を管理できます。場合によっては、管理者が設定を有効または無効にできます。たとえば、プロパティ AutoInitiateContacts を True に設定した場合、各ユーザーの連絡先リストにチーム メンバーが自動で追加されます。False に設定した場合、各ユーザーの連絡先リストにチーム メンバーが自動では追加されません。

別の場合では、値を変更する権限をユーザーに付与したまま、Lync の既定値を構成することができます。たとえば、ユーザーは場所の公開を中止する権限を持っていますが、既定では、場所データはユーザーに公開されます。PublishLocationDataByDefault プロパティを False に設定することで、管理者はこの動作を変更できます。その場合、ユーザーは選択すればこのデータを公開する権限を持っているにもかかわらず、既定では、場所データは公開されません。

プライバシーの構成設定は、グローバル スコープ、サイト スコープ、およびサービス スコープ (ただしユーザー サーバー サービスに対してのみ) で適用できます。**New-CsPrivacyConfiguration** コマンドレットでは、サイトまたはサービスに適用する新しいプライバシーの構成設定を作成できます (新しいコレクションはグローバル スコープでは作成できません)。個々のサイトまたはサービスが保持できるプライバシーの構成設定のコレクションは最大でも 1 つです。Redmond サイトに新しいコレクションを作成しようとしていて、サイトに既にプライバシー設定のコレクションがある場合、コマンドは失敗します。

このコマンドレットを実行できるユーザー: 既定では、**New-CsPrivacyConfiguration** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPrivacyConfiguration"}

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
<td><p>作成するプライバシーの構成設定を表す一意の識別子です。サイト スコープで設定の新しいコレクションを作成するには、次のような構文を使用します。-Identity site:Redmond。サービス スコープで新しい設定を作成するには、次のような構文を使用します。-Identity service:UserServer:atl-cs-001.litwareinc.com。プライバシー設定は、ユーザー サーバー サービスにのみ作成できます。これらの設定を他のサービスに適用しようとすると、エラーが発生します。</p>
<p>プライバシーの構成設定が、指定したサイトまたはサービスに既に存在する場合、コマンドは失敗することに注意してください。同様に、グローバル設定の新しいコレクションを作成しようとすると、コマンドは失敗します。</p></td>
</tr>
<tr class="even">
<td><p><em>AutoInitiateContacts</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True の場合、Lync は、上司と直属の部下を連絡先リストに自動的に追加します。既定値は True です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayPublishedPhotoDefault</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True の場合、ユーザーの写真が Lync によって自動的に公開されます。False の場合、ユーザーの写真は [自分の写真を他のユーザーに表示する] オプションを明示的にオンにしない限り表示されません。既定値は True です。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePrivacyMode</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True の場合、ユーザーは高度なプライバシー モードを有効にできます。高度なプライバシー モードでは、連絡先リストにあるユーザーに対してのみ、プレゼンス情報の参照が許可されます。False の場合、自分のプレゼンス情報は組織内の誰でも表示できます。既定値は False です。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>永続的な変更としてオブジェクトをコミットせずに、オブジェクト参照を作成します。このパラメーターを指定して呼び出したコマンドレットの出力を変数に割り当てる場合、オブジェクト参照のプロパティを変更し、コマンドレットに対応する Set- コマンドレットを呼び出してそれらの変更をコミットできます。</p></td>
</tr>
<tr class="even">
<td><p><em>PublishLocationDataDefault</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True の場合、場所データが Lync によって自動的に公開されます。False の場合、場所データは [所在地情報を連絡先に表示する] オプションを明示的にオンにしない限り表示されません。既定値は True です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Guid</p></td>
<td><p>新しいプライバシー構成設定を作成する Skype for Business Online テナント アカウントのグローバル一意識別子 (GUID)。次に例を示します。</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を返すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

なし。**New-CsPrivacyConfiguration** コマンドレットは、パイプ処理による入力を受け入れません。

## 戻り値の種類

**New-CsPrivacyConfiguration** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration オブジェクトの新しいインスタンスを作成します。

## 関連項目

#### その他のリソース

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

