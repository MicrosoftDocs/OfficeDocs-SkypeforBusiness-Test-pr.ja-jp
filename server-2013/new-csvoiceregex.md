---
title: New-CsVoiceRegex
TOCTitle: New-CsVoiceRegex
ms:assetid: a1a498b7-8353-40bd-9c02-424c95743ec3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412751(v=OCS.15)
ms:contentKeyID: 48273134
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRegex

 

_**トピックの最終更新日:** 2015-03-09_

電話番号を他の形式に変換するための正規表現のパターンと変換を作成します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsVoiceRegex -AtLeastLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    New-CsVoiceRegex -ExactLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## 例

## 例 1

この例では、新しい正規表現のパターンと変換を作成します。この表現には、長さが 7 文字ちょうどであるパターン (-ExactLength 7) が含まれ、照合する番号のうち最初の 3 桁が削除 (-DigitsToStrip 3) されます。この正規表現を使用して作成する Pattern は ^\\d{3}(\\d{4})$ になり、Translation は $1 になります。たとえば、5551212 という番号はこのパターンと照合され、変換結果は 1212 になります。つまり、7 桁の番号のうち最初の 3 文字が削除されます。

    $regex = New-CsVoiceRegex -ExactLength 7 -DigitsToStrip 3

## 例 2

この例でも、新しい正規表現のパターンと変換を作成しますが、その後、これらの値を使用して新しい音声正規化ルールを作成します。最初の行では **New-CsVoiceRegEx** コマンドレットを呼び出して正規表現を作成しますが、この表現と照合される番号は長さが少なくとも 7 文字 (-AtLeastLength 7) であり、"1" で始まる (-StartsWith "1") ことが必要です。このコマンドの結果は、変数 $regex に割り当てられます。

2 行目では、**New-CsVoiceNormalizationRule** コマンドレットを呼び出します。新しいルールに一意の名前を割り当てます。この例では、"global/internal rule" (グローバル/社内のルール) です。次に、**New-CsVoiceRegex** コマンドレットを呼び出して作成した Pattern を、正規化ルールの Pattern として割り当てます。これは次のようになります。-Pattern $regex.Pattern。Translation についても同様に、**New-CsVoiceRegex** コマンドレットを呼び出して作成した Translation を割り当てます。これは次のようになります。-Translation $regex.Translation。

注: この例で作成した Pattern は ^(1\\d{5}\\d+)$ です。これを解読すると、1 (1) で始まり、その後に 5 桁が続き (\\d{5})、さらに任意の数の桁が続く (\\d+) 番号を意味します。これらを総合すると、少なくとも 7 桁の長さ (1 桁、5 桁、1 桁以上) で、"1" で始まる番号になり、要求したものはこのとおりです。

    $regex = New-CsVoiceRegex -AtLeastLength 7 -StartsWith "1"
    New-CsVoiceNormalizationRule "global/internal rule" -Pattern $regex.Pattern -Translation $regex.Translation

## 解説

正規表現は、文字パターンを照合する目的で使用します。Lync Server は正規表現を使用して電話番号と各種形式の間で相互に変換を行いますが、この中にはダイヤルした番号、E.164、ローカルの構内交換機 (PBX)、および公衆交換電話網 (PSTN) の各形式が含まれます。正規表現の構文と形式のルールを理解するまでは、これらの変換ルールの定義は混乱を招く可能性があります。**New-CsVoiceRegex** コマンドレットには、特定の条件を指定するとその正規表現を生成することができるパラメーターが用意されています。

このコマンドレットを使用して、正規化ルール (**New-CsVoiceNormalizationRule** コマンドレット) や発信の変換ルール (**New-CsOutboundTranslationRule** コマンドレット) の Pattern 値および Translation 値と、ボイス ルート (**New-CsVoiceRoute** コマンドレット) の NumberPattern 値に使用する正規表現を生成することができます。

このコマンドレットを実行できるユーザー: 既定では、**New-CsVoiceRegex** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRegex"}

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
<td><p><em>AtLeastLength</em></p></td>
<td><p>必須</p></td>
<td><p>System.Int32</p></td>
<td><p>表現と照合する文字列 (電話番号) に対して要求する最小の長さ。たとえば、長さが少なくとも 7 桁 (または 7 文字) であることが必要な番号にのみ影響を及ぼす正規化ルールを定義する場合は、このパラメーターに対して 7 という値を指定します。</p>
<p>このパラメーターまたは ExactLength パラメーターのどちらかの値を入力する必要があります。両方に対して値を入力することはできません。</p></td>
</tr>
<tr class="even">
<td><p><em>ExactLength</em></p></td>
<td><p>必須</p></td>
<td><p>System.Int32</p></td>
<td><p>正規表現と照合する必要のある文字列 (電話番号) の長さ。たとえば、10 桁の番号にのみ影響を及ぼす正規化ルールが必要な場合は、このパラメーターに対して 10 という値を指定します。</p>
<p>このパラメーターまたは AtLeastLength パラメーターのどちらかの値を入力する必要があります。両方に対して値を入力することはできません。</p></td>
</tr>
<tr class="odd">
<td><p><em>DigitsToPrepend</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>電話番号の先頭に追加する文字または番号を指定する文字列。このパラメーターに対して入力した値は Translation の値に影響し、正規表現の Pattern と照合する番号の先頭に文字を追加します。たとえば、パターンと照合する番号が 5551212 であり、DigitsToPrepend の値が 425 の場合は、変換後の番号は 4255551212 になります (他の変換が適用されていないことを想定した場合)。</p></td>
</tr>
<tr class="even">
<td><p><em>DigitsToStrip</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Int32</p></td>
<td><p>文字列 (電話番号) の先頭から削除する文字の数。たとえば、番号 2065551212 を入力し、DigitsToStrip が 3 の場合は、この番号は 5551212 に変換されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>StartsWith</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>文字列 (電話番号) の最初の文字。文字列が、StartsWith パラメーターで指定した文字列で始まっていない場合は、その文字列は正規表現と照合されません。たとえば、StartsWith に対して &quot;+1&quot; という値を指定した場合は、&quot;+1&quot; で始まる番号のみがこのパターンと照合され、変換されます。StartsWith 文字列の文字の数は、ExactLength および AtLeastLength の合計に含まれることに注意してください。たとえば、ExactLength に 10、StartsWith に +1 という文字列を指定した場合、合計が 10 桁であるため、+1 の後に続く 8 文字の長さの電話番号が照合されることになります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.Voice.OcsVoiceRegex 型のオブジェクトが作成されます。

## 関連項目

#### その他のリソース

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[New-CsVoiceRoute](new-csvoiceroute.md)

