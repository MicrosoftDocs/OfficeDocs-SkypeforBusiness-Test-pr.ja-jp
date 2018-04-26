---
title: Test-CsDialPlan
TOCTitle: Test-CsDialPlan
ms:assetid: e6618394-82c5-4bc2-85cc-97ac4686a1aa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399024(v=OCS.15)
ms:contentKeyID: 48274000
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialPlan

 

_**トピックの最終更新日:** 2015-03-09_

電話番号のテストをダイヤル プラン (以前はロケーション プロファイルと呼ばれていました) に対して行い、その番号に適用される正規化ルールと、その正規化ルールが適用された後の変換された番号を戻します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsDialPlan -DialedNumber <PhoneNumber> -Dialplan <LocationProfile>

## 例

## 例 1

この例では、site:Redmond の Identity を持つダイヤル プランに対してテストを実行します。最初に、**Get-CsDialPlan** コマンドレットを実行して、site:Redmond の Identity を持つダイヤル プランを取得します。次に、このダイヤル プラン オブジェクトは **Test-CsDialPlan** コマンドレットにパイプ処理され、これにより、ダイヤル プランが電話番号 14255559999 に対してテストされます。出力は、一致するパターンを持つ音声正規化ルールが適用された後の DialedNumber になります。一致するパターンを持つ正規化ルールがサイト内に複数ある場合、Priority の値が最も小さいルールが適用されます。DialedNumber 値に一致するパターンのルールが存在しない場合 (たとえば、正規化ルールが 11 桁の番号のパターンに一致する場合に、7 桁の番号を指定した場合)、値は戻りません。

このコマンドの出力には、電話番号と正規化ルールが含まれます。正規化ルールには多数のプロパティがあり、既定では、このプロパティの出力は省略記号 (...) で省略されます。戻された音声正規化ルールのプロパティと値をすべて表示するには、出力を画面に表示する前に **Format-List** コマンドレットにパイプ処理します。これにより、電話番号と正規化ルールが個別の行に表示され、正規化ルールのプロパティと値は画面に収まるように折り返されます。

    Get-CsDialPlan -Identity site:Redmond | Test-CsDialPlan -DialedNumber 14255559999 | Format-List

## 例 2

例 2 は例 1 とほとんど同じ内容ですが、Get 操作の結果を直接 **Test-CsDialPlan** コマンドレットにパイプ処理する代わりに、そのオブジェクトを変数 $a に格納したうえで、テスト実行時に参照されるダイヤル プラントして使用するために DialPlan パラメーターの値として渡している点が異なります。

例 1 の場合と同様に、出力を **Format-List** コマンドレットにパイプ処理して、音声正規化ルールの情報を既定よりも多く表示できるようにして、このコマンドを完了します。

    $a = Get-CsDialPlan -Identity site:Redmond
    Test-CsDialPlan -DialedNumber 14255559999 -Dialplan $a | Format-List

## 例 3

この例では、Lync Server 展開内で定義されたすべてのダイヤル プランに対し、ダイヤル プラン テストを実行します。まず、**Get-CsDialPlan** コマンドレットを (パラメーターを指定せずに) 実行して、すべてのダイヤル プランを取得します。次に、返されたダイヤル プランのコレクションを **Test-CsDialPlan** コマンドレットにパイプ処理します。これにより、コレクション内の各ダイヤル プランが電話番号 2065559999 に対してテストされます。その出力は、変換後の番号および適用された音声正規化ルール (コレクション内のダイヤル プランごと) の一覧になります。特定のダイヤル プランの DialedNumber 値に適用される、ダイヤル プラン内の音声正規化ルールが存在しない場合 (たとえば、正規化ルールが 11 桁の番号のパターンに一致する場合に、7 桁の番号を指定した場合)、一覧内でのそのダイヤル プランの行は空白になります。

既定の出力では、適用された音声正規化ルールの全体は表示されません。例 1 と 2 では、テストの結果を **Format-List** コマンドレットにパイプ処理することで、出力全体を表示することができました。この例では、出力を **Format-Table** コマンドレットにパイプ処理し、Wrap パラメーターを指定します。これにより、表形式で各エントリが表示されますが (1 列は変換後の番号用、1 列は適用された音声正規化ルール用)、出力は折り返されるので、正規化ルールは列内で折り返されます。

    Get-CsDialPlan | Test-CsDialPlan -DialedNumber 2065559999 | Format-Table -Wrap

## 解説

このコマンドレットを使用すると、ダイヤル プランを特定の電話番号に割り当てた結果を表示できます。ダイヤル プランは、正規化ルールの適用方法など、エンタープライズ VoIP ユーザーが通話をするのに必要な情報を提供します。ダイヤルした番号とダイヤル プランを指定すると、このコマンドレットは、ダイヤル プラン内のどの正規化ルールが適用されるのか、および変換後の番号を確認します。

このコマンドレットを使用すると、番号変換時の問題を解決したり、特定の番号に対するルールの適用を確認したりすることができます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーは **Test-CsDialPlan** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialPlan"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>必須</p></td>
<td><p>PhoneNumber</p></td>
<td><p>Dialplan パラメーターで指定したダイヤル プランをテストする電話番号です。</p>
<p>完全なデータ型: Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>Dialplan</em></p></td>
<td><p>必須</p></td>
<td><p>LocationProfile</p></td>
<td><p>DialedNumber パラメーターで指定した番号をテストするダイヤル プランへの参照を含んだオブジェクトです。</p>
<p>完全なデータ型: Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile オブジェクト。ダイヤル プラン オブジェクトのパイプ処理された入力を受け入れます。

## 戻り値の種類

Microsoft.Rtc.Management.Voice.LocationProfileTestResult 型のオブジェクトを戻します。

## 関連項目

#### その他のリソース

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)

