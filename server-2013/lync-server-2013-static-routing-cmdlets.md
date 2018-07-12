---
title: 静的ルーティングのコマンドレット
TOCTitle: 静的ルーティングのコマンドレット
ms:assetid: 71d5e0cd-8412-4383-818a-95b851a4da4b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg416492(v=OCS.15)
ms:contentKeyID: 48272445
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 静的ルーティングのコマンドレット

 

_**トピックの最終更新日:** 2016-12-08_

管理者は静的ルートを使用して、SIP メッセージが経由するネットワーク ルートをあらかじめ設定できます。サーバーはメッセージを受信すると、そのメッセージのアドレスを確認し、管理者があらかじめ設定した次ホップ サーバーに転送します。正しく構成されている場合、静的ルートによって、メッセージを適切なタイミングで正確に配信でき、サーバーにかかるオーバーヘッドが最小限になります。

## 静的ルーティングのコマンドレット

Microsoft サポート担当者に指示されない限り、Microsoft Lync Server 2013 用に構成する静的ルートは [New-CsStaticRoute](new-csstaticroute.md) コマンドレットを使用して作成する必要があります。ルートの作成後に、CsStaticRoutingConfiguration コマンドレットを使用して、ルートを静的ルーティング コレクションに追加できます。

**静的ルーティング**

  - [Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)

  - [New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)

  - [Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)

  - [Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

  - [New-CsStaticRoute](new-csstaticroute.md)

  - [Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)

  - [New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)

  - [Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)

  - [Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

  - [New-CsSipProxyCustom](new-cssipproxycustom.md)

  - [New-CsSipProxyRealm](new-cssipproxyrealm.md)

  - [New-CsSipProxyTCP](new-cssipproxytcp.md)

  - [New-CsSipProxyTLS](new-cssipproxytls.md)

  - [New-CsSipProxyTransport](new-cssipproxytransport.md)

  - [New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

  - [New-CsSipProxyUseDefaultCert](new-cssipproxyusedefaultcert.md)

  - [New-CsIssuedCertId](new-csissuedcertid.md)

## 関連項目

#### その他のリソース

[Lync Server PowerShell ブログ](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x411)

