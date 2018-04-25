---
title: Windows PowerShell を使用した Lync Online への接続
TOCTitle: Windows PowerShell を使用した Lync Online への接続
ms:assetid: 6167dad9-9628-4fdb-bed1-bdb3f7108e64
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362795(v=OCS.15)
ms:contentKeyID: 56270081
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows PowerShell を使用した Lync Online への接続

 

_**トピックの最終更新日:** 2017-03-03_

必要なソフトウェアをインストールすれば、Windows PowerShell を使用して Skype for Business Online を管理する作業を開始する準備が完了します。このためには、まず Windows PowerShell の標準インスタンスを開きます。(たとえば Lync Server 管理シェル のような) Windows PowerShell の特別なインスタンスを開く必要はなく、またコントロール パネル アプリやその他の特別な種類のアプリケーションを開く必要もありません。これは、Windows PowerShell のリモート セッションを使用して Skype for Business Online の管理を行うためです。これは、次のことを意味します。

1.  Windows PowerShell の通常のセッションを使用して Skype for Business Online に接続します。リモートで接続する場合は、ローカル コンピューター上で作業し、Windows PowerShell のローカル コピーを使用しますが、リモート システム上にあるオブジェクト (つまり Skype for Business Online) を管理します。

2.  Skype for Business Online の管理に必要なすべてのコマンドレット、スクリプト、およびその他のアイテムがコンピューターにダウンロードされます。これらのアイテムはメモリ内に保持され、Skype for Business Online との間で確立されたリモート セッションのみで使用できます。この点は重要であるため注意する必要があります。Skype for Business Online へのリモート接続を行うと、[Get-CsTenant](get-cstenant.md) などの Skype for Business Online のコマンドレットがコンピューターのメモリ内にコピーされます。リモート セッションでは、これらのコマンドレットを実行できます。ただし、これらのコマンドレットはそのリモート セッションのみで使用できます。たとえば、Windows PowerShell の 2 つ目のセッションを開始するが、このセッションで Skype for Business Online には接続しない場合があります。そのセッションから **Get-CsTenant** コマンドレットを実行しようとすると、次のエラー メッセージが表示されます。
    
        Get-CsTenant : The term 'Get-CsTenant' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
    
    また、ハード ディスクで **Get-CsTenant** コマンドレット (または他の Skype for Business Online のコマンドレット) を検索しても、見つかりません。これは、リモート セッションを作成したときに、実際にはハード ディスクに何も保存されないためです。

3.  リモート セッションを閉じると、ダウンロードしたアイテムはコンピューターのメモリから削除されます。たとえば、**Get-CsTenant** コマンドレットを使用して Windows PowerShell のリモート セッションを開始してから、そのセッションを閉じた場合、Windows PowerShell を再起動すると、**Get-CsTenant** コマンドレットは使用できなくなっています。**Get-CsTenant** コマンドレットにアクセスするには、Skype for Business Online に再接続する必要があります。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ハイブリッド展開を使用している場合は、「<a href="using-windows-powershell-in-a-hybrid-deployment-with-skype-for-business-online.md">ハイブリッド展開での Windows PowerShell の使用</a>」の記事に示されている手順を実行する必要があります。</td>
</tr>
</tbody>
</table>


Skype for Business Online へのリモート接続を作成するには、まずローカル コンピューター上で Windows PowerShell の新しいセッションを開始します。Windows 7、Windows Server 2008 R2、Windows Server 2012、または Windows Server 2012 R2 を実行している場合は、次の操作を実行します。

  - \[**スタート**\] ボタン、\[**すべてのプログラム**\]、\[**アクセサリ**\]、\[**Windows PowerShell**\]、\[**Windows PowerShell**\] の順にクリックします。

Windows 8 または 8.1 を実行している場合は、代わりに次の手順を実行します。

  - チャーム バーにアクセスし、\[**検索**\] をクリックし、\[**Windows PowerShell**\] をクリックします。(タッチ スクリーンの有無に関係なく) Windows 8 または 8.1 コンピューターでチャーム バーにすばやくアクセスするには、Windows キーを押しながら C キーを押します。

