---
title: Set-CsNetworkInterSitePolicy
TOCTitle: Set-CsNetworkInterSitePolicy
ms:assetid: 973979bc-db2c-47a6-909e-5949a927f51c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398772(v=OCS.15)
ms:contentKeyID: 48272908
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterSitePolicy

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 構成内で直接リンクされているサイト間の帯域幅の制限を定義する、既存のネットワーク サイト間ポリシーを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterSitePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkSiteID1 <String>] [-NetworkSiteID2 <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例は、ID が Reno\_Portland のネットワーク サイト ポリシーを変更します。BWPolicyProfileID パラメーターを使用してこのネットワーク サイト ポリシーに関連する帯域幅ポリシー プロファイルを HighBWLimits に変更します。

    Set-CsNetworkInterSitePolicy -Identity Reno_Portland -BWPolicyProfileID HighBWLimits

## 解説

ネットワーク サイトが直接リンクを共有している場合、音声およびビデオ接続の帯域幅の制限をその 2 サイト間で定義することができます。このコマンドレットは、帯域幅の制限ポリシーを直接接続されている 2 つのサイトに関連付ける、ネットワーク サイト間ポリシーを変更します。

このコマンドレットを実行できるユーザー: 既定では、**Set-CsNetworkInterSitePolicy** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterSitePolicy"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このサイト ポリシーに制限を定義する帯域幅ポリシー プロファイルの Identity です。利用可能なプロファイルの一覧は、<strong>Get-CsNetworkBandwidthPolicyProfile</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>変更するネットワーク サイト ポリシーの一意の識別子です。ネットワーク サイト ポリシーはグローバル スコープでのみ作成されるので、この識別子はスコープを指定する必要がありません。その代わりに、サイト ポリシーを識別する一意の名前の文字列が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>InterNetworkSitePolicyType</p></td>
<td><p>メモリ内で変更されたサイト ポリシーへのオブジェクト参照です。このオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType 型である必要があり、<strong>Get-CsNetworkInterSitePolicy</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSiteID1</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このポリシーに関連付けられた 2 つのサイトのうちの片方の Identity (NetworkSiteID) です。NetworkSiteID1 および NetworkSiteID2 の組み合わせは一意である必要があります (たとえば、Reno と Portland に接続するように定義されたサイト ポリシーを 2 つ持つことはできません)。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID2</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このポリシーに関連付けられた 2 つのサイトのうちの片方の Identity (NetworkSiteID) です。NetworkSiteID1 および NetworkSiteID2 の組み合わせは一意である必要があります (たとえば、Reno と Portland に接続するように定義されたサイト ポリシーを 2 つ持つことはできません)。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType オブジェクトです。ネットワーク サイト間ポリシー オブジェクトのパイプ処理による入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

