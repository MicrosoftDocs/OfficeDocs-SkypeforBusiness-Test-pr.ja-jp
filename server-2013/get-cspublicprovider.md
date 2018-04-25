---
title: Get-CsPublicProvider
TOCTitle: Get-CsPublicProvider
ms:assetid: c122505d-7209-4dcb-a888-5c73f58fa68a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412945(v=OCS.15)
ms:contentKeyID: 48273481
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPublicProvider

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用するように構成されたパブリック プロバイダーに関する情報を戻します。パブリック プロバイダーとは、インスタント メッセージ、プレゼンス、および関連サービスを、一般公衆に対して提供する組織のことです。Lync Server には、Yahoo\!、AIM (AOL)、および Messenger (MSN) の 3 つの構成済みのパブリック プロバイダーが付属していますが、無効になっています。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPublicProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 に示すコマンドを実行すると、組織での使用向けに構成されているすべての公開プロバイダーのコレクションが戻されます。追加パラメーターを指定せずに **Get-CsPublicProvider** コマンドレットを呼び出すと、公開プロバイダーの完全なコレクションが常に戻されます。

    Get-CsPublicProvider

## 例 2

例 2 では、Messenger という ID を持つすべての公開プロバイダーが戻されます。ID は公開プロバイダー (およびホスティング プロバイダー) の間で一意である必要があるため、このコマンドは常に、最大 1 つの項目を戻します。

    Get-CsPublicProvider -Identity "Messenger"

## 例 3

例 3 では、W という文字で始まる ID を持つすべての公開プロバイダーが戻されます。Filter パラメーターとフィルター値 "W\*" を指定して、これを行います。

    Get-CsPublicProvider -Filter W*

## 例 4

例 4 に示すコマンドを実行すると、現在無効にされているすべての公開プロバイダーのコレクションが戻されます。これを行うため、このコマンドでは最初に **Get-CsPublicProvider** コマンドレットを呼び出して、組織での使用向けに構成されているすべての公開プロバイダーのコレクションを戻します。次にこのコレクションを **Where-Object** コマンドレットにパイプ処理し、Enabled プロパティが False のプロバイダーだけを選択します。

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False}

## 例 5

例 5 では、VerificationLevel プロパティに AlwaysUnverifiable または UseSourceVerification が設定されている、すべての公開プロバイダーが戻されます (公開レベルには、AlwaysUnverifiable、UseSourceVerification、または AlwaysVerifiable のいずれかが設定できます)。このタスクを実行するため、このコマンドでは最初に **Get-CsPublicProvider** コマンドレットを呼び出して、組織での使用向けに構成されているすべての公開プロバイダーのコレクションを戻します。次に、このコレクションを **Where-Object** コマンドレットにパイプ処理し、VerificationLevel プロパティが AlwaysVerifiable と等しくないプロバイダーだけを選択します。結果として、VerificationLevel プロパティに AlwaysUnverifiable または UseSourceVerification のどちらかが設定されているプロバイダーだけが選択されます。

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable"}

## 解説

フェデレーションは、2 つの組織間で信頼関係を設定してコミュニケーションを促進する手段です。フェデレーションが確立されると、2 つの組織のユーザーはインスタント メッセージを互いに送信したり、プレゼンス通知を登録したりできます。また、Lync 2013 などの SIP アプリケーションを使用して、互いに他の通信を行うこともできます。Lync Server では、1) 自組織と他組織間の直接フェデレーション、2) 自組織と公開プロバイダー間のフェデレーション、3) 自組織とサードパーティ ホスティング プロバイダー間のフェデレーションの 3 種類のフェデレーションを使用できます。

公開プロバイダーとは、一般公衆向けの SIP 通信サービスを提供する組織のことです。公開プロバイダーとフェデレーション関係を確立すると、そのプロバイダーがホストするアカウントを持つすべてのユーザーと、効率よくフェデレーションを確立できます。たとえば、Messenger (MSN) とフェデレーションを確立すると、組織のユーザーが、Messenger のインスタント メッセージ アカウントを持つすべてのユーザーと、インスタント メッセージやプレゼンス情報を交換できるようになります。

公開プロバイダーとフェデレーションを行うためには、新しい公開プロバイダーを作成して有効にする必要があります (また、公開プロバイダー側でもフェデレーション関係を作成する必要があります)。**Get-CsPublicProvider** コマンドレットを使用すると、組織での使用向けに構成されている公開プロバイダーに関する情報を戻すことができます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Get-CsPublicProvider** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPublicProvider"}

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
<td><p>1 つまたは複数の公開プロバイダーを戻すのに、ワイルドカード値を使えるようにします。たとえば、Y という文字で始まる ID を持つすべての公開プロバイダーのコレクションを戻すには、次の構文を使用します。-Filter &quot;Y*&quot;。ID のどこかに &quot;Windows&quot; という文字列値を含むすべての公開プロバイダーのコレクションを戻すには、次の構文を使用します。-Filter &quot;*Windows*&quot;。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>戻される公開プロバイダーの一意の識別子。Identity は、通常、サービスを提供する Web サイトの名前 (Yahoo!、AOL、MSN など) です。</p>
<p>ID の指定時にワイルドカードを使用することはできません。1 つまたは複数の公開プロバイダーを戻すのにワイルドカードを使用するには、代わりに Filter パラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体ではなく、中央管理ストア のローカル レプリカから公開プロバイダーのデータを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsPublicProvider** コマンドレットでは、パイプライン入力を受け入れません。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

