---
title: Get-CsVoiceRoute
TOCTitle: Get-CsVoiceRoute
ms:assetid: 422abb2d-bff3-4b9a-b18c-d8202b01f69b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425926(v=OCS.15)
ms:contentKeyID: 48271893
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceRoute

 

_**トピックの最終更新日:** 2015-03-09_

組織での使用が構成されているボイス ルートに関する情報を戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

組織で定義されているすべてのボイス ルートのプロパティを取得しています。

    Get-CsVoiceRoute

## 例 2

Route1 というボイス ルートのプロパティを取得しています。

    Get-CsVoiceRoute -Identity Route1

## 例 3

このコマンドを実行すると、ID のどこかに "test" という文字列が含まれるボイス ルート設定が表示されます。ID の末尾に test という値が含まれる文字列のみを検索するには、\*test という値を使用します。同様に、ID の先頭に test という文字列が含まれる文字列のみを検索するには、test\* という値を指定します。

    Get-CsVoiceRoute -Filter *test*

## 例 4

このコマンドを実行すると、PSTN ゲートウェイが割り当てられていないボイス ルートがすべて取得されます。最初に、**Get-CsVoiceRoute** コマンドレットを使用してすべてのボイス ルートを取得します。次に、これらのボイス ルートを **Where-Object** コマンドレットにパイプ処理します。**Where-Object** コマンドレットを実行して、取得操作結果を絞り込みます。ここでは、$\_ で表示されている各ボイス ルートの、PstnGatewayList プロパティの Count プロパティをチェックします。PSTN ゲートウェイ数が 0 の場合は、一覧は空で、ルートに定義されているゲートウェイはありません。

    Get-CsVoiceRoute | Where-Object {$_.PstnGatewayList.Count -eq 0}

## 解説

このコマンドレットを使用して、既存のボイス ルートを 1 つ以上取得します。ボイス ルートには、エンタープライズ VoIP ユーザーからの呼び出しを公衆交換電話網 (PSTN) または構内交換機 (PBX) の電話番号へルーティングする方法についての Lync Server への指示が含まれます。

このコマンドレットを使用して、ボイス ルートの情報を取得できます。この情報には、ルートが関連付けられている PSTN ゲートウェイ (存在する場合)、ルートに関連付けられている PSTN 使用法、ルートを適用する電話番号を識別する (正規表現形式の) パターン、発信者 ID 設定などが含まれます。PSTN 使用法によってボイス ルートと音声ポリシーを関連付けます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Get-CsVoiceRoute** コマンドレットのローカル実行を承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceRoute"}

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
<td><p>このパラメーターによって、渡されたワイルドカード値に基づく Get 操作の結果をフィルターします。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>ボイス ルートを一意に識別する文字列です。ID を設定しないと、組織のすべてのボイス ルートが戻されます。</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア 自体ではなく、中央管理ストア のローカル レプリカからボイス ルートを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

このコマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)

