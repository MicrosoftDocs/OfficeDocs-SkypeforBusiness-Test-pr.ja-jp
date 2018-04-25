---
title: ユーザー ID を使用するコマンドレット
TOCTitle: ユーザー ID を使用するコマンドレット
ms:assetid: be87409f-6372-4c70-91ac-6ef13dfbe65a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362842(v=OCS.15)
ms:contentKeyID: 56270141
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ユーザー ID を使用するコマンドレット

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online では、個々のユーザー ID を参照するためのさまざまな方法があります。

  - ユーザーの Active Directory ドメイン サービスの表示名を使用する。例:
    
        -Identity "Ken Myer"

  - ユーザーの SIP アドレスを使用する。例:
    
        -Identity "sip:kenmyer@litwareinc.com"

  - ユーザーの UPN を使用する。例:
    
        -Identity " kenmyer@litwareinc.com"

  - ユーザーの Active Directory ドメイン サービスの識別名を使用する。例:
    
        -Identity "CN=48ebd1ba-95d4-460c-b751-811ebf0c4611,OU=fa8226f5-14fa-46da-8 236-039b25bc7a27,OU=Lync Online Tenants,DC=litwareinc,DC=com"

次のコマンドレットでは、ユーザー ID を使用できます。

  - [Disable-CsMeetingRoom](disable-csmeetingroom.md)

  - [Enable-CsMeetingRoom](enable-csmeetingroom.md)

  - [Get-CsExUmContact](get-csexumcontact.md)

  - [Get-CsMeetingRoom](get-csmeetingroom.md)

  - [Get-CsOnlineUser](get-csonlineuser.md)

  - [Get-CsUserAcp](get-csuseracp.md)

  - [New-CsExUmContact](new-csexumcontact.md)

  - [Remove-CsExUmContact](remove-csexumcontact.md)

  - [Remove-CsUserAcp](remove-csuseracp.md)

  - [Set-CsExUmContact](set-csexumcontact.md)

  - [Set-CsMeetingRoom](set-csmeetingroom.md)

  - [Set-CsUserAcp](set-csuseracp.md)

次のいずれかの **Get-Cs** コマンドレットを呼び出す場合は、ユーザー ID を指定する必要はありません。この場合、コマンドレットによって指定した項目のすべてのインスタンスが返されます。たとえば、次のコマンドを実行すると Skype for Business Online が有効なすべてのユーザーに関する情報が返されます。

    Get-CsOnlineUser

特定のユーザーの情報を返したい場合にのみ、Identity パラメーターが必要です。

    Get-CsOnlineUser -Identity "Ken Myer"

## 関連項目

#### 概念

[ID、スコープ、およびテナント](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online のコマンドレット](the-skype-for-business-online-cmdlets.md)

