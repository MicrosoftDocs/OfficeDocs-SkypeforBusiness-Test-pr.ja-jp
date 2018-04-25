---
title: 'Lync Online: Windows PowerShell 3.0 のダウンロードとインストール'
TOCTitle: Windows PowerShell 3.0 のダウンロードとインストール
ms:assetid: 39ae065d-02d7-4ce3-9e6f-6ad550a1777e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362783(v=OCS.15)
ms:contentKeyID: 56270064
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Online での Windows PowerShell 3.0 のダウンロードとインストール

 

_**トピックの最終更新日:** 2016-12-08_

Windows Server 2012、 Windows Server 2012 R2、Windows 8、または Windows 8.1 を使用している場合は、 Windows PowerShell 3.0 が既に用意されています。これは、このアプリケーションがこれらのオペレーティング システムに組み込まれているためです。

Windows 7 または Windows Server 2008 R2 を実行している場合は、Windows PowerShell 3.0 も実行している可能性があります。ただし、これらのオペレーティング システムに元から付属しているバージョンであるバージョン 2.0 を実行している可能性もあります。使用している Windows PowerShell のバージョンを確認するには、Windows 7 または Windows Server 2008 R2 コンピューター上で次の操作を実行します。

1.  \[**スタート**\] ボタン、\[すべてのプログラム\]、\[**アクセサリ**\]、\[**Windows PowerShell**\]、\[**Windows PowerShell**\] の順にクリックします。

2.  Windows PowerShell コンソールで、次のコマンドを入力して Enter キーを押します。
    
        Get-Host | Select-Object Version

3.  コンソール ウィンドウには、次のような情報が表示されます。
    
        Version
        -------
        3.0

