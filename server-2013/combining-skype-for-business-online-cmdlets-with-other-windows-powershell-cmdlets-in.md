---
title: Lync Online コマンドレットとその他の Windows PowerShell コマンドレットとの組み合わせ
TOCTitle: Lync Online コマンドレットとその他の Windows PowerShell コマンドレットとの組み合わせ
ms:assetid: 8bb8800a-f966-4570-8c8b-db87a91ad783
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362816(v=OCS.15)
ms:contentKeyID: 56270109
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Online コマンドレットとその他の Windows PowerShell コマンドレットとの組み合わせ

 

_**トピックの最終更新日:** 2015-06-22_

Windows PowerShell を使用して Skype for Business Online に接続している場合、約 40 個の Skype for Business Online コマンドレットを使用できます。ただし、Skype for Business Online の管理には、この 40 個以外のコマンドレットも使用できます。Skype for Business Online コマンドレットのほか、コンピューターにインストールされているその他の Windows PowerShell コマンドレットも使用できます (Windows PowerShell 3.0 をインストールしている場合は、数百個の Windows PowerShell コア コマンドレットもインストールされます)。Skype for Business Online コマンドレットとコンピューターで使用できるその他のコマンドレットを組み合わせて、コマンドを作成できます。

Windows PowerShell 3.0 についてはここで詳しく説明しませんが、コマンドレットを組み合わせる理由について、いくつかの例を示します。まず、Skype for Business Online コマンドレットには Print コマンドが含まれません。また、そのようなコマンドは Windows PowerShell コンソールにもありません。では、コマンドレットで取得した情報はどうやって印刷するのでしょうか。1 つは情報を取得し、その情報を **Out-Printer** コマンドレットに送るという方法です。

    Get-CsTenant | Out-Printer

追加パラメーターは含まれないため、**the Out-Printer** コマンドレットによって返される情報はすべて既定のプリンターで印刷されます。

同様に、Skype for Business Online コマンドレットにはデータをファイルに保存できるパラメーターも含まれません。でも問題はありません。このコマンドでは **Out-File** コマンドレットを使用して、返された情報をテキスト ファイル C:\\Logs\\Tenants.txt に保存します。

    Get-Tenant | Out-File -FilePath "C:\Logs\Tenants.txt"

またこのコマンドでは、**Select-Object** コマンドレットを使用して返されるデータを制限し、画面に表示します。この例では、[Get-CsOnlineUser](get-csonlineuser.md) コマンドレットですべての Skype for Business Online ユーザーの情報を取得し、**Select-Object** コマンドレットを使用して、表示データをユーザーの ID 値とアーカイブ ポリシーに限定しています。

    Get-CsOnlineUser | Select-Object Identity, ArchivingPolicy

コンピューターでは数百個のコマンドレットを使用できるため、Skype for Business Online コマンドレットとそれ以外のコマンドレットを区別するのは難しいかもしれません。Skype for Business Online コマンドレット (および Skype for Business Online コマンドレットのみ) のリストを返すには、まずすべての Skype for Business Online コマンドレットを含む一時的な Windows PowerShell モジュールの名前を特定する必要があります。この操作を実行するには、Windows PowerShell プロンプトから次のコマンドを実行します。

    Get-Module

次のような情報が画面に表示されます。

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

ModuleType スクリプトを含むモジュールは、Skype for Business Online コマンドレットを含むモジュールです。これらのコマンドレットのリストを返すには、モジュール名と同じ Script モジュール名を使用して **Get-Command** コマンドレットを実行します。

    Get-Command -Module tmp_5astd3uh.m5v

ModuleType = Script の複数のモジュールがある場合があります。この場合は次のコマンドを実行して、**Get-CsTenant** コマンドレットが含まれるモジュールを検索できます。

    Get-Command Get-CsTenant

**Get-CsTenant** コマンドレットで返されるモジュールには、すべての Skype for Business Online コマンドレットが含まれます。

    CommandType     Name                                               ModuleName
    -----------     ----                                               ----------
    Function        Get-CsTenant                                       tmp_5astd3uh.m5v

## 関連項目

#### 概念

[Windows PowerShell と Lync Online の概要](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

