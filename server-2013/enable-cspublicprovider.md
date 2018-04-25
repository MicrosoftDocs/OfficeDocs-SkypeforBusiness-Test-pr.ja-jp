---
title: Enable-CsPublicProvider
TOCTitle: Enable-CsPublicProvider
ms:assetid: 98370dfd-9a53-41a8-a1f3-bb7a516c3c5e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398780(v=OCS.15)
ms:contentKeyID: 48272920
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsPublicProvider

 

_**トピックの最終更新日:** 2015-03-09_

組織内で使用するために構成したパブリック プロバイダーを有効にします。パブリック プロバイダーとは、インスタント メッセージ、プレゼンス、および関連サービスを、一般公衆に対して提供する組織のことです。Lync Server には、Yahoo\!、AIM (AOL)、および Messenger (MSN) の 3 つの構成済みのパブリック プロバイダーが付属していますが、無効になっています。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Enable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Enable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドは、Identity が Messenger の公開プロバイダーを有効にします。Messenger が既に有効になっている場合は、エラーを戻します。

    Enable-CsPublicProvider -Identity "Messenger"

## 例 2

例 2 では、現在無効になっているすべての公開プロバイダーを有効にします。このタスクを実行するために、まず **Get-CsPublicProvider** コマンドレットを使用して、組織内で使用するように構成されているすべての公開プロバイダーのコレクションを戻します。このコレクションを **Where-Object** コマンドレットへパイプ処理し、Enabled プロパティが False に等しいプロバイダーのみを選択します。次に、このフィルター後のコレクションを **Enable-CsPublicProvider** コマンドレットへパイプ処理し、コレクション内の各プロバイダーを有効にします。

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Enable-CsPublicProvider

## 例 3

例 3 は、現在有効になっていない公開プロバイダーをすべて有効にします。ただし、これらのプロバイダーの確認レベルが、AlwaysVerifiable に設定されているとします。これを行うため、まず **Get-CsPublicProvider** コマンドレットを呼び出し、組織内で現在使用されているすべての公開プロバイダーのコレクションを戻します。このコレクションを **Where-Object** コマンドレットへパイプ処理し、次の 2 つの条件を満たすプロバイダーを選び出します。その条件は、1) VerificationLevel プロパティが AlwaysVerifiable に等しいこと、および 2) Enabled プロパティが False に等しいことです (-and 演算子を使用して、**Where-Object** コマンドレットが、指定した条件をすべて満たすオブジェクトを選択するようにします)。次に、このフィルター後のコレクションを **Enable-CsPublicProvider** コマンドレットへパイプ処理し、コレクション内の各プロバイダーを有効にします。

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -eq "AlwaysVerifiable" -and $_.Enabled -eq $False} | Enable-CsPublicProvider

## 解説

フェデレーションは、2 つの組織間で信頼関係を設定してコミュニケーションを促進する手段です。フェデレーションが確立されると、2 つの組織のユーザーはインスタント メッセージを互いに送信したり、プレゼンス通知を登録したりできます。また、Lync 2013 などの SIP アプリケーションを使用して、互いに他の通信を行うこともできます。Lync Server では、1) 自組織と他組織間の直接フェデレーション、2) 自組織と公開プロバイダー間のフェデレーション、3) 自組織とサードパーティ ホスティング プロバイダー間のフェデレーションの 3 種類のフェデレーションを使用できます。

公開プロバイダーとは、一般公衆向けの SIP 通信サービスを提供する組織のことです。公開プロバイダーとフェデレーション関係を確立すると、そのプロバイダーがホストするアカウントを持つすべてのユーザーと、効率よくフェデレーションを確立できます。たとえば、Messenger (MSN) とのフェデレーションを確立すると、組織のユーザーが、MSN Messenger のインスタント メッセージ アカウントを持つすべてのユーザーと、インスタント メッセージやプレゼンス情報を交換できるようになります。

公開プロバイダーとフェデレーションを行うためには、新しい公開プロバイダーを作成して有効にする必要があります (また、公開プロバイダー側でもフェデレーション関係を作成する必要があります)。公開プロバイダーは作成時に有効にすることも、**Enable-CsPublicProvider** コマンドレットを使用して後で有効にすることもできます。

このコマンドレットを実行できるユーザー: 既定では、**Enable-CsPublicProvider** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsPublicProvider"}

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
<td><p>有効にする公開プロバイダーの一意の識別子です。通常、Identity はサービスを提供している Web サイトの名称 (Yahoo!、AOL、MSN など) です。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider オブジェクトです。**Enable-CsPublicProvider** コマンドレットは、公開プロバイダー オブジェクトのインスタンスをパイプ処理で受け入れます。

## 戻り値の種類

なし。代わりに、Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider オブジェクトのインスタンスを有効化します。

## 関連項目

#### その他のリソース

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

