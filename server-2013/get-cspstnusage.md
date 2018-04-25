---
title: Get-CsPstnUsage
TOCTitle: Get-CsPstnUsage
ms:assetid: 9dc82b88-303b-4678-8298-0dbc769f6781
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412734(v=OCS.15)
ms:contentKeyID: 48272994
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPstnUsage

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用されている公衆交換電話網 (PSTN) 使用法レコードの情報を戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPstnUsage [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

このコマンドは、組織で使用できるグローバルな PSTN 使用法の一覧を戻します。

    Get-CsPstnUsage

## 例 2

この例のコマンドは、定義済みのすべての PSTN 使用法の一覧を、出力の各行に 1 つの使用法が表示された形式で戻します。**Get-CsPstnUsage** コマンドレットを単独で呼び出すと、ID および使用法の一覧が戻されます。使用法の一覧に 3 つまたは 4 つ以上のエントリが含まれている場合、出力では一覧がこのように省略されます。

Usage : {Internal, Local, Long Distance, International...}

この例のコマンドを使用して、使用法の一覧のみを表示します。出力は、このようになります。

Internal

Local

Long Distance

International

Restricted

    (Get-CsPstnUsage).Usage

## 例 3

このコマンドは、名前の中に文字列 "tern" があるすべての PSTN 使用法の名前を戻します。たとえば、このコマンドは、"Internal" および "International" は戻しますが、"Local" または "Long Distance" は戻しません。

このコマンドの最初の部分では、**Get-CsPstnUsage** コマンドレットがかっこで囲まれています。これは、まず、すべての PSTN 使用法を取得することを意味します。.Usage プロパティは、PSTN 使用法の使用法情報のみを戻し、ID は戻しません。次に、使用法の一覧は **ForEach-Object** コマンドレットにパイプ処理され、これにより、使用法の文字列が 1 つずつ検索されます。If ステートメントは、現在の使用法の文字列を文字列 "\*tern\*" (\* はワイルドカード) に対して照合し、このパターンに一致するものを表示します。

    (Get-CsPstnUsage).Usage | ForEach-Object {if ($_ -like "*tern*") {$_}}

## 解説

PSTN 使用法は、呼び出しの認証に使用する文字列値です。PSTN 使用法は、音声ポリシーをルートにリンクします。**Get-CsPstnUsage** コマンドレットは、組織で使用可能な、すべての PSTN 使用法の一覧を取得します。

このコマンドレットを実行できるユーザー: 既定では、**Get-CsPstnUsage** コマンドレットをローカルで実行する権限があるのは、RTCUniversalUserAdmins および RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPstnUsage"}

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
<td><p>Filter パラメーターにより、特定のワイルドカード文字列に一致する ID を持つ PSTN 使用法のみを取得できます。ただし、PSTN 使用法で使用可能な唯一の ID は Global なので、このパラメーターはこのコマンドレットでは機能しません。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>これらの設定を適用するレベルです。PSTN 使用法に適用できる唯一の ID は Global です。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>メインの 中央管理ストア からではなくローカルのデータ ストアから、PSTN 使用法の情報を取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

**Get-CsPstnUsage** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PSTNUsages オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Set-CsPstnUsage](set-cspstnusage.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