Windows PowerShell コンソールが表示された後、Windows PowerShell の資格情報オブジェクトを作成する必要があります。資格情報オブジェクトは、ユーザー名とパスワードを安全な方法で Skype for Business Online に伝達するために使用されます。資格情報オブジェクトを作成するには、Windows PowerShell プロンプトで次のコマンドを入力して、Enter キーを押します。

    $credential = Get-Credential

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>この例では、ユーザー名とパスワードは変数 $credential に格納されます。Windows PowerShell の変数名の規則に準拠している限り、この変数に任意の名前を付けることができます。ただし、ユーザー名とパスワードを格納するために、ある種の変数を使用する必要があります。このようにしないと、作成した資格情報オブジェクトは、作成後にすぐ消滅します。</td>
</tr>
</tbody>
</table>


Enter キーを押すと、\[**Windows PowerShell 資格情報の要求**\] ダイアログ ボックスが表示されます。

![Windows PowerShell ログイン資格情報](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Windows PowerShell ログイン資格情報")

\[**ユーザー名**\] ボックスに Skype for Business Online のユーザー名を入力します。\[**パスワード**\] ボックスに Skype for Business Online のパスワードを入力します (パスワードはマスクされ、画面には表示されません)。たとえば、ユーザー名が kenmyer@litwareinc.com で、パスワードが p@ssw0rd\! である場合、ダイアログ ボックスは次のようになります。

![Windows PowerShell 資格情報ログイン](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Windows PowerShell 資格情報ログイン")

資格情報オブジェクトを作成するには、\[**OK** \] をクリックします。オブジェクトが作成されたことを確認するには、単に Windows PowerShell プロンプトで変数名を入力して Enter キーを押します。

    $credential

Windows PowerShell は、次のような表示で応答します。

    UserName                            Password
    --------                            --------
    kenmyer@litwareinc.com              System.Security.SecureString

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Get-Credential</strong> コマンドレットは、ユーザーが入力したすべての資格情報を受け入れ、有効なユーザー名とパスワードを入力したかを確認しないことにご注意ください。ユーザーが Skype for Business Online にログオンしようとするときのみ、この検証が行われます。</td>
</tr>
</tbody>
</table>


資格情報オブジェクトを作成した後、Skype for Business Online への接続を行う新しいリモート Windows PowerShell セッションを作成できます。これを行うには、Windows PowerShell プロンプトで次のコマンドを入力して、Enter キーを押します。

    $session = New-CsOnlineSession -Credential $credential

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>$session は情報を保持するために使用される変数です。この場合は、Skype for Business Online への接続に関する情報です。この場合も、名前が Windows PowerShell の変数名のガイドラインを満たす限り、この変数に任意の名前を付けることができます (たとえば、名前に空白や句読点を含めることはできません)。</td>
</tr>
</tbody>
</table>


必ず、表示どおり正確にコマンドを入力します (変数名の例外が存在する可能性があります)。Skype for Business Online ドメインがどのような名前であるかは問題にならないことにご注意ください。ドメイン名に関係なく、指定された資格情報を使用して **New-CsOnlineSession** コマンドレットによりユーザーは Office 365 に接続し、ログオンします。ユーザーが接続を行い、認証された後、指定された資格情報に基づいてユーザーは自動的に適切な URI にリダイレクトされます。

接続が成功した場合、Windows PowerShell コンソールには次のようなメッセージが表示されます。

    VERBOSE: Determining domain to admin
    VERBOSE: AdminDomain = litwareinc.com
    VERBOSE: Discovering PowerShell endpoint URI
    VERBOSE: TargetUri = https://webdir0d.litwareinc.com/OcsPowerShellLiveId
    VERBOSE: Requesting authentication token
    VERBOSE: Success
    VERBOSE: Initializing remote session
    VERBOSE: Success
    Id Name       ComputerName    State        ConfigurationName     Availability -- ----       ------------    -----        -----------------     ------------
    2 Session2    litwarein...    Opened       Microsoft.PowerShell  Available

ただし、これで Windows PowerShell を使用して Skype for Business Online を管理する作業を開始する準備ができたわけではありません。**New-CsOnlineSession** コマンドレットは Skype for Business Online に接続し、ユーザー用の新しいセッションを作成しました。ただし、ユーザーはその新しいセッションを Windows PowerShell コンソールにインポートする必要があります。これを行うには、次のコマンドを実行します。

    Import-PSSession $session

Enter キーを押すと、Windows PowerShell コンソールに次のようなインジケーターが表示されます。

    Creating implicit remoting module . . .
         Getting command information from remote session . . . 16 commands  
              received
         [oooooooooooooooo
         00:00:33 remaining

この時点では、Windows PowerShell は、Skype for Business Online の管理に必要なコマンドレットなどのアイテムをダウンロードしています。ダウンロードが完了した時点で、Windows PowerShell コンソールには次のような情報が表示されます。

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enable-Cs ...}

この時点で、Windows PowerShell を使用して Skype for Business Online を管理する作業を開始する準備ができました。ダウンロードが成功したことを確認し、使用できる Skype for Business Online のコマンドレットを表示するには、まず、すべての Skype for Business Online のコマンドレットが含まれる一時 Windows PowerShell モジュールの名前を確認する必要があります。これを行うには、Windows PowerShell プロンプトから次のコマンドを実行します。

    Get-Module

次のような情報が画面に表示されます。

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

ModuleType Script が含まれるモジュールは、Skype for Business Online のコマンドレットが含まれるモジュールです。これらのコマンドレットの一覧を返すには、モジュール名として Script モジュールの名前を使用して **Get-Command** コマンドレットを実行します。

    Get-Command -Module tmp_5astd3uh.m5v

これで、Windows PowerShell では Skype for Business Online のすべてのコマンドレットの一覧が表示されます。

管理タスクが完了した後は、Windows PowerShell コンソールを閉じる前に、必ず次のコマンドを実行する必要があります。

    Remove-PSSession $session

**Remove-PSSession** コマンドレットにより、ユーザーは Skype for Business Online から切断され、リモート セッションが閉じられます。実際、(**Import-PSSession** コマンドレットを実行して) セッションを再インポートしようとすると、次のエラー メッセージが表示されます。

    Import-PSSession : State of runspace is not valid for this operation.

このメッセージは、単に、Skype for Business Online に再接続するには新しいセッションを作成する必要があることを意味します。

Windows PowerShell コンソールを閉じる前にセッションを削除することを忘れた場合 (またはコンソールが予期せず終了した場合)、不都合なことは何も起こりません。アクティブでない状態が 15 分経過すると、セッションは自動的に切断されます。ただし、既定では、Skype for Business Online の各管理者に許可される Skype for Business Online への同時接続は 3 つに限定されます。セッションを削除せずに Windows PowerShell コンソールを閉じた場合、その閉じられたセッションは、その時点で使用されていない場合であっても 1 つの接続としてカウントされます (また、タイムアウトになるまで引き続き 1 つの接続としてカウントされます)。たとえば、毎回 Skype for Business Online セッションを削除することなく Windows PowerShell コンソールを 3 回開いて閉じた場合、Windows PowerShell を開いて 4 つ目の接続を行おうとすると、コマンドはハングし、接続は行われません。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>接続しようとしているときに Windows PowerShell がハングした場合は、Ctrl + C キーを押して、停止状態のコマンドを終了します。</td>
</tr>
</tbody>
</table>


個々の管理者は Skype for Business Online テナントへの同時接続を 3 つだけ使用できますが、組織では最大 9 つの同時接続を使用できます。これは、Skype for Business Online に対して、3 人の管理者がそれぞれ 3 つの同時接続を使用したり、9 人の管理者が 1 つの接続を使用したりできる、といったことを意味します。ただし、繰り返しになりますが、1 人の管理者が 4 つ以上のアクティブなセッションを使用することはできません。

## 関連項目

#### 概念

[Lync Online 管理用のコンピューターの構成](configuring-your-computer-for-skype-for-business-online-management.md)

