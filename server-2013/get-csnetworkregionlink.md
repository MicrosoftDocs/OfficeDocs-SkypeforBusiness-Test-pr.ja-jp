---
title: Get-CsNetworkRegionLink
TOCTitle: Get-CsNetworkRegionLink
ms:assetid: dc5cb988-13e2-4af4-8b36-0aaa58ebf1c5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398972(v=OCS.15)
ms:contentKeyID: 48273750
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegionLink

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 用に構成されたネットワーク地域間の 1 つ以上のリンクを取得します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegionLink [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

例 1 は、Lync Server の展開内で定義されたすべてのネットワーク地域リンクを取得します。

    Get-CsNetworkRegionLink

## 例 2

例 2 では、Identity が NA\_EMEA である (最大でも) 1 つのネットワーク地域リンクに関する情報を取得します。

    Get-CsNetworkRegionLink -Identity NA_EMEA

## 例 3

この例では、Filter パラメーターを使用して、リンクの名前 (Identity) の中に文字列 EMEA が含まれているすべてのネットワーク地域リンクを取得します。\* という文字が、文字列 EMEA の前と後にあることに注意してください。これは、この文字列の前または後ろに、任意の 1 文字以上が存在してよいことを意味します。文字列 EMEA は単純に、Identity の中のどこかに含まれている必要があります。この結果、NA\_EMEA、EMEA\_APAC、および EMEA2\_SA のような名前を持つリンクが取得されます。

    Get-CsNetworkRegionLink -Filter *EMEA*

## 例 4

この例では、リンクされている 2 つの地域のいずれかに EMEA という文字列が含まれているすべてのネットワーク地域リンクを取得します。この例ではまず、パラメーターを指定せずに **Get-CsNetworkRegionLink** コマンドレットを呼び出して、すべての地域リンクを取得します。次に、このリンクのコレクションは **Where-Object** コマンドレットにパイプ処理されます。**Where-Object** コマンドレットはコレクションの各メンバーを 1 つずつ参照し、NetworkRegionID1 プロパティと NetworkRegionID2 プロパティの値をチェックします。これらのプロパティのいずれかが EMEA に等しい場合、言い換えると、NetworkRegionID1 が EMEA に等しい (-eq) または (-or) NetworkRegionID2 が EMEA に等しい (-eq) 場合は、その項目をコレクション内に保持し、表示します。

    Get-CsNetworkRegionLink | Where-Object {$_.NetworkRegionID1 -eq "EMEA" -or $_.NetworkRegionID2 -eq "EMEA"}

## 解説

あるネットワーク内の地域どうしは、物理的な WAN 接続を介してリンクされます。このコマンドレットは、Lync Server の展開用のネットワーク構成設定内で定義されている 1 つ以上の地域リンクを取得します。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーは **Get-CsNetworkRegionLink** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegionLink"}

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
<td><p>ワイルドカード文字列に一致する Identity 値に基づいてネットワーク リンクを取得するために使用するワイルドカード文字列を受け入れます。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>取得するネットワーク地域リンクの一意の識別子です。ネットワーク地域リンクはグローバル スコープのみで作成されるので、この識別子でスコープを指定する必要はありません。代わりに、リンクを識別する一意の名前を示す文字列を格納しています (この値は NetworkRegionLinkID と同じであることに注意してください)。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体からではなく、中央管理ストア のローカル レプリカからネットワーク地域リンク情報を取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 型の 1 つ以上のオブジェクトを取得します。

## 関連項目

#### その他のリソース

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)

