---
title: ハイブリッド展開での Windows PowerShell の使用
TOCTitle: ハイブリッド展開での Windows PowerShell の使用
ms:assetid: b19625d4-4b68-403c-a072-5296aa590556
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362835(v=OCS.15)
ms:contentKeyID: 56270132
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ハイブリッド展開での Windows PowerShell の使用

 

_**トピックの最終更新日:** 2015-06-22_

ハイブリッド展開では、組織の一部のユーザーが Lync Server 2013 の社内版に、その他のユーザーが Skype for Business Online に所属します。Windows PowerShell の 1 つのセッションを使用して、Lync Server の社内版と自分の Skype for Business Online テナントの両方を同時に管理できます。このためには、次の 2 つの重要な点を理解する必要があります。

1.  Lync Server と Skype for Business Online に同時接続する方法。

2.  同時接続から Skype for Business Online の設定を参照する方法。

Lync Server と Skype for Business Online に同時接続するのはとても簡単です。まず通常どおりの方法、つまり Lync Server 管理シェル を起動するか、フロント エンド プールへのリモート接続を作成して、Lync Server に接続します。Lync Server の社内版に接続できたら、Skype for Business Online のみに接続する場合と同じ手順で Skype for Business Online に接続できます。この接続を行うには、まず Office 365 のログオン情報を使用して Windows PowerShell の資格情報オブジェクトを作成する必要があります。この操作を行うには、Windows PowerShell プロンプトで次のように入力して Enter キーを押します。

    $credential = Get-Credential

Enter キーを押すと、\[**Windows PowerShell 資格情報**\] ダイアログ ボックスが表示されます

![Windows PowerShell ログイン資格情報](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Windows PowerShell ログイン資格情報")

\[**ユーザー名**\] ボックスに Skype for Business Online の名前を入力します。\[**パスワード**\] ボックスに Skype for Business Online のパスワードを入力します (パスワードはマスク表示され、画面で見ることはできません)。たとえば、ユーザー名が jun@example.com でパスワードが p@ssw0rd\! の場合、ダイアログ ボックスは次のようになります。

![Windows PowerShell 資格情報ログイン](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Windows PowerShell 資格情報ログイン")

資格情報オブジェクトを作成するには、\[**OK**\] をクリックします。資格情報オブジェクトを作成したら、次のコマンドを実行して Skype for Business Online に接続できます。

    $session = New-CsOnlineSession -Credential $credential

表示されているとおりに正しくコマンドを入力してください。Skype for Business Online ドメインの名前は関係ありません。**New-CsOnlineSession** コマンドレットによって Office 365 に接続され、入力した資格情報でログオンされます。接続して認証されたら、適切な URI に自動的にリダイレクトされます。

接続に成功すると、Windows PowerShell のコンソールに次のようなメッセージが表示されます。

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

Skype for Business Online との接続を正常に確立したら、次のようなコマンドを実行してそのセッションをインポートします。

    Import-PSSession $session -AllowClobber

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>AllowClobber パラメーターを使用すると、通常の Lync Server コマンドレットと同じ名前を持つコマンドレットを含む、すべての Skype for Business Online コマンドレットがインポートされます。このようなコマンドレットは多数あります。ほとんどの Skype for Business Online コマンドレット (<a href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</a>、<a href="new-csexumcontact.md">New-CsExUmContact</a>、<a href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</a> など) は社内版と同等であるためです。ペアのコマンドレット (Lync Server<strong>Get-CsMeetingConfiguration</strong> コマンドレットと Skype for Business Online<strong>Get-CsMeetingConfiguration</strong> コマンドレットなど) は同じで、使用するコマンドレットは関係ありません。AllowClobber パラメーターを使用する唯一の理由は、警告メッセージが画面に表示されないようにするためです。</td>
</tr>
</tbody>
</table>


この時点で、Lync Server の社内版と Skype for Business Online の管理を開始できる準備ができています。この際、重要な疑問が生まれるかもしれません。Lync Server と Skype for Business Online の間のポリシーと設定を区別する方法です。たとえば、グローバル会議の構成設定を変更するため、次のコマンドを実行するとします。

    Set-CsMeetingConfiguration -Identity "global" -AdmitAnonymousUsersByDefault $False

このコマンドによってグローバル設定は変更されますが、どちらのグローバル設定でしょうか? Lync Server 社内版、Skype for Business Online、その両方のうちどれが変更されるでしょうか? またはいずれも変更されないのでしょうか?

この特定の場合は、社内版の設定が変更されます。これがわかるのは、コマンドに Tenant パラメーターが含まれていないためです。Lync Server 社内版と Skype for Business Online に同時に接続している場合、いずれかのプラットフォームに対して機能するコマンドレットは、特に指定しない限り Lync Server に対して実行されます。この指定を行う唯一の方法は、コマンドの実行時に Tenant パラメーターを含めることです。たとえば次のコマンドでは、テナント ID が bf19b7db-6960-41e5-a139-2aa373474354 の Skype for Business Online テナントのグローバル設定が更新されます。

    Set-CsMeetingConfiguration -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AdmitAnonymousUsersByDefault $False

Tenant パラメーターは重要です。このコマンドによって、Lync Server 社内版のグローバル外部アクセス ポリシーが返されます。

    Get-CsExternalAccessPolicy -Identity "global"

またこのコマンドによって、Skype for Business Online テナントのグローバル外部アクセス ポリシーが返されます。

    Get-CsExternalAccessPolicy -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

700 個を優に超える社内用コマンドレットがあります。ただし、この大部分には Tenant パラメーターが含まれません。つまり、これらのコマンドレットは Skype for Business Online で使用できないということです。また、Tenant パラメーターを使用するコマンドレットはいくつかありますが、Skype for Business Online ではまだ使用できないという点にも注意してください。Skype for Business Online で使用できる一連のコマンドレットを正しく取得するには、Windows PowerShell プロンプトから次のコマンドを実行します。

    Get-Module

次のような情報が表示されます。

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

ModuleType Script が含まれるモジュールには、Skype for Business Online コマンドレットが含まれます。これらのコマンドレットのリストを返すには、モジュール名として Script モジュールの名前を使用して、**Get-Command** コマンドレットを実行します。

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell にすべての Skype for Business Online コマンドレットの一覧が表示されます。

**ハイブリッド展開での接続に関するトラブルシューティング**

管理者が Office 365 アカウント (administrator@litwareinc.net) ではなく社内アカウント (administrator@litwareinc.onmicrosoft.com) を使用しているとき、場合によっては Office 365 にログオンできないことがあります。本来、ディレクトリ同期が正常に機能していれば、どちらのアカウントを使用してもログオンできるはずです (それがハイブリッド展開の 1 つの利点です)。しかし、管理者が社内アカウントを使用してログオンできないケースが実際に起こっています。これは通常、自動検索によって、ログオン処理が Office 365 ではなく、社内にインストールされた Lync Server に向けられることが原因です。

この問題は簡単な方法で回避できます。**New-CsOnlineSession** コマンドレットを使用して Office 365 にログオンするときに、OverrideAdminDomain パラメーターとそれに続いて Office 365 ドメイン名を指定します。たとえば、アカウント administrator@litwareinc.net を使用して Office 365 にログオンするには、OverrideAdminDomain パラメーターの後にドメイン名 litwareinc.onmicrosoft.com を指定します。

    $session = New-CsOnlineSession -Credential $credential -OverrideAdminDomain "litwareinc.onmicrosoft.com"

このコマンドにより、ログオン処理が Office 365 サーバーと litwareinc.onmicrosoft.com domain に対して明示的に実行されます。

