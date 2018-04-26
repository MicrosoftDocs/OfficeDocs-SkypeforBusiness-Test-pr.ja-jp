---
title: Remove-CsNetworkInterSitePolicy
TOCTitle: Remove-CsNetworkInterSitePolicy
ms:assetid: daf1afc8-cce4-4192-8ba4-05d26817198e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398963(v=OCS.15)
ms:contentKeyID: 48273742
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterSitePolicy

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 構成内で直接リンクされているサイト間で帯域幅の制限を定義しているネットワーク サイト間ポリシーを削除します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsNetworkInterSitePolicy -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、Reno\_Portland という Identity を持つネットワーク サイト ポリシーを削除します。

    Remove-CsNetworkInterSitePolicy -Identity Reno_Portland

## 例 2

例 2 では、CAC 構成の中で定義されているすべてのネットワーク サイト ポリシーを削除します。まず **Get-CsNetworkInterSitePolicy** コマンドレットを呼び出して、すべてのネットワーク サイト ポリシーのコレクションを取得します。次に、コレクションを **Remove-CsNetworkInterSitePolicy** コマンドレットにパイプ処理し、コレクション内の各項目を削除します。

    Get-CsNetworkInterSitePolicy | Remove-CsNetworkInterSitePolicy

## 解説

ネットワーク サイトが 1 つの直接リンクを共有している場合は、音声とビデオの接続に対する帯域幅の制限は、これら 2 つのサイト間で定義できます。このコマンドレットでは、直接接続された 2 つのサイトに帯域幅の制限ポリシーを関連付けるネットワーク サイト ポリシーを削除します。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが **Remove-CsNetworkInterSitePolicy** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterSitePolicy"}

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
<td><p>削除するネットワーク サイト ポリシーの一意の識別子です。ネットワーク サイト ポリシーはグローバル スコープのみで作成されるので、この識別子でスコープを指定する必要はありません。代わりに、サイト ポリシーを識別する一意の名前を示す文字列を格納しています。</p></td>
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
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType オブジェクト。ネットワーク サイト間ポリシー オブジェクトのパイプ処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType 型のオブジェクトが削除されます。

## 関連項目

#### その他のリソース

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

