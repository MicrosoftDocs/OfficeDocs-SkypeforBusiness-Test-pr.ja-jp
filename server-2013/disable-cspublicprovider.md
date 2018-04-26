---
title: Disable-CsPublicProvider
TOCTitle: Disable-CsPublicProvider
ms:assetid: df1338ea-fe6d-45da-a39c-86108bb54ef5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398984(v=OCS.15)
ms:contentKeyID: 48273774
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsPublicProvider

 

_**トピックの最終更新日:** 2015-03-09_

組織内で使用する目的で構成されたパブリック プロバイダーを無効にします。パブリック プロバイダーとは、インスタント メッセージ、プレゼンス、および関連サービスを、一般公衆に対して提供する組織のことです。Lync Server には、Yahoo、AIM (AOL)、および Messenger (MSN) の 3 つの構成済みのパブリック プロバイダーが付属していますが、無効になっています。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Disable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Disable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 は、Messenger という ID を持つ公開プロバイダーを無効にします。MSN が既に無効になっている場合、このコマンドはエラーを返します。

    Disable-CsPublicProvider -Identity "Messenger"

## 例 2

例 2 では、現在有効になっているすべての公開プロバイダーを無効にします。この処理を行うため、コマンドはまず、**Get-CsPublicProvider** コマンドレットを使用して、組織内で現在使用されているすべての公開プロバイダーのコレクションを戻します。次に、このコレクションは **Where-Object** コマンドレットにパイプ処理され、Enabled プロパティが True と等しいプロバイダーのみを選択します。次に、このコレクションは **Disable-CsPublicProvider** コマンドレットにパイプ処理され、これにより、コレクション内の各プロバイダーが無効にされます。

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $True} | Disable-CsPublicProvider

## 例 3

例 3 のコマンドでは、現在有効になっていて、確認レベルが AlwaysVerifiable に設定されているすべての公開プロバイダーを無効にします。このタスクを実行するため、コマンドはまず、**Get-CsPublicProvider** コマンドレットを呼び出して、組織内で現在使用されているすべての公開プロバイダーのコレクションを戻します。次に、このコレクションが **Where-Object** コマンドレットにパイプ処理されます。このコマンドレットでは、次の 2 つの条件を満たすプロバイダーを選択します。1) VerificationLevel プロパティが AlwaysVerifiable に等しい、および 2) Enabled プロパティが True に等しい (-and 演算子は **Where-Object** コマンドレットに、オブジェクトが選択されるには、指定したすべての条件をオブジェクトが満たす必要があることを指示します)。次に、このコレクションは **Disable-CsPublicProvider** コマンドレットにパイプ処理され、これにより、コレクション内の各プロバイダーが無効にされます。

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable" -and $_.Enabled -eq $True} | Disable-CsPublicProvider

## 解説

フェデレーションは、2 つの組織が組織間のコミュニケーションを促進する信頼関係を設定できるようにするための手段です。フェデレーションが確立されると、2 つの組織のユーザーはインスタント メッセージの送受信やプレゼンス通知の登録ができ、Lync 2013 のような SIP アプリケーションを使用して互いに通信することもできます。Lync Server では、次の 3 種類のフェデレーションが可能です。1) 自組織と他組織間の直接フェデレーション、2) 自組織と公開プロバイダー間のフェデレーション、3) 自組織とサードパーティ ホスティング プロバイダー間のフェデレーション。

公開プロバイダーとは、一般公衆向けのセッション開始プロトコル (SIP) 通信サービスを提供する組織のことです。公開プロバイダーとフェデレーション関係を確立すると、そのプロバイダーがホストするアカウントを持つすべてのユーザーと、効率よくフェデレーションを確立できます。たとえば、Messenger (MSN) とフェデレーションを確立すると、自組織のユーザーが、Messenger のインスタント メッセージ アカウントを持つすべてのユーザーと、インスタント メッセージやプレゼンス情報を交換できるようになります。

公開プロバイダーとフェデレーションを行うためには、新しい公開プロバイダーを作成して有効にする必要があります (また、公開プロバイダー側でもフェデレーション関係を作成する必要があります)。公開プロバイダーを作成する場合は、フェデレーション関係を有効または無効にするオプションを使用できます。公開プロバイダーが有効な場合は、自組織のユーザーが、公開プロバイダーのアカウントを持つユーザーと、インスタント メッセージやプレゼンス情報を交換できるようになります。公開プロバイダーが無効な場合は、自組織のユーザーが、公開プロバイダーのアカウントを持つユーザーとコミュニケーションを行う機能は中断され、公開プロバイダーを再び有効にするまでは中断されたままになります。プロバイダー関係を一時的に中断する必要がある場合は、**Disable-CsPublicProvider** コマンドレットを使用して実行できます。プロバイダーを完全に削除することを希望する場合は、**Remove-CsPublicProvider** コマンドレットを使用します。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが **Disable-CsPublicProvider** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsPublicProvider"}

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
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>削除しようとする公開プロバイダーに関する一意の識別子です。Identity は、通常、サービスを提供する Web サイトの名前 (Yahoo!、AOL、MSN など) です。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>DisplayPublicProvider オブジェクト</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider オブジェクト。**Disable-CsPublicProvider** コマンドレットは、公開プロバイダー オブジェクトに関する、パイプ処理されたインスタンスを受け入れます。

## 戻り値の種類

なし。代わりに、このコマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider オブジェクトのインスタンスを無効にします。

## 関連項目

#### その他のリソース

[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

