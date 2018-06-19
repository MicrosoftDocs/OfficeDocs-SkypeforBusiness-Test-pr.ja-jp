---
title: エッジ サーバーのコマンドレット
TOCTitle: エッジ サーバーのコマンドレット
ms:assetid: 1a5427f4-a0d1-4652-8135-91333158ffc8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg415635(v=OCS.15)
ms:contentKeyID: 48271421
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# エッジ サーバーのコマンドレット

 

_**トピックの最終更新日:** 2016-12-08_

エッジ サーバーを使用すると、内部ネットワークにログオンしていないユーザーに Microsoft Lync Server 2013 の機能を拡張できます。たとえば、リモート ユーザー (内部ネットワークではなくインターネット経由で Lync Server 2013 にログオンする認証済みユーザー) がいる場合は、Lync Server アクセス エッジ サービスを実行するエッジ サーバーを設定する必要があります。また、他の組織とフェデレーションを確立する場合や、Yahoo\!、AOL、MSN など、パブリック インスタント メッセージング サービスのアカウントを持つユーザーと通信するための権限をユーザーに付与する場合にも、エッジ サーバーが必要になります。


> [!IMPORTANT]
> <UL>
> <LI>
> <P>2012 年 9 月 1 日の時点で、Microsoft Lync パブリック IM 接続のユーザー サブスクリプション ライセンス ("PIC USL") を新規または更新契約において購入することができなくなりました。アクティブなライセンスをお持ちのお客様は、サービスの停止日まで Yahoo! Messenger とのフェデレーションを引き続きご利用いただけます。AOL と Yahoo! に関しては、2014 年 6 月の終了日が発表されています。詳細については、「<A href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Lync Server 2013 でのパブリック インスタント メッセンジャーの接続のサポート</A>」を参照してください。</P>
> <LI>
> <P>PIC USL は、ユーザー単位および月単位のサブスクリプション ライセンスであり、Lync Server または Office Communications Server と Yahoo! Messenger とのフェデレーションを行うにはこのライセンスが必要です。Microsoft がこのサービスを提供できるのは、Yahoo! からのサポートを条件とするものでしたが、その基盤となる契約の終了が近づいてきました。</P>
> <LI>
> <P>Lync は組織間を接続したり世界中のユーザーと接続したりするための、これまで以上の強力なツールとなります。Windows Live Messenger とのフェデレーションを行うのに、Lync Standard CAL を超えてユーザー/デバイス ライセンスを追加する必要はありません。Skype フェデレーションがこのリストに追加されることで、Lync ユーザーは IM および音声を使用して数億のユーザーにアクセスできます。</P></LI></UL>



## エッジ サーバーのコマンドレット

以下は、エッジ サーバーの管理に直接関連するコマンドレットの一覧です。

**エッジ サーバー**

  - [Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md)

  - [Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

  - [Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)

  - [New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)

  - [Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

  - [Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

  - [Test-CsAVEdgeConnectivity](test-csavedgeconnectivity.md)

  - [Set-CsEdgeServer](set-csedgeserver.md)

## 関連項目

#### その他のリソース

[Lync Server PowerShell ブログ](http://go.microsoft.com/fwlink/?linkid=203150)

