---
title: Set-CsPstnUsage
TOCTitle: Set-CsPstnUsage
ms:assetid: ecba9ed6-4845-4035-933e-0c540d530b72
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399069(v=OCS.15)
ms:contentKeyID: 48273933
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnUsage

 

_**トピックの最終更新日:** 2015-03-09_

許可されている公衆交換電話網 (PSTN) の使用法を識別する文字列セットを変更します。このコマンドレットを使用して、PSTN 使用法の一覧に対する使用法の追加または削除を行うことができます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPstnUsage [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Usage <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

このコマンドは、現在の使用可能な PSTN 使用法の一覧に文字列 "International" を追加します。

    Set-CsPstnUsage -Identity global -Usage @{add="International"}

## 例 2

このコマンドは、使用可能な PSTN 使用法の一覧から文字列 "Local" を削除します。

    Set-CsPstnUsage -Identity global -Usage @{remove="Local"}

## 例 3

この例のコマンドは例 2 とまったく同じ処理を実行し、"Local" という PSTN 使用法を削除します。この例は、このコマンドで Identity パラメーターを指定しない場合を示しています。**Set-CsPstnUsage** コマンドレットで使用できる唯一の ID は Global ID なので、Identity パラメーターを省略するとその値は既定で Global に設定されます。

    Set-CsPstnUsage -Usage @{remove="Local"}

## 例 4

このコマンドは、使用法の一覧の内容をすべて International と Restricted という値に置換えます。それまでの既存の使用法はすべて削除されます。

    Set-CsPstnUsage -Usage @{replace="International","Restricted"}

## 解説

PSTN 使用法は、通話の承認で使用される文字列値です。PSTN 使用法は、音声ポリシーをルートに関連付けます。**Set-CsPstnUsage** コマンドレットは、使用法の一覧に対する電話使用法の追加または削除を行うために使用されます。この一覧は、グローバルなので、Lync Server の展開の全域でポリシーやルートによって使用できます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Set-CsPstnUsage** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnUsage"}

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
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>これらの設定を適用するスコープです。このコマンドレットの ID は常に Global です。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>PstnUsages</p></td>
<td><p>PSTN 使用法オブジェクトへの参照です。このオブジェクトは PstnUsages 型である必要があり、<strong>Get-CsPstnUsage</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Usage</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>許容される使用法の文字列一覧が含まれます。すべての文字列値がこれらのエントリに含まれる可能性があります。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages オブジェクト。PSTN 使用法オブジェクトのパイプライン処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットは、値またはオブジェクトを戻しません。代わりに、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages オブジェクトのインスタンスを構成します。

## 関連項目

#### その他のリソース

[Get-CsPstnUsage](get-cspstnusage.md)

