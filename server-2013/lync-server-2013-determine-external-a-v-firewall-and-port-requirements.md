﻿---
title: 'Lync Server 2013: 外部の音声ビデオ ファイアウォールおよびポートの要件を決定する'
TOCTitle: 外部の音声ビデオ ファイアウォールおよびポートの要件を決定する
ms:assetid: 3b849dc7-175d-40d1-820d-80e6ade6d332
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425882(v=OCS.15)
ms:contentKeyID: 48271819
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 の外部の音声ビデオ ファイアウォールおよびポートの要件を決定する

 

_**トピックの最終更新日:** 2015-03-09_

音声ビデオ (A/V) 通信は複雑になります。音声ビデオで使用されるプロトコルの性質と、クライアントおよびサーバーによるプロトコルの使用方法により、クライアント バージョンとサーバー バージョンの違いを説明する特別なセクションが必要です。

次の音声ビデオ ファイアウォールとポートの表を使用して、ファイアウォールの要件と開く必要のあるポートを確認します。次に、ネットワーク アドレス変換 (NAT) 用語を確認します。これは、NAT が多くの異なる方法で実装される可能性があるためです。ファイアウォールのポート設定例の詳細については、「[Lync Server 2013 の外部ユーザー アクセスのシナリオ](lync-server-2013-scenarios-for-external-user-access.md)」の参照アーキテクチャを参照してください。

### 音声ビデオおよびメディア トラフィックにおける UDP と TCP プロトコルの一般的な使用法

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>音声ビデオ トランスポート</th>
<th>使用量</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UDP</p></td>
<td><p>音声とビデオの優先トランスポート層プロトコル</p></td>
</tr>
<tr class="even">
<td><p>TCP</p></td>
<td><p>音声とビデオの代替トランスポート層プロトコル</p>
<p>Office Communications Server 2007 R2、Lync Server 2010、および Lync Server 2013 に対するアプリケーション共有の必須トランスポート層プロトコル</p>
<p>Lync Server 2010 および Lync Server 2013 に対するファイル転送の必須トランスポート層プロトコル</p></td>
</tr>
</tbody>
</table>


## 外部ユーザー アクセス用の外部の音声ビデオ ファイアウォール ポートの要件

外部 (および内部) SIP と会議のインターフェイスのファイアウォール ポートの要件は、クライアントのバージョンまたはフェデレーション パートナーのバージョンに関係なく一貫しています。

音声ビデオ エッジの外部インターフェイスの場合は、そうではありません。Office Communications Server 2007 とのフェデレーションの場合、音声ビデオ エッジ サービスでは、外部ファイアウォール ルールによって、50,000 ～ 59,999 のポート範囲で RTP/TCP および RTP/UDP トラフィックが双方向に通過できる必要があります。上の表は、Lync Server 2013 が主なフェデレーション パートナーであり、表示されている他の種類のフェデレーション パートナーのうちのいずれかと通信できるように構成されていることを前提とします。

音声ビデオのポート範囲を 50,000 ～ 59,999 に構成する場合は、そのポート範囲に、フェデレーション パートナーへの通信の発信元ポートが含まれることを考慮する必要があります。つまり、フェデレーション パートナーから通信が開始されることを考慮します。50,000 ～ 59,999 の範囲内にある 音声ビデオ エッジ サービス ポートからの通信は、パートナーの 音声ビデオ エッジ サービスで想定されるポート TCP 443 に接続します。逆に、音声ビデオ エッジ サービス ポート TCP 443 への受信トラフィックの発信元ポートの範囲は 50,000 ～ 59,999 になります。

宛先ルールのみを構成すればよいか、宛先と発信元の両方を構成する必要があるかは、ファイアウォールやファイアウォールを管理するポリシーに応じて異なります。要件が宛先ポートのみを対象としている場合、音声ビデオの要件は次のとおりです。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>発信元 IP アドレス</th>
<th>送信先 IP アドレス</th>
<th>宛先ポート</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>音声ビデオ エッジ サービス インターフェイス</p></td>
<td><p>任意</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>音声ビデオ エッジ サービス インターフェイス</p></td>
<td><p>任意</p></td>
<td><p>UDP 3478</p></td>
</tr>
<tr class="odd">
<td><p>任意</p></td>
<td><p>音声ビデオ エッジ サービス インターフェイス</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>任意</p></td>
<td><p>音声ビデオ エッジ サービス インターフェイス</p></td>
<td><p>UDP 3478</p></td>
</tr>
</tbody>
</table>


