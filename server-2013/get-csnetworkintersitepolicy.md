---
title: Get-CsNetworkInterSitePolicy
TOCTitle: Get-CsNetworkInterSitePolicy
ms:assetid: a4a64048-f8d7-483a-9565-0c6f3b0937b7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412769(v=OCS.15)
ms:contentKeyID: 48273057
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterSitePolicy

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 構成内で直接接続されているサイト間に帯域幅制限を定義する 1 つ以上のネットワーク サイト間ポリシーを取得します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterSitePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

**Get-CsNetworkInterSitePolicy** コマンドレットをパラメーターなしで呼び出して、2 つの直接接続されたネットワーク サイト間で定義されているすべてのネットワーク サイト ポリシーを取得しています。

    Get-CsNetworkInterSitePolicy

## 例 2

この例では、Reno\_Portland という ID を持つネットワーク サイト ポリシーを取得しています。

    Get-CsNetworkInterSitePolicy -Identity Reno_Portland

## 例 3

例 3 では、ID 値の一部に文字列 Reno が含まれるネットワーク サイト ポリシーをすべて取得しています。Filter パラメーターに渡される値に含まれているワイルドカード文字 (\*) は、"任意の文字または文字のセット" を示します。つまり、文字列 \*Reno\* は、任意の 1 つまたは複数の文字で始まり、次に文字列 Reno が続き、さらに任意の 1 つまたは複数の文字が続く ID 値と一致します。

    Get-CsNetworkInterSitePolicy -Filter *Reno*

## 例 4

この例では、帯域幅ポリシーのプロファイルが割り当てられていないすべてのネットワーク サイト ポリシーを取得しています。このコマンドでは、まず **Get-CsNetworkInterSitePolicy** コマンドレットを呼び出し、例 1 と同様に、すべてのネットワーク サイト ポリシーのコレクションを取得します。次に、このコレクションを **Where-Object** コマンドレットへパイプ処理します。**Where-Object** コマンドレットは、コレクションを帯域幅ポリシーのプロファイルが割り当てられていないサイト ポリシーのみに絞り込みます。これは、各サイト ポリシーの BWPolicyProfileID プロパティが Null ($null) と等しい (-eq) かどうかを比較することによって行われます。

    Get-CsNetworkInterSitePolicy | Where-Object {$_.BWPolicyProfileID -eq $null}

## 解説

ネットワーク サイトが直接リンクを共有している場合、これらの 2 つのサイト間にオーディオ接続およびビデオ接続の帯域幅制限を定義できます。このコマンドレットを使用すると、帯域幅制限の設定と直接接続されたサイトを関連付ける 1 つ以上のネットワーク サイト ポリシーを取得できます。

このコマンドレットを実行できるユーザー: 既定では、**Get-CsNetworkInterSitePolicy** コマンドレットをローカルで実行する権限があるのは、RTCUniversalUserAdmins および RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterSitePolicy"}

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
<td><p>ワイルドカード文字を含む文字列です。このワイルドカード文字列と一致する Identity 値を持つポリシーを検索します。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>取得するネットワーク サイト ポリシーを表す一意の識別子です。ネットワーク サイト ポリシーはグローバル スコープでのみ作成されます。そのため、この識別子にスコープを指定する必要はありません。代わりに、そのポリシーを識別する一意の名前である文字列が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>ネットワーク サイト間ポリシーの情報を、中央管理ストア 本体からではなく、中央管理ストア のローカル レプリカから取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType 型のオブジェクトを取得します。

## 関連項目

#### その他のリソース

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)

