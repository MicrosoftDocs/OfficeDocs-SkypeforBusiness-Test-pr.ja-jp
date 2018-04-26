---
title: Get-CsVoiceNormalizationRule
TOCTitle: Get-CsVoiceNormalizationRule
ms:assetid: 59fe1370-1cec-4cf9-8f65-029a7c2454d1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398393(v=OCS.15)
ms:contentKeyID: 48272168
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceNormalizationRule

 

_**トピックの最終更新日:** 2015-03-09_

組織で使用している音声正規化ルールに関する情報を戻します。音声正規化ルールは、電話のダイヤル要件 (外線接続の際に 9 をダイヤルするなど) を Lync Server で使用されている E.164 の電話番号形式に変換します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Get-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceNormalizationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## 例

## 例 1

この例では、組織で定義されているすべての音声正規化ルールを取得しています。

    Get-CsVoiceNormalizationRule

## 例 2

例 2 では、全サイト向けに指定されている音声正規化ルールをすべて取得しています。

    Get-CsVoiceNormalizationRule -Filter site*

## 例 3

例 3 では、s という文字がスコープに含まれるすべての音声正規化ルールを取得しています。たとえば、ここでは、すべてのサイト レベルおよびサービス レベルのルールと、RedmondEastUsers のようなスコープ名に s を含むユーザーごとのルールを戻しています。

    Get-CsVoiceNormalizationRule -Filter *s*

## 例 4

例 2 および 3 で使用しているフィルター パラメーターは、ID のスコープ部分にのみ一致します。この例では名前部分に対して検索を実行し、"seattle" という文字列を含む名前を持つルールをすべて戻しています。これを実行するため、最初に **Get-CsVoiceNormalizationRule** コマンドレットを呼び出して組織の正規化ルールをすべて取得しています。次に、このコレクションを **Where-Object** コマンドレットにパイプ処理して、Name プロパティが "seattle" という文字列と一致するコレクション内にあるすべての項目を検索しています。

    Get-CsVoiceNormalizationRule | Where-Object {$_.Name -match "seattle"}

## 解説

このコマンドレットを実行すると、指定の音声正規化ルールや音声正規化ルールのコレクションが戻されます。これらのルールは、電話の認証および呼び出しルーティングの必要部分です。これらのルールによって、番号を Lync Server 内部形式から標準 (E.164) 形式に変換する際の要件を定義します。変換する番号パターンを定義する際には、正規表現を理解していると便利です。

このコマンドレットを使用してアクセスする同様のルールによって、**Get-CsDialPlan** コマンドレットを呼び出すことで戻される NormalizationRules プロパティ経由でもアクセスできます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Get-CsVoiceNormalizationRule** コマンドレットをローカルで実行することを承認されています。RTCUniversalUserAdmins、RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceNormalizationRule"}

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
<td><p>ワイルドカード文字列を使用して、ID に基づいて正規化ルールのコレクションを戻します。フィルターは ID のスコープ部分に対してのみ機能し、名前に対しては機能しないことに注意してください。たとえば *lob* というフィルター値を設定すると、グローバル スコープ (lob という文字が含まれるスコープ) のルールがすべて戻されますが、site:Redmond/lobby という ID を持つルールは戻されません。この場合、lob が含まれるのは ID の名前の部分だけで、スコープには含まれないためです。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>ルールの一意の識別子です。このパラメーターに値を指定する場合、その値の形式はスコープ/名前の形式 (site:Redmond/Rule1 など) である必要があります。ここでは、site:Redmond がスコープで Rule1 が名前です。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>中央管理ストア自体からではなく 中央管理ストアのローカル レプリカから、音声正規化ルールを取得します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

**Get-CsVoiceNormalizationRule** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Get-CsDialPlan](get-csdialplan.md)