返されたバージョン番号が 3.0 である場合は、 Windows PowerShell 3.0 を実行しています。返されたバージョン番号が 3.0 ではない場合は、 Windows PowerShell 3.0 をインストールする必要があります。 Windows PowerShell 3.0 を含む Windows Management Framework 3.0 は、 [Microsoft Downloads Center](http://www.microsoft.com/en-us/download/details.aspx?id=34595) からダウンロードできます。

Windows PowerShell 3.0 がインストールされていることを確認した後、リモート スクリプトを実行するように Windows PowerShell が構成されていることを確認する必要があります。これを行うには、管理者として Windows PowerShell を起動します。Windows 7、Windows Server 2008 R2、Windows Server 2012、または Windows Server 2012 R2 では、次の操作を行います。

1.  \[**スタート**\] ボタン、\[**すべてのプログラム**\]、\[**アクセサリ**\]、\[**Windows PowerShell**\] の順にクリックします。\[**Windows PowerShell**\] を右クリックし、\[**管理者として実行**\] をクリックします。

2.  \[**ユーザー アカウント制御**\] ダイアログ ボックスが表示されたら、\[**はい**\] をクリックして、管理者の資格情報で Windows PowerShell を実行することを確認します。

Windows 8 を実行している場合は、代わりに次の手順を実行します。

1.  チャーム バーにアクセスし、\[**検索**\] をクリックし、\[**Windows PowerShell**\] を右クリックします。(タッチ スクリーンの有無に関係なく) Windows 8 コンピューターでチャーム バーにすばやくアクセスするには、Windows キーを押したまま C キーを押します。

2.  画面の一番下にあるツール バーで \[**管理者として実行**\] をクリックします。

3.  \[**ユーザー アカウント制御**\] ダイアログ ボックスが表示されたら、\[**はい**\] をクリックして、管理者の資格情報で Windows PowerShell を実行することを確認します。

Windows PowerShell が実行されたら、実行ポリシーを変更してリモート スクリプトの実行を許可する必要があります。 Windows PowerShell コンソールで、次のコマンドを入力して Enter キーを押します。

    Set-ExecutionPolicy RemoteSigned -Force

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>上記のコマンドを実行すると、次のエラー メッセージが表示されることがあります。<br />
Set-ExecutionPolicy: レジストリ キー 'HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Micrsoft.PowerShell' へのアクセスが拒否されました。<br />
通常、このエラー メッセージが表示されるのは、管理者の資格情報で Windows PowerShell を実行していない場合です。 Windows PowerShell のセッションを閉じ、管理者として新しいセッションを開始します。</td>
</tr>
</tbody>
</table>


実行ポリシーが正しく構成されていることを確認するには、 Windows PowerShell プロンプトで次のコマンドを入力して Enter キーを押します。

    Get-ExecutionPolicy

次の値が返された場合は、すべてが正しく構成されています。

    RemoteSigned

この時点で Windows PowerShell 3.0 を実行していない場合は、Microsoft ダウンロード センターから Windows Management Framework 3.0 をダウンロードしてインストールする必要もあります。これは、 Windows PowerShell 3.0 と Windows Remote Management (WinRM) 3.0 が含まれるインストール パッケージです。Windows 7 を実行しているが、まだ Windows PowerShell 3.0 に更新していない場合は、このインストール パッケージが必要になることがあります。Windows Server 2012、 Windows Server 2012 R2、Windows 8、または Windows 8.1 を実行している場合は、 Windows PowerShell 3.0 をインストールする必要はありません。 Windows PowerShell 3.0 はこれらのオペレーティング システムに組み込まれています。

Windows Management Framework 3.0 をインストールする前に:

  - 適切なバージョンのインストール パッケージをダウンロードしたことを確認します。64 ビット版の Windows 7 を実行している場合は、Windows6.1-KB2506143-x64.msu ファイルをダウンロードします。32 ビット版の Windows 7 を実行している場合は、Windows6.1-KB2506143-x86.msu ファイルをダウンロードします。

  - コンピューターで Windows 7 を実行している場合は、Windows 7 Service Pack 1 をインストールしたことを確認します。

実行している Windows のバージョンが不明である場合、または Windows 7 Service Pack 1 をインストールしたかどうかが不明である場合は、\[**スタート**\] ボタンをクリックし、\[**コンピューター**\] を右クリックし、\[**プロパティ**\] をクリックします。\[システム\] ダイアログ ボックスにこの情報が報告されます。

![\[システム\] ダイアログ ボックスに表示されている設定](images/Dn362783.30bff2e8-2862-4dd7-828f-43732f4b9314(OCS.15).png "[システム] ダイアログ ボックスに表示されている設定")

Windows Management Framework 3.0 をインストールするには、次の手順を実行します。

1.  .MSU インストール ファイル ( **Windows6.1-KB2506143-x64.msu** と **Windows6.1-KB2506143-x86.msu** のいずれか) をダブルクリックします。

2.  更新プログラムのダウンロードとインストール ウィザードの \[**ライセンス条項をお読みください (1/1)**\] ページで、\[**I Accept**\] (同意する) をクリックします。

3.  インストールが完了したら、\[**今すぐ再起動**\] をクリックしてコンピューターを再起動します。

コンピューターが再起動した後、 Windows PowerShell を起動でき、また管理者の資格情報でアプリケーションを実行できることを確認します。そのためには、次の操作を行います。

1.  \[**スタート**\] ボタン、\[**すべてのプログラム**\]、\[**アクセサリ**\]、\[**Windows PowerShell**\] の順にクリックします。\[**Windows PowerShell**\] を右クリックし、\[**管理者として実行**\] をクリックします。

2.  \[ユーザー アカウント制御\] ダイアログ ボックスが表示されたら、\[**はい**\] をクリックして、管理者の資格情報で Windows PowerShell を実行することを確認します。

Windows PowerShell コンソールが表示されたら、WinRM サービスが実行されていて、適切に構成されていることを確認する必要があります。サービスが実行されていることを確認するには、 Windows PowerShell プロンプトで次のコマンドを入力して Enter キーを押します。

    Get-Service winrm

WinRM サービスに関する情報が次のように画面に表示されます。

    Status   Name               DisplayName
    ------   ----               -----------
    Running  winrm              Windows Remote Management (WS-Manag...

サービスの状態が "Runing" でない場合は、次のコマンドを入力し、Enter キーを押して、WinRM サービスを開始します。

    Start-Service winrm

サービスが起動した後、次のコマンドを実行して WinRM が基本認証を使用していることを確認します。

    winrm set winrm/config/client/auth '@{Basic="True"}'

次のような情報が画面に表示されます。

    Auth
        Basic = true
        Digest = true
        Kerberos = true
        Negotiate = true
        Certificate = true
        CredSSP = false

基本認証が "true" に設定されている場合は、 Windows PowerShell を使用して Skype for Business Online に接続する準備ができています。

