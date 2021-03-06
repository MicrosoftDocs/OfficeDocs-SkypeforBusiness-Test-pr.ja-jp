﻿---
title: 'Lync Server 2013: 中央サイトの音声の復元の計画'
TOCTitle: 中央サイトの音声の復元の計画
ms:assetid: 52dd0c3e-cd3c-44cf-bef5-8c49ff5e4c7a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398347(v=OCS.15)
ms:contentKeyID: 48272091
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 での中央サイトの音声の復元の計画

 

_**トピックの最終更新日:** 2015-03-09_

世界中に多数のサイトを持つ企業がますます増えています。エンタープライズ VoIP 復旧ソリューションでは、中央サイトのサービスが停止したときに、緊急サービス、ヘルプ デスクへのアクセス、および重要なビジネス タスクの遂行能力を維持することが不可欠となっています。中央サイトを利用できなくなった場合、以下の条件を満たすことが求められます。

  - ボイス フェールオーバーを備えることが必要です。

  - 通常、中央サイトの フロント エンド プールに登録しているユーザーは、代替 フロント エンド プールに登録できる必要があります。それには、複数の DNS SRV レコードを作成し、それぞれのレコードが各中央サイトの ディレクター プールまたは フロント エンド プールに解決されるようにします。SRV レコードの優先順位と重みを調整することで、その中央サイトで処理されるユーザーが、他の SRV レコードのディレクター プールとフロントエンド プールよりも先に、対応する ディレクターと フロント エンド プールを取得できるようになります。

  - 他のサイトに存在するユーザーとの通話を、PSTN に再ルーティングする必要があります。

このトピックでは、中央サイトの音声復元をセキュリティ保護するための推奨ソリューションについて説明します。

## アーキテクチャおよびトポロジ

中央サイトでの音声復元を計画する場合、ボイス フェールオーバーを実現する際に Lync Server 2013 レジストラーが担う中心的な役割に関する基本的な知識が必要となります。Lync Server レジストラーは、クライアントの登録と認証を可能にし、ルーティング サービスを提供するサーバーの役割です。レジストラーは、Standard Edition サーバー、フロント エンド サーバー、ディレクター、または 存続可能ブランチ アプライアンス上に他のコンポーネントと共に存在します。レジストラー プールは、フロント エンド プールで実行され、同じサイトに存在するレジストラー サービスで構成されます。フロント エンド プールは負荷分散する必要があります。DNS 負荷分散をお勧めしますが、ハードウェア負荷分散でも十分です。Lync クライアントは、次の検出メカニズムを使用して フロント エンド プールを検出します。

1.  DNS SRV レコード

2.  自動検出 Web サービス (Lync Server 2013 の新機能)

3.  DHCP オプション 120

Lync クライアントが フロント エンド プールに接続すると、ロード バランサーによってプール内の フロント エンド サーバーのいずれかにリダイレクトされます。次に、その フロント エンド サーバーがプール内の優先レジストラーにクライアントをリダイレクトします。

エンタープライズ VoIP が有効になっている各ユーザーは、そのユーザーのプライマリ レジストラー プールになる特定のレジストラー プールに割り当てられます。特定のサイトで、通常、数百人または数千人のユーザーが 1 つのプライマリ レジストラー プールを共有します。プレゼンス、会議、またはフェールオーバーのために中央サイトに依存するブランチ サイトのユーザーによる中央サイトのリソース消費に対応するには、各ブランチ サイトのユーザーを、中央サイトに登録されたユーザーと同様に扱うことをお勧めします。現在、存続可能ブランチ アプライアンスに登録されたユーザーを含め、ブランチ サイトのユーザー数に制限はありません。

中央サイトの障害時に音声を確実に復元するには、プライマリ レジストラー プールで、別のサイトに配置された単一のバックアップ レジストラー プールを指定しておく必要があります。バックアップは、トポロジ ビルダーの復元設定を使用して構成できます。2 つのサイト間の WAN リンクが復元できている場合は、プライマリ レジストラー プールを使用できなくなったユーザーは自動的にバックアップ レジストラー プールにダイレクトされます。

以下のステップでは、クライアントの検出と登録のプロセスについて説明します。

