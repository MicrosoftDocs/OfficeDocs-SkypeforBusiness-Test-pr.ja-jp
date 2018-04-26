---
title: Set-CsOutboundTranslationRule
TOCTitle: Set-CsOutboundTranslationRule
ms:assetid: fbf82146-7884-418c-8239-66c0ca0f2ba6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg413073(v=OCS.15)
ms:contentKeyID: 48274195
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOutboundTranslationRule

 

_**トピックの最終更新日:** 2015-03-09_

既存の発信変換ルールを変更します。発信変換ルールは、構内交換機 (PBX) システムとやり取りする目的で、電話番号を地域のダイヤル形式に変換します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsOutboundTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsOutboundTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、site:Redmond/Prefix Redmond という Identity を持つグローバル発信変換ルールを変更しています。このルールが E.164 形式から 7 桁の電話番号への変換を行うという説明を追加しました。また、パターンと変換の値も指定済みです。この結果、これらのプロパティに対応する既存の値を変更することになります。これらの値によって、パターンの正規表現で指定した E.164 の番号 (この場合は +1425 で始まる 12 桁) を、最初の 5 桁を削除した 7 桁の番号に変換します。たとえば、+14255551212 という番号は、5551212 という番号に変換されます。

    Set-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond" -Description "Convert to seven digits" -Pattern '^\+1425(\d{7})$' -Translation '$1'

## 例 2

この例では、発信変換ルールの Name プロパティを変更します。この結果、このルールの Identity が変化することに注意してください。この例の最初のコマンドでは、**Get-CsOutboundTranslationRule** コマンドレットを呼び出します。site:Redmond\\OBR1 という Identity を指定し、この結果、指定した Identity を持つ 1 つの変換ルールが戻されます。このルールを表示する代わりに、このルールを変数 $a に割り当てます。この例の 2 行目では、"Outbound Rule 1" という文字列を変数 $a の Name プロパティに割り当てます。この変数は、site:Redmond/OBR1 ルールへの参照を保持しています。この例の最後の行で **Set-CsOutboundTranslationRule** コマンドレットを呼び出し、Instance パラメーターを指定し、変数 $a を渡します。ここで Identity の値として site:Redmond/OBR1 を指定して **Get-CsOutboundTranslationRule** コマンドレットを呼び出すと、何も戻されません。この Identity を持つルールはもう存在しなくなっているためです。そのようなルールは、site:Redmond/Outbound Rule 1 という Identity を持つ類似のルールによって置き換えられました。

    $a = Get-CsOutboundTranslationRule -Identity "site:Redmond/OBR1"
    $a.Name = "Outbound Rule 1"
    Set-CsOutboundTranslationRule -Instance $a

## 解説

Lync Server は、電話番号を正規化し、E.164 形式にします。ただし、構内交換機 (PBX) システムの多くは、この形式で動作できません。発信変換ルールは、番号を 仲介サーバー またはゲートウェイに送信する前に、番号を地域のダイヤル形式に変換します。このコマンドレットを呼び出して、既存の発信変換ルールを変更します。

各発信変換ルールはトランク構成に関連付けられています。つまり、このコマンドレットを使用してルールを変更すると、該当するトランク構成に影響が及びます。複数の発信変換ルールを、各構成に関連付けることもできます。したがって、各ルールに対応する Identity は単一のスコープと、そのスコープ内で一意である名前で構成されています (スコープ/名前の形式、たとえば、site:Redmond/OBR1)。ルールは、同じスコープを持つトランク構成に対して自動的に関連付けられます。トランク構成の中で発信変換ルールを変更するために推奨される方法は、**Set-CsOutboundTranslationRule** コマンドレットを呼び出すことです。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Set-CsOutboundTranslationRule** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOutboundTranslationRule"}

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
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>発信変換ルールの簡単な説明です。この説明を使用して、管理者がルールの目的を簡単に識別できるようにします。</p></td>
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
<td><p>XdsIdentity</p></td>
<td><p>変更する発信変換ルールの一意の識別子です。この Identity は、スコープと、それに続く各スコープ内で一意である名前で構成されます。たとえば、site:Redmond/OutboundRule1 です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>TranslationRule</p></td>
<td><p>発信変換ルールへのオブジェクト参照です。このオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule 型であることが必要です。このオブジェクトは、<strong>Get-CsOutboundTranslationRule</strong> コマンドレットを呼び出して取得します。</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>変換の適用先となる番号パターンを表す正規表現です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>複数の発信変換ルールのパターンと一致する番号の場合は、優先順位に従ってルールが適用されます。ルールに優先順位を割り当てるには、このパラメーターを使用します。</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>発信ルーティングの目的で番号を準備するために、パターンに一致する番号に適用する正規表現です。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule オブジェクト。発信変換ルール オブジェクトのパイプライン入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)

