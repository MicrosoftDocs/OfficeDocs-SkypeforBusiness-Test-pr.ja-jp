---
title: Set-CsPstnGateway
TOCTitle: Set-CsPstnGateway
ms:assetid: 5d61e7e5-dacb-4dd3-bdd5-b757d98181d3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398408(v=OCS.15)
ms:contentKeyID: 48272252
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnGateway

 

_**トピックの最終更新日:** 2015-03-09_

公衆交換電話網 (PSTN) ゲートウェイのプロパティを変更します。PSTN ゲートウェイは、外部の PSTN ネットワーク上のデバイスと内部のエンタープライズ VoIP ネットワーク上のデバイスとの間で通話をルーティングするのに役立ちます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsPstnGateway [-Identity <XdsGlobalRelativeIdentity>] [-AlternateByPassId <String>] [-Confirm [<SwitchParameter>]] [-Default <$true | $false>] [-Force <SwitchParameter>] [-GatewaySipClientTcpPort <UInt16>] [-GatewaySipClientTlsPort <UInt16>] [-MediationServer <String>] [-RepresentativeMediaIP <String>] [-Routable <$true | $false>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 に示すコマンドでは、ゲートウェイ PstnGateway:192.168.0.240 を既定のゲートウェイに構成しています。つまり、PstnGateway:192.168.0.240 を使用して Office Communications Server 2007 R2 を発信元とする通話を処理できます。

    Set-CsPstnGateway -Identity "PstnGateway:192.168.0.240" -Default $True

## 例 2

例 2 では、組織内のすべての PSTN ゲートウェイを構成し、これらのゲートウェイをそれぞれ発信ルーティングで使用できるようにしています。これを実行するため、まず、**Get-CsService** コマンドレットと PstnGateway パラメーターを使用して、現在使用しているすべての PSTN ゲートウェイのコレクションを戻します。次にこのコレクションを、**ForEach-Object** コマンドレットにパイプ処理します。**ForEach-Object** コマンドレットは、コレクションの各ゲートウェイに対して **Set-CsPstnGateway** コマンドレットを実行し、それぞれの Routable プロパティを True に設定します。

    Get-CsService -PstnGateway | ForEach-Object {Set-CsPstnGateway -Identity $_.Identity -Routable $True}

## 解説

PSTN ゲートウェイを使用すると、エンタープライズ VoIP のユーザーは、PSTN ネットワーク上のユーザーに通話を発信したり、PSTN ネットワーク上のユーザーから通話を受信したりできます。これらのゲートウェイは、仲介サーバーと PSTN ネットワークの間のブリッジとして動作します。

PSTN ゲートウェイは、通常、時分割多重構内交換網 (PBX) 電話システムを使用する場合に必要になります。その場合、一般的には、エンタープライズ VoIP 通話を PSTN ネットワークにルーティングするために PSTN ゲートウェイと仲介サーバーが必要です。一方、IP-PBX システムを使用する場合は、PBX と仲介サーバーの間に直接 SIP 接続を作成して、PSTN ゲートウェイを不要にすることができます。

PSTN ゲートウェイは、インストールして構成した後、**Set-CsPstnGateway** コマンドレットを使用して管理できます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Set-CsPstnGateway** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnGateway"}

## パラメーター


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>必須かどうか</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AlternateByPassId</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>代替バイパス ID を表すグローバル一意識別子 (GUID) です。この ID は Lync Server によって自動生成され、ヘアピン コールを排除するために使用されます。この ID により、システムの構成方法に応じて、ヘアピン コールが自動的に 仲介サーバー をバイパスするように設定できます。ユーザーが個々のサブネットを定義し、すべてのサイトおよび地域と関連付ける必要はありません。</p>
<p>これを行うには、一般に、バイパスをグローバルに有効にしてネットワーク構成サイトと地域を使用し、使用する PSTN ゲートウェイのトランク構成のバイパスを有効にする必要があります。</p>
<p>ヘアピン コールは、PSTN ネットワークからの着信通話が、着信の転送または同時呼び出しを使用してそのネットワークまでルーティングして戻される場合に発生します。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Default</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True に設定すると、このゲートウェイは Office Communications Server 2007 R2 から送信される通話を処理します。1 つの仲介サーバーによって管理されるゲートウェイのコレクションには、既定のゲートウェイを 1 つだけ含めることができます。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドレットを実行するときに発生する可能性のある、すべての確認メッセージまたは致命的ではないエラー メッセージが表示されないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>GatewaySipClientTcpPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>伝送制御プロトコル (TCP) による仲介サーバーとの通信で使用するリッスン ポートです。既定値は 5066 です。</p></td>
</tr>
<tr class="even">
<td><p><em>GatewaySipClientTlsPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.UInt16</p></td>
<td><p>トランスポート層セキュリティ (TLS) プロトコルによる仲介サーバーとの通信で使用するリッスン ポートです。既定値は 5067 です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>変更する PSTN ゲートウェイのサービス ID です。次に例を示します。-Identity &quot;PstnGateway:192.168.0.240&quot;。</p>
<p>PSTN ゲートウェイを指定するときには、&quot;PstnGatewayServer:&quot; プレフィックスを省略できます。次に例を示します。-Identity &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>MediationServer</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>PSTN ゲートウェイと関連付ける仲介サーバーのサービス ID です。次に例を示します。-MediationServer &quot;MediationServer:atl-cs-001.litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>RepresentativeMediaIP</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>ゲートウェイと関連付けるメディア プロセッサの IP アドレスです。プロセッサの場所が信号送信アドレスと異なることが前提です。メディア バイパスと通話受付管理 (CAC) の両方は、ゲートウェイのメディア プロセッサの場所に基づいています。既定では信号送信アドレスと同じ場所になります。2 つの場所が異なる場合 (たとえば、メディア プロセッサがリモート サイトにあり、信号発信ピアがセントラル サイトにある場合) は、メディア プロセッサの IP アドレスを使用して RepresentativeMediaIP を構成する必要があります。</p>
<p>同じサイトに複数のメディア プロセッサを展開しており、それぞれに独自の IP アドレスがある場合は、RepresentativeMediaIP プロパティの構成時にそれらの IP アドレスのいずれかを使用できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Routable</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True に設定すると、ゲートウェイを発信ルーティングのルートで使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Get-CsPstnGateway** コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

**Set-CsPstnGateway** コマンドレットはオブジェクトまたは値を戻しません。代わりに、Microsoft.Rtc.Management.Xds.DisplayPstnGateway オブジェクトの既存のインスタンスを変更します。

## 関連項目

#### その他のリソース

[Get-CsService](get-csservice.md)

