---
title: Remove-CsPublicProvider
TOCTitle: Remove-CsPublicProvider
ms:assetid: b9eec2f4-cf36-41b7-8023-67790cc8d4cd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412906(v=OCS.15)
ms:contentKeyID: 48273380
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPublicProvider

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用するように構成されたパブリック プロバイダーを削除します。パブリック プロバイダーとは、インスタント メッセージ (IM)、プレゼンス、および関連サービスを、一般公衆に対して提供する組織のことです。Lync Server には、Yahoo\!、AIM (AOL)、および Messenger (MSN) の 3 つの構成済みのパブリック プロバイダーが付属していますが、無効になっています。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsPublicProvider -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 を実行すると、Identity が Messenger の公開プロバイダーが削除されます。このコマンドの完了後、Messenger は構成済み公開プロバイダーのリストに表示されなくなります。その時点で、Messenger とのフェデレーションを再確立する唯一の方法は、このプロバイダーを再作成することです。

    Remove-CsPublicProvider -Identity "Messenger"

## 例 2

例 2 を実行すると、組織で使用するように構成されているすべての公開プロバイダーが削除されます。これを実行するには、まず、このコマンドでは **Get-CsPublicProvider** コマンドレットを使用して、使用するために現在構成されているすべての公開プロバイダーのコレクションを取得します。次に、このコレクションを **Remove-CsPublicProvider** コマンドレットにパイプ処理し、これにより、コレクション内の各プロバイダーを削除します。

    Get-CsPublicProvider | Remove-CsPublicProvider

## 例 3

例 3 を実行すると、現在無効にされているすべての公開プロバイダーが、構成済み公開プロバイダーのセットから削除されます。このタスクを実行するために、このコマンドでは最初に **Get-CsPublicProvider** コマンドレットを使用して、使用するために現在構成されたすべての公開プロバイダーのコレクションを取得しています。このコレクションを **Where-Object** コマンドレットにパイプ処理し、Enabled プロパティが False に等しいプロバイダーだけを選択しています。次に、このフィルター処理済みのコレクションを **Remove-CsPublicProvider** コマンドレットにパイプ処理し、コレクション内のすべての項目を削除しています。

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Remove-CsPublicProvider

## 解説

フェデレーションは、2 つの組織間で信頼関係を設定してコミュニケーションを促進する手段です。フェデレーションが確立されると、2 つの組織のユーザーはインスタント メッセージを互いに送信したり、プレゼンス通知を登録したりできます。また、Lync 2013 などの SIP アプリケーションを使用して、互いに他の通信を行うこともできます。Lync Server では、1) 自組織と他組織間の直接フェデレーション、2) 自組織と公開プロバイダー間のフェデレーション、3) 自組織とサードパーティ ホスティング プロバイダー間のフェデレーションの 3 種類のフェデレーションを使用できます。

公開プロバイダーとは、一般公衆向けの SIP 通信サービスを提供する組織のことです。公開プロバイダーとフェデレーション関係を確立すると、そのプロバイダーがホストするアカウントを持つすべてのユーザーと、効率よくフェデレーションを確立できます。たとえば、Messenger (MSN) とフェデレーションを確立すると、組織のユーザーが、Messenger のインスタント メッセージ アカウントを持つすべてのユーザーと、インスタント メッセージやプレゼンス情報を交換できるようになります。

公開プロバイダーとフェデレーションを行うためには、新しい公開プロバイダーを作成して有効にする必要があります (また、公開プロバイダー側でもフェデレーション関係を作成する必要があります)。後でこの関係を終了する場合は、**Remove-CsPublicProvider** コマンドレットを使用してその公開プロバイダーを削除できます。公開プロバイダーを削除すると、そのプロバイダーがフェデレーション パートナーのリストから削除されます。その時点で、関係を再確立する唯一の方法は、そのプロバイダーを再作成することです。関係を一時的に中断する場合は、代わりに **Disable-CsPublicProvider** コマンドレットを使用します。公開プロバイダーを無効にしても、そのプロバイダーはフェデレーション パートナーのリストからは削除されません。代わりに、そのプロバイダーを無効とするマークが付けられ、自組織とそのプロバイダー間の通信が中断されるだけです。関係を再確立するために、**Enable-CsPublicProvider** コマンドレットを使用してプロバイダーを再度有効にできます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Remove-CsPublicProvider** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPublicProvider"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>削除する公開プロバイダーの一意の識別子。Identity は、通常、サービスを提供する Web サイトの名前 (Yahoo!、AOL、MSN など) です。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider オブジェクト。**Remove-CsPublicProvider** コマンドレットは、公開プロバイダー オブジェクトのパイプライン処理されたインスタンスを受け入れます。

## 戻り値の種類

なし。代わりに、Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider オブジェクトのインスタンスを削除します。

## 関連項目

#### その他のリソース

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