1.  クライアントは DNS SRV レコードによって Lync Server を検出します。Lync Server 2013 では、DNS SRV クエリに対して複数の FQDN を返すように DNS SRV レコードを構成できます。たとえば、企業 Contoso に 3 つの中央サイト (北米、欧州、およびアジア太平洋) があり、各中央サイトにディレクター プールがある場合、DNS SRV レコードで 3 つの各場所のディレクター プールの FQDN を指すことができます。このいずれかの場所のディレクター プールが使用可能であれば、クライアントは最初のホップである Lync Server に接続できます。
    
    > [!NOTE]
    > ディレクター プールの使用はオプションです。代わりに、フロント エンド プールを使用できます。


2.  ディレクター プールは、ユーザーのプライマリ レジストラー プールとバックアップ レジストラー プールの情報を Lync クライアントに通知します。

3.  Lync クライアントは、まずユーザーのプライマリ レジストラー プールへの接続を試みます。プライマリ レジストラー プールが使用可能な場合、レジストラーは登録を受け入れます。プライマリ レジストラー プールを使用できない場合、Lync クライアントはバックアップ レジストラー プールへの接続を試みます。バックアップ レジストラー プールが使用可能であり、(指定したフェールオーバーの間隔でハートビートが送信されないことを検出して) ユーザーのプライマリ レジストラー プールを使用できないと判断された場合、バックアップ レジストラー プールはユーザーの登録を受け入れます。プライマリ レジストラーが再び使用可能になったことをバックアップ レジストラーが検出すると、バックアップ レジストラー プールはフェールオーバー Lync クライアントをプライマリ プールにリダイレクトします。

以下の図に、中央サイトの復元を確実にするための推奨トポロジを示します。2 つのサイトは復元 WAN リンクで接続されています。中央サイトが使用できなくなると、そのプールに割り当てられているユーザーは、バックアップ サイトにダイレクトされて登録が行われます。

**中央サイトの音声復元を確保する推奨トポロジ**

![中央サイトの音声復元のトポロジ](images/Gg398347.19ea3e74-8a5c-488c-a34e-fc180ab9a50a(OCS.15).jpg "中央サイトの音声復元のトポロジ")

## 要件と推奨事項

中央サイトで音声復元を実装するための要件と推奨事項は、たいていの組織で適しています。

  - プライマリおよびバックアップ レジストラー プールのあるサイトは、復元 WAN リンクで接続する必要があります。

  - 各中央サイトには、1 つ以上のレジストラーで構成されるレジストラー プールが存在する必要があります。

  - 各レジストラー プールは、DNS 負荷分散かハードウェア負荷分散またはその両方を使用して負荷分散する必要があります。ハードウェア負荷分散構成の計画の詳細については、「[Lync Server 2013 での負荷分散の要件](lync-server-2013-load-balancing-requirements.md)」を参照してください。

  - 各ユーザーは、Lync Server 管理シェル**set-CsUser** コマンドレットまたは Lync Server コントロール パネルを使用して、プライマリ レジストラー プールに割り当てる必要があります。

  - プライマリ レジストラー プールは、別の中央サイトに配置されたバックアップ レジストラー プールを 1 つ持つ必要があります。

  - プライマリ レジストラー プールは、バックアップ レジストラー プールにフェールオーバーするように構成する必要があります。既定では、プライマリ レジストラーは 300 秒の間隔が経過した後でバックアップ レジストラー プールにフェールオーバーするように設定されています。この間隔は、Lync Server 2013 トポロジ ビルダーを使用して変更できます。

  - 「計画」のドキュメントの「[Lync Server 2013 でのフェールオーバー ルートの構成](lync-server-2013-configuring-a-failover-route.md)」の説明に従ってフェールオーバー ルートを構成してください。ルートを構成する際、プライマリ ルートで指定されたゲートウェイとは別のサイトにあるゲートウェイを指定します。

  - 中央サイトにプライマリ管理サーバーがあり、サイトが長期間ダウンする可能性が高い場合、管理ツールをバックアップ サイトに再インストールする必要があります。そうしないと、どの管理設定も変更できなくなります。

## 依存関係