受信ファイアウォールと送信ファイアウォールの両方のルール定義がポリシーに必要な場合、音声ビデオの要件は次のとおりです。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>発信元 IP アドレス</th>
<th>送信先 IP アドレス</th>
<th>送信元ポート</th>
<th>宛先ポート</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>音声ビデオ エッジ サービス インターフェイス</p></td>
<td><p>任意</p></td>
<td><p>TCP 50,000 ～ 59,999</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>音声ビデオ エッジ サービス インターフェイス</p></td>
<td><p>任意</p></td>
<td><p>UDP 3478</p></td>
<td><p>UDP 3478</p></td>
</tr>
<tr class="odd">
<td><p>任意</p></td>
<td><p>音声ビデオ エッジ サービス インターフェイス</p></td>
<td><p>任意</p></td>
<td><p>TCP 443</p></td>
</tr>
<tr class="even">
<td><p>任意</p></td>
<td><p>音声ビデオ エッジ サービス インターフェイス</p></td>
<td><p>任意</p></td>
<td><p>UDP 3478</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> Microsoft Office Communications Server 2007 については、必要な構成が若干異なります。この場合、50,000 ～ 59,999 の TCP と UDP のポート範囲はオープン インバウンドとオープン アウトバウンドである必要があります。この要件は、Office Communicator 2007 にのみ適用されます。Office Communications Server 2007 R2、Lync Server 2010、および Lync Server 2013 の場合、必要なのは TCP 範囲 50,000 ～ 59,999 のオープン アウトバウンドだけです。



## 外部ユーザー アクセス用の NAT 要件

通常、NAT はルーティング機能ですが、ファイアウォールなどの新しいデバイスや、ハードウェア ロード バランサーでも NAT を構成できます。ここでは、NAT を実行するデバイスについてではなく、必要な NAT 動作について説明します。

Lync Server 2013  通信ソフトウェアは、エッジの内部インターフェイスではなく、エッジの外部インターフェイスとの送受信トラフィックで NAT をサポートします。次の NAT 動作が必要です。


> [!IMPORTANT]
> 受信と送信のトラフィックについて、対称 NAT を構成する必要があります。対称 NAT は、このトピックで説明する NAT 用語です。



このドキュメントでは、ChangeDST と ChangeSRC という頭字語を表と図の中で使用して、次の必要な動作を定義しています。

  - **ChangeDST**   NAT を使用しているネットワーク宛のパケット上の宛先 IP アドレスを変更するプロセスです。これは別名で透過性、ポート転送、宛先 NAT モード、ハーフ NAT モードなどとして知られます。

  - **ChangeSRC**   NAT を使用しているネットワークからのパケット上の送信元 IP アドレスを変更するプロセスです。これは別名でプロキシ、セキュア NAT、ステートフル NAT、送信元 NAT またはフル NAT モードなどとして知られます。

使用する名前付け規則に関わらず、エッジ サーバーの外部インターフェイスで必要な NAT 動作は次のとおりです。

  - インターネットからエッジの外部インターフェイスへ送信されるトラフィックの場合:
    
      - エッジの外部インターフェイスのパブリック IP アドレスからの受信パケットの宛先 IP アドレスを、エッジの外部インターフェイスの変換された IP アドレスに変更します。
    
      - 送信元 IP アドレスは変更しないでおくため、トラフィックの戻りのルートは存在します。

  - エッジの外部インターフェイスからインターネットへ送信されるトラフィックの場合:
    
      - エッジの外部インターフェイスから送信されるパケットの送信元 IP アドレスを、エッジの外部インターフェイスの変換された IP アドレスからパブリック IP アドレスに変更します。エッジの内部 IP アドレスはルーティング可能な IP アドレスではないため、公開されないようにするためです。
    
      - 送信パケットの宛先 IP アドレスは、変更しないでおきます。

次の図では、受信トラフィックの宛先 IP アドレスの変更 (ChangeDST) と、送信トラフィックの送信元 IP アドレスの変更 (ChangeSRC) の違いについて、音声ビデオ エッジの例を使用して説明しています。

**受信トラフィックの宛先 IP アドレスの変更 (ChangeDST) と送信元 IP アドレスの変更 (ChangeSRC)**

![送信先/送信元 IP アドレスの変更](images/Gg425882.0fee7ec5-4cb8-4aff-9164-e7fbab73336d(OCS.15).jpg "送信先/送信元 IP アドレスの変更")

主な点は次のとおりです。

  - 音声ビデオ エッジ サービスを実行しているサーバーへの受信トラフィックでは、送信元 IP アドレスは変更されませんが、宛先 IP アドレスは 131.107.155.30 から 10.45.16.10 という変換された IP アドレスに変更されます。

  - 音声ビデオ エッジ サービスを実行しているサーバーからワークステーションへの送信トラフィックでは、送信元 IP アドレスは、サーバーのパブリック IP アドレスから、音声ビデオ エッジ サービスを実行しているサーバーのパブリック IP アドレスに変更されます。また、宛先 IP は、ワークステーションのパブリック IP アドレスのままです。パケットが最初の NAT デバイスから送信されると、NAT デバイス上のルールによって、音声ビデオ エッジ サービスを実行しているサーバーの送信元 IP アドレスが、外部インターフェイスの IP アドレス (10.45.16.10) から、そのパブリック IP アドレス (131.107.155.30) に変更されます。

