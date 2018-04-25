---
title: アドレス帳サーバーのコマンドレット
TOCTitle: アドレス帳サーバーのコマンドレット
ms:assetid: 33da45da-3c57-4d04-9679-f0e5a0cfd37e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg415643(v=OCS.15)
ms:contentKeyID: 48271727
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# アドレス帳サーバーのコマンドレット

 

_**トピックの最終更新日:** 2016-12-08_

アドレス帳サーバーは、Active Directory ドメイン サービスと Microsoft Lync Server 2013 の間の仲介役です。アドレス帳サーバーは、Lync Server 2013 に格納されているユーザー情報と Active Directory に格納されているユーザー情報が、確実に同期するようにします。これは、ユーザー データベース内に格納されているアドレス帳ファイルを定期的に同期することで実行されます。また、Lync Server にはアドレス帳サーバーを管理するための多くのコマンドレットが含まれます。

## アドレス帳サーバーのコマンドレット

Lync Server コントロール パネルでアドレス帳サーバーの設定を構成することはできません。そのような設定を管理するための主要なツールは Windows PowerShell です。以下は、アドレス帳サーバーの管理に直接関連するコマンドレットの一覧です。

**アドレス帳サーバー**

  -   
    [Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)

  -   
    [New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)

  -   
    [Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

  -   
    [Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

<!-- end list -->

  -   
    [Update-CsAddressBook](update-csaddressbook.md)

  -   
    [Debug-CsAddressBookReplication](debug-csaddressbookreplication.md)

<!-- end list -->

  -   
    [Test-CsAddressBookService](test-csaddressbookservice.md)

  -   
    [Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

## 関連項目

#### その他のリソース

[Lync Server PowerShell ブログ](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x411)

