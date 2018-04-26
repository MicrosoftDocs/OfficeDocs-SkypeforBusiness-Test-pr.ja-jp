---
title: Set-CsCallParkServiceMusicOnHoldFile
TOCTitle: Set-CsCallParkServiceMusicOnHoldFile
ms:assetid: af5e7573-4bfd-47b1-a92b-83b06a537158
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412836(v=OCS.15)
ms:contentKeyID: 48273275
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCallParkServiceMusicOnHoldFile

 

_**トピックの最終更新日:** 2015-03-09_

コール パーク中の発信者に対して再生するオーディオ ファイルを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsCallParkServiceMusicOnHoldFile -Content <Byte[]> -Service <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、SoothingMusic.wma というファイルを、通話が保留にされた発信者に再生するオーディオ ファイルとして設定します。この例の最初の行は、**Get-Content** コマンドレットに対する呼び出しです。このコマンドレットは、ファイルの内容をただ読み取って、この場合は変数 $a に割り当てます。値 0 を ReadCount パラメーターに渡して、**Get-Content** コマンドレットがファイル全体を (オーディオ ファイルには適用されない一行ごとの読み取りではなく) 一度に読み取るようにします。Encoding パラメーターはバイトに設定しています。これにより、変数 $a に読み込まれる内容は, .wma 形式のオーディオ ファイルではなく、バイト配列であることが、**Get-Content** コマンドレットに指示されます。

この例の行 2 では、実際にオーディオ ファイルを割り当てます。**Set-CsCallParkServiceMusicOnHoldFile** コマンドレットを呼び出して、Call Park Service が実行されているサービス ID を指定します。次に、変数 $a に読み込んだオーディオ ファイルの内容を Content パラメーターに渡します (これらの内容はバイト形式にする必要があることに注意してください)。

    $a = Get-Content -ReadCount 0 -Encoding byte "C:\MoHFiles\soothingmusic.wma"
    Set-CsCallParkServiceMusicOnHoldFile -Service ApplicationServer:pool0.litwareinc.com -Content $a

## 解説

コール パークは、ユーザーが着信通話を "保留 (パーク)" できるサービスです。通話を保留すると、通話は指定の範囲の番号に転送されて、すぐに保留状態になります。通話の保留中、Call Park Service の構成設定に基づいて、保留音を発信者に対して再生することができます。コール パーク中の発信者に対して再生するオーディオ ファイル (保留音) を変更する場合は、このコマンドレットを使用します。

Call Park Service の EnableMusicOnHold プロパティが True に設定されている場合にだけ、保留音が再生されます。このプロパティを確認するには、**Get-CsCpsConfiguration** コマンドレットを呼び出します。コール パークの構成を **New-CsCpsConfiguration** コマンドレットで作成するとき、または **Set-CsCpsConfiguration** コマンドレットでコール パークの構成を呼び出した後のどちらかに、このプロパティを設定できます。このプロパティは、既定では True になっています。

Lync Server には、Call Park Service の既定の保留音ファイルが付属しています。オーディオ ファイルを割り当てない場合は、既定のファイルが使用されます。

オーディオ ファイルは次の形式にする必要があります。Windows Media オーディオ 9、44 kHz、16 ビット、モノラル、CBR、または 32 Kbps。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsCallParkServiceMusicOnHoldFile** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCallParkServiceMusicOnHoldFile"}

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
<td><p><em>Content</em></p></td>
<td><p>必須</p></td>
<td><p>System.Byte[]</p></td>
<td><p>バイト形式でのオーディオ ファイルの内容。</p>
<p>オーディオ ファイルの内容をバイト形式で取得するには、<strong>Get-Content</strong> コマンドレットを使用します (詳細については、このトピックの「例」のセクションを参照してください)。</p></td>
</tr>
<tr class="even">
<td><p><em>Service</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>Call Park Service のあるサービスの ID。たとえば、ApplicationServer:pool0.litwareinc.com。</p></td>
</tr>
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
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Byte\[\]。保留音ファイルを含むバイト配列のパイプライン処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。

## 関連項目

#### その他のリソース

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)

