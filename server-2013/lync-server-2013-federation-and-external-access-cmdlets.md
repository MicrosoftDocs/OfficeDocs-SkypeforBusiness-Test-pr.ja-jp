---
title: Lync Server 2013 でのフェデレーションおよび外部アクセスのコマンドレット
TOCTitle: Lync Server 2013 でのフェデレーションおよび外部アクセスのコマンドレット
ms:assetid: 4a384a57-257f-47a6-98d9-54cea2c647b7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg415651(v=OCS.15)
ms:contentKeyID: 48272000
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 でのフェデレーションおよび外部アクセスのコマンドレット

 

_**トピックの最終更新日:** 2016-12-08_

フェデレーションおよび外部アクセスには、2 つの重要な機能があります。フェデレーションによって組織の外部の人と通信でき、外部アクセスによって内部ネットワークの外から Microsoft Lync Server 2013 にアクセスできます。Lync Server 2013 のフェデレーションおよび外部アクセスの管理に利用可能なコマンドレットを使用すると、ユーザーが通信できる (または通信できない) 相手と、それらのユーザーが内部ネットワークにログオンしなくても Lync Server に接続できるかどうかを指定できます。

## フェデレーションおよび外部アクセスのコマンドレット

フェデレーションおよび外部アクセスに適用されるほとんどの管理タスクは、Lync Server コントロール パネルから実行できます。これらのタスクは、Lync Server 管理シェルまたはスクリプト内からコマンドレットを使用することで実行することもできます。スクリプトを使用すると、特定のタスクを自動化できます。以下は、フェデレーションおよび外部アクセスの管理に直接関連するコマンドレットの一覧です。

  - [Get-CsAllowedDomain](get-csalloweddomain.md)

  - [New-CsAllowedDomain](new-csalloweddomain.md)

  - [Remove-CsAllowedDomain](remove-csalloweddomain.md)

  - [Set-CsAllowedDomain](set-csalloweddomain.md)

  - [Get-CsBlockedDomain](get-csblockeddomain.md)

  - [New-CsBlockedDomain](new-csblockeddomain.md)

  - [Remove-CsBlockedDomain](remove-csblockeddomain.md)

  - [Set-CsBlockedDomain](set-csblockeddomain.md)

  - [Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)

  - [Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)

  - [New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)

  - [Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)

  - [Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)

  - [Get-CsFIPSConfiguration](get-csfipsconfiguration.md)

  - [New-CsFIPSConfiguration](new-csfipsconfiguration.md)

  - [Remove-CsFIPSConfiguration](remove-csfipsconfiguration.md)

  - [Set-CsFIPSConfiguration](set-csfipsconfiguration.md)

  - [Disable-CsHostingProvider](disable-cshostingprovider.md)

  - [Enable-CsHostingProvider](enable-cshostingprovider.md)

  - [Get-CsHostingProvider](get-cshostingprovider.md)

  - [New-CsHostingProvider](new-cshostingprovider.md)

  - [Remove-CsHostingProvider](remove-cshostingprovider.md)

  - [Set-CsHostingProvider](set-cshostingprovider.md)

  - [Disable-CsPublicProvider](disable-cspublicprovider.md)

  - [Enable-CsPublicProvider](enable-cspublicprovider.md)

  - [Get-CsPublicProvider](get-cspublicprovider.md)

  - [New-CsPublicProvider](new-cspublicprovider.md)

  - [Remove-CsPublicProvider](remove-cspublicprovider.md)

  - [Set-CsPublicProvider](set-cspublicprovider.md)

  - [Test-CsFederatedPartner](test-csfederatedpartner.md)

  - [Get-CsXmppAllowedPartner](get-csxmppallowedpartner.md)

  - [New-CsXmppAllowedPartner](new-csxmppallowedpartner.md)

  - [Remove-CsXmppAllowedPartner](remove-csxmppallowedpartner.md)

  - [Set-CsXmppAllowedPartner](set-csxmppallowedpartner.md)

  - [Get-CsXmppGatewayConfiguration](get-csxmppgatewayconfiguration.md)

  - [Set-CsXmppGatewayConfiguration](set-csxmppgatewayconfiguration.md)

  - [Test-CsXmppIM](test-csxmppim.md)

## 関連項目

#### その他のリソース

[Lync Server PowerShell ブログ](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x411)