Lync Server は、音声復元を確実に実現するために、以下のインフラストラクチャとソフトウェア コンポーネントを使用しています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>コンポーネント</strong></p></td>
<td><p><strong>機能</strong></p></td>
</tr>
<tr class="even">
<td><p>DNS</p></td>
<td><p>SRV レコードおよび A レコードを解決して、サーバー間の接続およびサーバーとクライアント間の接続を確立</p></td>
</tr>
<tr class="odd">
<td><p>Exchange および Exchange Web サービス (EWS)</p></td>
<td><p>コンタクト ストレージ、予定表データ</p></td>
</tr>
<tr class="even">
<td><p>Exchange ユニファイド メッセージングおよび Exchange Web サービス</p></td>
<td><p>通話ログ、ボイス メール一覧、ボイス メール</p></td>
</tr>
<tr class="odd">
<td><p>DHCP オプション 120</p></td>
<td><p>DNS SRV を使用できない場合、クライアントは DHCP オプション 120 を使用してレジストラーの検出を試みます。これを機能させるには、DHCP サーバーを構成するか、Lync Server 2013 DHCP を有効にする必要があります。詳細については、「<a href="lync-server-2013-branch-site-resiliency-requirements.md">Lync Server 2013 のブランチ サイトの復元要件</a>」の「ブランチ サイトの復元のハードウェアおよびソフトウェア要件」を参照してください。</p></td>
</tr>
</tbody>
</table>


## 存続可能な音声機能

前述の要件と推奨事項が実装されている場合は、以下の音声機能がバックアップ レジストラー プールによって提供されます。

  - PSTN 通話の発信

  - テレフォニー サービス プロバイダーがバックアップ サイトへのフェールオーバー機能をサポートしている場合は、PSTN 通話の着信

  - 同じサイトおよび 2 つの異なるサイト間でのユーザー同士のエンタープライズ通話

  - 通話の保留、取得、転送などの基本的な通話処理

  - 2 者間のインスタント メッセージングおよび同じサイトでのユーザー間のオーディオとビデオの共有

  - 着信の転送、エンドポイントの同時呼び出し、通話委任、およびチーム通話サービス。ただし、通話委任の両者または全チーム メンバーが同じサイトで構成されている場合のみ。

  - 既存の電話およびクライアントは動作し続けます。

  - 通話詳細記録 (CDR)

  - 認証と承認

プライマリ中央サイトがサービス停止になったときに以下の音声機能が動作するかどうかは、その構成方法によります。

  - ボイス メールの預かりと取得
    
    プライマリ中央サイトがサービス停止になっているときに Exchange UM を使用可能にするには、以下のいずれかを実行する必要があります。
    
      - 中央サイトの Exchange UM サーバーが別のサイトのバックアップ Exchange UM サーバーをポイントするように、DNS SRV レコードを変更します。
    
      - 中央サイトとバックアップ サイトの両方の Exchange UM サーバーを含めるように各ユーザーの Exchange UM ダイヤル プランを構成します。ただし、バックアップ Exchange UM サーバーは無効にするよう指定します。プライマリ サイトが使用できなくなった場合、Exchange 管理者がバックアップ サイトの Exchange UM サーバーを有効としてマークする必要があります。
    
    前述のソリューションのいずれも使用できない場合、中央サイトが使用できなくなると、Exchange UM は使用できなくなります。

  - すべての種類の会議
    
    バックアップ サイトにフェールオーバーしたユーザーは、プールを使用できる開催者によって作成またはホストされる会議に出席できますが、使用不可になった自身のプライマリ プールで会議を作成またはホストすることはできません。他のユーザーも、そのユーザーのプライマリ プールでホストされる会議に参加することはできません。

以下の音声機能は、プライマリ中央サイトが停止しているときには動作しません。

  - 会議自動アテンダント

  - プレゼンスおよび DND ベースのルーティング

  - 着信の転送設定の更新

  - 応答グループ サービスとコール パーク

  - 新しい電話とクライアントのプロビジョニング

  - アドレス帳 Web 検索

## 関連項目

#### その他のリソース

[Lync Server 2013 ブランチ サイト VoIP の復元の計画](lync-server-2013-planning-for-branch-site-voice-resiliency.md)

