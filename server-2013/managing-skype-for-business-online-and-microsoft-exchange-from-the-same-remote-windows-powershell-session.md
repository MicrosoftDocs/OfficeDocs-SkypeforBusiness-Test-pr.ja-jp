---
title: 同じリモート Windows PowerShell セッションからの Lync Online と Microsoft Exchange の管理
TOCTitle: 同じリモート Windows PowerShell セッションからの Lync Online と Microsoft Exchange の管理
ms:assetid: 4eb4b5f0-f407-46bd-a2ac-a7ccbc387d51
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362787(v=OCS.15)
ms:contentKeyID: 56270072
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 同じリモート Windows PowerShell セッションからの Lync Online と Microsoft Exchange の管理

 

_**トピックの最終更新日:** 2015-06-22_

Office 365 を購読すると、Skype for Business Onlineだけでなく、Exchange Online にもアクセスできます。Windows PowerShell のリモート セッションを使用すると、Skype for Business Online を管理できます。また、Windows PowerShell のリモート セッションを使用して Exchange を管理することもできます。ただし、Skype for Business Online と Exchange Online では同じ URI を共有することはなく、また同じ接続方式を使用することもありません。これは、Skype for Business Online と Exchange を管理するには別のセッションを使用する必要があることを意味します。また、Windows PowerShell の 1 つのリモート セッションを使用して両方の製品を管理する何らかの方法があるかが問題になります。

実際には、Windows PowerShell の同一のインスタンスから両方の製品を管理できるだけでなく、このデュアル管理セッションを設定すると非常に簡単になります。(Credentials オブジェクトを作成してから、Skype for Business Online に接続する新しいセッションを作成する方法) で Windows PowerShellを起動し、Skype for Business Online に接続します。

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $lyncSession = New-CsOnlineSession -Credential $credential

次に、同じような手順を使用して、Exchange Online に接続します。新しい Credentials オブジェクトを作成する必要はありません。Skype for Business Online へのログオン時に使用した同じオブジェクト ($credential) を引き続き使用できます。

    $exchangeSession = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "https://outlook.office365.com/powershell-liveid/" -Credential $credential -Authentication "Basic" -AllowRedirection

Exchange Online に接続する場合には常に URI Office 365 を使用する必要があり、また Office 365 の URI に関係なくこのようにする必要があります。認証された後は、自動的に適切な URI にリダイレクトされます。このため、AllowRedirection パラメーターを含めることが特に重要になります。このパラメーターを省略すると、認証はされますが、リダイレクトが失敗し、Exchange Online には接続されません。

    New-PSSession : [ps.outlook.com] The WinRM service cannot process the request because the request needs to be sent to a different machine. Use the redirect information to send the request to a new machine.  Redirect location reported: https://pod51043psh.outlook.com/powershell-liveid?PSVersion=3.0 . To automatically connect to the redirected URI, verify  MaximumConnectionRedirectionCount" property of session preference variable "PSSessionOption" and use "AllowRedirection" parameter on the cmdlet.

この時点で、コンピューター上で 2 つの独立したリモート セッションが実行されている必要があります。これを確認するには、Windows PowerShell プロンプトで次のコマンドを入力します。

    Get-PSSession

次のような情報が画面に表示されます。

    Id Name      ComputerName  State   ConfigurationName     Availability
    -- ----      ------------  -----   -----------------     ------------
     1 Session1  pod510w43...  Opened  Microsoft.PowerShell     Available
     2 Session2  up02921vd...  Opened  Microsoft.Exchange       Available

この時点で、Windows PowerShell のローカル セッションにインポートできるリモート セッションのペアを入手できます。入手するには、次の 2 つのコマンドを実行します。

    Import-PSSession $lyncSession
    Import-PSSession $exchangeSession

この時点で、Skype for Business Online コマンドレットと Exchange Online コマンドレットの両方が使用できるようになります。このことを確認するには、次のコマンドを実行し、ユーザー情報を取得したことを確認します。

    Get-CsOnlineUser -ResultSize 1

続いて、次の Exchange のコマンドを実行し、メールボックス情報を取得したことを確認します。

    Get-Mailbox -ResultSize 1

管理セッションを終了する場合は、必ず両方のリモート セッションを閉じます。

    Remove-PSSession $lyncSession
    Remove-PSSession $exchangeSession

## 関連項目

#### 概念

[Lync Online 管理用のコンピューターの構成](configuring-your-computer-for-skype-for-business-online-management.md)

