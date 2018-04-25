---
title: Test-CsVoicePolicy
TOCTitle: Test-CsVoicePolicy
ms:assetid: 4d631e36-3a9d-4ca2-913f-8c9f4e93183d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398310(v=OCS.15)
ms:contentKeyID: 48272035
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoicePolicy

 

_**トピックの最終更新日:** 2015-03-09_

電話番号を音声ポリシーに対してテストし、その電話番号のポリシーに対して使用するボイス ルートを決定します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsVoicePolicy -TargetNumber <PhoneNumber> -VoicePolicy <VoicePolicy> [-Force <SwitchParameter>] [-RouteSettings <PstnRoutingSettings>]

## 例

## 例 1

この例では、site:Redmond という ID を持つ音声ポリシーに対して音声ポリシーのテストを実行しています。まず、**Get-CsVoicePolicy** コマンドレットを実行して、ID が site:Redmond のポリシーを取得します。次に、このポリシー オブジェクトを **Test-CsVoicePolicy** コマンドレットにパイプ処理して、電話番号 +14255559999 に対してテストします。出力は、番号のパターンが TargetNumber 値と一致し、電話使用法がポリシーの電話使用法と一致する、最初のボイス ルート (ルートの Priority プロパティに基づきます) になります。一致するルートが検出されない場合 (たとえば、一致する番号のパターンが 11 桁の番号のパターンであるのに対し、7 桁の番号を指定している場合など)、Null 値が戻されます。

    Get-CsVoicePolicy -Identity site:Redmond | Test-CsVoicePolicy -TargetNumber "+14255559999"

## 例 2

例 2 は例 1 と似ていますが、取得操作の結果を **Test-CsVoicePolicy** コマンドレットに直接パイプ処理するのではなく、オブジェクトを最初に変数 $a に格納し、値としてパラメーター VoicePolicy に渡してテスト対象のポリシーとして使用するという点が異なります。

    $a = Get-CsVoicePolicy -Identity site:Redmond
    Test-CsVoicePolicy -TargetNumber "+14255559999" -VoicePolicy $a

## 例 3

この例では、Lync Server 展開内で定義されたすべての音声ポリシーに対し、音声ポリシーのテストを実行しています。まず、**Get-CsVoicePolicy** コマンドレットを (パラメーターを指定せずに) 実行して、すべての音声ポリシーを取得します。次に、戻されたポリシーのコレクションを **Test-CsVoicePolicy** コマンドレットにパイプ処理し、指定した通話先電話番号 (+12065559999) と電話使用法に基づいて、コレクションの各ポリシーに一致するルートがあるかどうかを確認します。出力は、一致したルートのリストとなり、一致した電話使用法も示されます。

    Get-CsVoicePolicy | Test-CsVoicePolicy -TargetNumber "+12065559999"

## 解説

音声ポリシーは、公衆交換電話網 (PSTN) 使用法を介してボイス ルートに関連付けられています。特定の音声ポリシーが割り当てられているユーザーからの通話は、そのポリシーにある使用法と一致する PSTN 使用法およびダイヤルした番号と一致する電話番号のパターンがあるルートを介してのみ送信することができます。**Test-CsVoicePolicy** コマンドレットを呼び出して、特定の音声ポリシーを使用するユーザーからの通話をルーティングするのに使用するルート (存在する場合) と、そのポリシーをルートに関連付ける電話使用法を決定します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Test-CsVoicePolicy** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoicePolicy"}

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
<td><p><em>TargetNumber</em></p></td>
<td><p>必須</p></td>
<td><p>PhoneNumber</p></td>
<td><p>テストの実行対象となる電話番号です。この番号は、E.164 形式 (たとえば、+14255551212) にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>VoicePolicy</em></p></td>
<td><p>必須</p></td>
<td><p>VoicePolicy</p></td>
<td><p>テストの実行対象となる音声ポリシー オブジェクトへの参照です。音声ポリシー オブジェクトは、<strong>Get-CsVoicePolicy</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドレットを実行するときに発生する可能性のある、すべての確認メッセージまたは致命的ではないエラー メッセージが表示されないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>省略可能</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>テストの実行対象となるルート設定です。ルート設定は、<strong>Get-CsRoutingConfiguration</strong> コマンドレットの呼び出しによって取得できます。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy オブジェクト。音声ポリシー オブジェクトのパイプライン処理された入力を受け入れます。

## 戻り値の種類

Microsoft.Rtc.Management.Voice.VoicePolicyTestResult 型のオブジェクトを戻します。

## 関連項目

#### その他のリソース

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)

