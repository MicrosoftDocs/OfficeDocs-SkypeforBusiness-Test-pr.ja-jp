---
title: Test-CsComputer
TOCTitle: Test-CsComputer
ms:assetid: 0b33d951-510d-445c-9b01-c6431fda6d47
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398162(v=OCS.15)
ms:contentKeyID: 48271235
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsComputer

 

_**トピックの最終更新日:** 2015-03-09_

**Test-CsComputer** コマンドレットを実行して、ローカル コンピューターで実行されている Lync Server サービスの状態を確認します。また、このコマンドレットを実行して、Lync Server の適切な Active Directory グループがコンピューター上の対応するローカル グループに追加されており、コンピューターの必要なファイアウォール ポートが開いていることを確認します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsComputer [-Report <String>]

## 例

## 例 1

例 1 のコマンドを実行して、ローカル コンピューターのサービスのアクティブ化の状態を確認します。Verbose パラメーターをコマンドに指定して、処理の成功 (または失敗) が画面上で完全に報告されることを確認します。

    Test-CsComputer -Verbose

## 例 2

例 2 のコマンドを実行して、ローカル コンピューターのサービスのアクティブ化の状態についても確認します。また、このコマンドを実行して、アクティブ化の状態に関する詳細な情報をファイル C:\\Logs\\Computer.html に書き込みます。このログを生成するには、Report パラメーターの後に、情報を記録するログ ファイルへの完全なパスを指定します。

    Test-CsComputer -Verbose -Report C:\Logs\Computer.html

## 解説

**Test-CsComputer** コマンドレットは、Lync Server "代理トランザクション" の一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信などの一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) などのアプリケーションから自動で実行することもできます。

**Test-CsComputer** コマンドレットはローカル コンピューター上でのみ実行でき、これを実行して、そのコンピューター上のすべての Lync Server サービスの状態を確認します。また、このコマンドレットを実行して、コンピューターの適切なファイアウォール ポートが開いているかどうかを確認したり、Lync Server をインストールしたときに作成された Active Directory グループが対応するローカル グループに追加されているかどうかを確認したりします。たとえば、**Test-CsComputer** コマンドレットを実行して、Active Directory グループ RTCUniversalUserAdmins がローカルの Administrators グループに追加されていることを確認します。

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
<td><p><em>Report</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレット実行時に作成されるログ ファイルのファイル パスを指定できるようにします。次に例を示します。-Report &quot;C:\Logs\Computer.html&quot;。このファイルが既に存在する場合は、コマンドレットの実行時に上書きされます。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsComputer** コマンドレットはパイプライン処理された入力を受け入れません。

## 戻り値の種類

**Test-CsComputer** コマンドレットを実行すると、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)

