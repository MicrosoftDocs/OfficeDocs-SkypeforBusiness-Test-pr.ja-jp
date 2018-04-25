---
title: Windows PowerShell の起動時における Lync Online への常時自動接続
TOCTitle: Windows PowerShell の起動時における Lync Online への常時自動接続
ms:assetid: 68f76c36-5dd6-48ea-b19a-d65593199e4c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362799(v=OCS.15)
ms:contentKeyID: 56270095
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows PowerShell の起動時における Lync Online への常時自動接続

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online に接続するために必要なすべてのコマンドを記憶できない場合は、ショートカット ファイルをダブルクリックして Skype for Business Online のパスワードを入力すれば Skype for Business Online に接続されるように構成することができます。

このためには、まずメモ帳 (または他のテキスト エディター) を開き、次のコマンドを貼り付け、kenmyer@litwareinc.com をお使いの Skype for Business Online アカウント名に置き換えます。

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $session = New-CsOnlineSession -Credential $credential 
    Import-PSSession $session

.PS1 ファイル拡張子を付けてファイルを保存します (例: C:\\Scripts\\LyncOnline.ps1)。

ファイルを保存した後、次の手順を実行して、Windows PowerShell を起動して起動時にスクリプトを実行するデスクトップ ショートカットを作成します。

1.  デスクトップを右クリックし、\[**新規作成**\] をクリックし、\[**ショートカット**\] をクリックします。

2.  \[**ショートカットの作成**\] ウィザードの \[**項目の場所を入力してください**\] ボックスに次のように入力し、\[**次へ**\] をクリックします (作成したスクリプト ファイルへのパスを使用することを忘れないでください)。
    
        powershell.exe -noexit C:\Scripts\LyncOnline.ps1

3.  \[**このショートカットの名前を入力してください**\] ボックスにショートカットの名前 (**Skype for Business Online** など) を入力し、\[**完了**\] をクリックします。

4.  次回、Windows PowerShell を使用して Skype for Business Online を管理するときには、新しいショートカットをダブルクリックしてパスワードを入力するだけで済みます。スクリプトが、接続を行い、新しいリモート セッションを設定する処理を行います。

通常、この新しいセッションは変数 $session には格納されません。代わりに、通常はセッション ID 1 が付与されます。このことは (少なくともセッションを閉じて終了するまでは) セッションには影響しません。このようにするため、**Remove-PSSession** コマンドレットを呼び出すと、セッション ID が必要になります。

    Remove-PSSession 1

Windows PowerShell プロンプトからこのコマンドを実行すると、Skype for Business Online セッションに付与されている ID を確認できます。

    Get-PSSession

## 関連項目

#### 概念

[Lync Online 管理用のコンピューターの構成](configuring-your-computer-for-skype-for-business-online-management.md)

