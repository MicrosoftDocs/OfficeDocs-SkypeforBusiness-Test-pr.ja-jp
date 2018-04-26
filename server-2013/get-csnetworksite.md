---
title: Get-CsNetworkSite
TOCTitle: Get-CsNetworkSite
ms:assetid: 9627869d-101f-4668-bee2-01fce1d84cbd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398766(v=OCS.15)
ms:contentKeyID: 48272944
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkSite

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) または Enhanced 9-1-1 (E9-1-1) に対して定義されている、1 つまたは複数のネットワーク サイトを取得します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkSite [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

**Get-CsNetworkSite** コマンドレットをパラメーターを指定せずに呼び出すと、CAC または E9-1-1 に対して構成されている、Lync Server 展開内のすべてのネットワーク サイトを戻します。

    Get-CsNetworkSite

## 例 2

このコマンドは ID (定義上は NetworkSiteID) が Redmond であるサイトを取得します。

    Get-CsNetworkSite -Identity Redmond

## 例 3

例 3 のコマンドでは、**Get-CsNetworkSite** コマンドレットに Filter パラメーターを指定して呼び出しています。Filter パラメーターの値が NA\* であるため、このコマンドは文字列 NA で始まる任意の文字数の Identity のサイトをすべて取得します。これにより、NARedmond、NAVancouver、または NAChicago のようなサイトが戻されます。

    Get-CsNetworkSite -Filter NA*

## 例 4

例 4 では、**Get-CsNetworkSite** コマンドレットおよび **Where-Object** コマンドレットの 2 つのコマンドレットを使用して、NorthAmerica 地域に含まれるすべてのサイトを取得します。まず **Get-CsNetworkSite** コマンドレットをパラメーターを指定せずに呼び出し、すべてのネットワーク サイトを取得します。次に、このサイトのコレクションを **Where-Object** コマンドレットへパイプ処理し、コレクションをフィルタリングして、NetworkRegionID プロパティが NorthAmerica に等しい (-eq) コレクション内のサイトをすべて探します。

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"}

## 解説

ネットワーク サイトは、CAC または E9-1-1 展開の各地域内において構成されるオフィスまたは拠点です。このコマンドレットは、1 つまたは複数の既存のサイトの設定を取得します。

このコマンドレットを実行できるユーザー: 既定では、**Get-CsNetworkSite** コマンドレットをローカルで実行する権限があるのは、RTCUniversalUserAdmins および RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkSite"}

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
<td><p>サイトの ID とフィルター値の照合に基づき、複数のサイトを取得できるワイルドカード文字列です。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>取得するネットワーク サイトの一意の識別子です。サイトはグローバル スコープでのみ作成されるため、スコープを指定する必要はありません。その代わりに、サイト ID のみを指定する必要があります (これはネットワーク サイトの NetworkSiteID と同じ値であることに注意してください)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>ネットワーク サイトの情報を、中央管理ストア 本体からではなく、中央管理ストア のローカル レプリカから取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 型のオブジェクトを取得します。

## 関連項目

#### その他のリソース

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

