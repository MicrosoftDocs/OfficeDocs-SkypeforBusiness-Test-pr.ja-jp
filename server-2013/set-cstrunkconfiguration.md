---
title: Set-CsTrunkConfiguration
TOCTitle: Set-CsTrunkConfiguration
ms:assetid: 18152388-68de-4a6b-b5a1-248534ecde72
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398238(v=OCS.15)
ms:contentKeyID: 48271391
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrunkConfiguration

 

_**トピックの最終更新日:** 2015-02-27_

既存のトランク構成を変更します。この構成は、公衆交換電話網 (PSTN) ゲートウェイ、IP-PBX、サービス プロバイダーのセッション境界コントローラー (SBC) などのトランキング ピア エンティティの設定を説明するものです。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsTrunkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsTrunkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、メディア バイパスを有効にするように、site:Redmond という Identity を持つトランク構成を変更しています。EnableBypass パラメーターに値 $True を割り当てることで、メディア バイパスを有効にしています。この構成の残りのプロパティには、既存の値が保持されます。

    Set-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## 例 2

この例では、site:Redmond という Identity を持つトランク構成に定義されている発信変換ルールを変更しています。この変更を行うために、実際には **Set-CsTrunkConfiguration** コマンドレットは呼び出していません。**Set-CsOutboundTranslationRule** コマンドレットを使用して行った変更が、発信変換ルールの Identity のスコープ部分と一致する Identity を持つトランク構成に自動的に反映されています。

    Set-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Translation '$1'

## 例 3

例 3 では、サイト スコープで定義されているすべてのトランク構成の SRTPMode を省略可能に設定しています。コマンドの最初の部分は **Get-CsTrunkConfiguration** コマンドレットの呼び出しで、Filter パラメーターを使用して site: で始まる Identity を持つすべてのトランク構成 (つまり、サイト レベルで定義されているすべてのトランク構成) を取得しています。この構成のコレクションを **Set-CsTrunkConfiguration** コマンドレットにパイプ処理して、それぞれの SRTPMode プロパティを省略可能に設定しています。

    Get-CsTrunkConfiguration -Filter site:* | Set-CsTrunkConfiguration -SRTPMode "Optional"

## 例 4

例 4 では、PIDF-LO サポートを有効にするように、site:Redmond という Identity を持つトランク構成を変更しています。既定では、EnablePIDFLOSupport パラメーターは False です。この例では、このパラメーターの値を True に設定し、緊急電話用の場所サポートを有効にしています。発信ルーティング アプリケーションによって場所情報がトランクに送信されるようにするには、EnablePIDFLOSupport を True に設定する必要があります。

    Set-CsTrunkConfiguration -Identity site:Redmond -EnablePIDFLOSupport $True

## 解説

このコマンドレットを使用して、PSTN ゲートウェイ エンティティに適用可能なトランク構成を変更します。それぞれの構成には、PSTN ゲートウェイ、IP-PBX、サービス プロバイダーの SBC などの、トランキング ピア エンティティの固有の設定が含まれます。これらの設定では、このトランクでメディア バイパスが有効かどうか、特定の条件下でリアルタイム転送制御プロトコル (RTCP) パケットを送信するかどうか、セキュア リアルタイム プロトコル (SRTP) 暗号化を要求するかどうかなどを構成します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Set-CsTrunkConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrunkConfiguration"}

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
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターの値で、既知のメディア終端ポイントがあるかどうかを指定します (既知のメディア終端ポイントの例として、メディア終端が信号終端と同じ IP を持つ PSTN ゲートウェイがあります)。トランクに既知のメディア終端ポイントがない場合、この値を False に設定します。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>トランク構成の目的を説明する文字列。</p></td>
</tr>
<tr class="even">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>3PCC プロトコルを使用して、転送された通話が、ホストされているサイトをバイパスできるようにするかどうかを指定します。3PCC は、&quot;三者間通話コントロール&quot; とも呼ばれ、第三者を使用して 2 人の通話者を接続するとき (たとえば、オペレーターが人物 A から人物 B への通話を接続するとき) に使用します。REFER メソッドは、送信者が提供する情報を使用して、受信者が第三者に連絡する必要があることを示す標準の SIP メソッドです。既定値は False ($False) です。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBypass</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターの値で、このトランクに対してメディア バイパスを有効にするかどうかを指定します。この値を True に設定するとバイパスを有効にできます。メディア バイパスが正常に機能するには、PSTN ゲートウェイ、SBC、PBX で次のような特定の機能がサポートされている必要があります。</p>
<p>- 招待に対する分岐された応答を受信する機能。</p>
<p>- Lync Server クライアントとメディア終端ポイントが仲介サーバーを介さずに直接通信できる。</p>
<p>- ゲートウェイのサブネットがクライアントのサブネットと同じサイトに存在するよう定義されている。または、異なるサイトの場合、制限された帯域幅を使用している WAN リンクによってこれらのサイトが分離されていない。</p>
<p>メディア バイパスは、次の状況でのみ有効になります。</p>
<p>- ConcentratedTopology パラメーターが True に設定されている。</p>
<p>- EnableReferSupport パラメーターが False に設定されている、RTCPActiveCalls と RTCPCallsOnHold が False に設定されている、または EnableReferSupport が True に設定されている。</p>
<p>EnableBypass が True で EnableReferSupport が False の場合、次に転送されるバイパス呼び出しはバイパス不可になります。</p>
<p>メディアのバイパスを特定のトランクに対して有効にするには、そのメディアのパイパスと対象のトランクをグローバルに有効にする必要があります。<strong>New-CsNetworkMediaBypassConfiguration</strong> コマンドレットを使用すると、メディアのバイパスをグローバルに有効にすることができます。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>True に設定されていると、10 秒以内にゲートウェイによって応答されなかった発信通話は次の使用可能なトランクにルーティングされます。追加のトランクがない場合、その通話は自動的に削除されます。その結果、ネットワーク速度とゲートウェイ応答が遅い組織では、通話が不必要に削除される可能性があります。</p>
<p>既定値は True です。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>True に設定されている場合は、SIP トランクの構成設定の指定されたコレクションによって管理される SIP トランクを通過する通話で、場所に基づいた音声ルーティングが有効になります。場所に基づいた音声ルーティングの場合、ユーザーが通話を開始した場所と着信した場所を、通話をルーティングするときに考慮します。このプロパティが True に設定されている場合は、NetworkSiteId プロパティも同時に True に設定します。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>サービス プロバイダーが携帯電話会社であるかどうかを定義します。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>SIP トランクがオンライン音声をサポートするかどうかを指定します。オンライン音声を使用すると、ユーザーは社内の Lync Server アカウントを使用しますが、ボイスメールは Skype for Business Online でホストされます。既定値は False ($False) です。</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>定義されたゲートウェイ経由でプレゼンス情報データ形式場所オブジェクト (PIDF-LO) を使用して緊急電話をルーティングするかどうかを定義します。緊急電話が特定の緊急サービス プロバイダーにルーティングされる場合には、このパラメーターを True に設定します (場所は通話と共に送信されます)。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このトランクが、仲介サーバー からの REFER 要求の受信をサポートするかどうかを定義します。</p>
<p>メディア バイパスは、次の状況でのみ有効になります。</p>
<p>- ConcentratedTopology パラメーターが True に設定されている。</p>
<p>- EnableReferSupport パラメーターが False に設定されている、RTCPActiveCalls と RTCPCallsOnHold が False に設定されている、または EnableReferSupport が True に設定されている。</p>
<p>EnableBypass が True で EnableReferSupport が False の場合、次に転送されるバイパス呼び出しはバイパス不可になります。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>SIP トランクが RTP ラッチをサポートするかどうかを指定します。RTP ラッチは、NAT (ネットワーク アドレス変換) 装置またはファイアウォールを経由した RTP/RTCP 接続を可能にする技術です。既定値は False ($False) です。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>セッション タイマーを有効にするかどうかを指定します。セッション タイマーは、特定のセッションが継続してアクティブであるかどうかを特定するために使用します。</p>
<p>このパラメーターが False に設定されていても、セッション タイマーがリモート接続により有効にされた場合は適用可能です。その場合、仲介サーバー はリモート エンティティからのセッション タイマー プローブに返信します。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定した場合、PSTN ゲートウェイ、IP-PBX、またはサービス プロバイダーの SBC では、仲介サーバーまたは Lync Server クライアントに送信される音声ストリームの音声の量が増大します。この値を False に設定した場合、音声は仲介サーバー (バイパス不可通話の場合) または Lync Server クライアント (バイパス通話の場合) のどちらかで増大します。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>通話履歴の情報をトランク経由で転送するかどうかを指定します。既定値は False ($False) です。</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardPAI</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>P-Asserted-Identity (PAI) ヘッダーを通話とともに転送するかどうかを指定します。PAI ヘッダーがあれば、発信者 ID を確認できます。既定値は False ($False) です。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsIdentity</p></td>
<td><p>トランク構成のスコープを含む一意の識別子。トランク構成はグローバル スコープまたはサイト スコープでも、PSTN ゲートウェイ サービスのサービス スコープでも存在することができます。たとえば、site:Redmond (サイト用) または PstnGateway:Redmond.litwareinc.com (サービス用) です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>TrunkConfiguration</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。</p>
<p>このパラメーターは、Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 型のオブジェクトが必要です。このオブジェクトは、<strong>Get-CsTrunkConfiguration</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>省略可能</p></td>
<td><p>UInt32</p></td>
<td><p>PSTN ゲートウェイ、IP-PBX、またはサービス プロバイダーの SBC が、仲介サーバー に送信した INVITE に対して受信できる分岐応答の最大数です。</p>
<p>既定値は次のとおりです。20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>ネットワーク サイトのサイト ID は、トランクの構成設定のコレクションに関連付けられています。EnableLocationRestriction プロパティが True に設定されている場合、場所に基づいた音声ルーティングで、このトランクを通じてルーティングされるものは、指定のサイトの構成設定を使って管理されます。ネットワーク サイト ID はこのコマンドを使って取得できます。</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>トランクに割り当てられた発信電話番号の変換ルールのコレクションです。次のコマンドを実行することによって、利用できるルールに関する情報を取得できます。</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>発信ルーティングで処理される通話 (通話先の PBX または PST にルーティングされる通話) に適用される、電話番号変換ルールのコレクション。</p>
<p>このコマンドレットを使用して、このリストとこれらのルールを直接変更することもできますが、<strong>Set-CsOutboundTranslationRule</strong> コマンドレットを使用して発信変換ルールを変更することをお勧めします。<strong>Set-CsOutboundTranslationRule</strong> コマンドレットを実行すると、ルールが変更されて、これらの変更がトランク構成に自動的に反映されます。新しい発信変換ルールを追加してトランク構成を変更するには、<strong>New-CsOutboundTranslationRule</strong> コマンドレットを呼び出します。新しいルールが、一致するスコープがあるトランク構成に追加されます。</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>トランクに割り当てられた PSTN 使用法のコレクションです。次のコマンドを実行することによって、利用できる使用法に関する情報を取得できます。</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、仲介サーバー が Uniform Resource Identifier (URI) をサービス プロバイダーに送信する前に、その URI から先行する正符号 (+) を削除します。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターでは、アクティブな通話に対して、RTCP パケットが PSTN ゲートウェイ、IP-PBX、またはサービス プロバイダーの SBC から送信されるかどうかを指定します。この場合のアクティブな通話とは、メディアが最低でも一方向に流れることのできる通話のことです。RTCPActiveCalls が True に設定されている場合、仲介サーバー または Lync Server クライアントは、30 秒を超過しても RTCP パケットを受信しない場合に通話を終了することができます。</p>
<p>Lync Server の要素のアクティブな通話に対する受信 RTCP メディアのチェックを無効にすることは、欠落したピアを検出するための重要なセーフガードをなくすことになるので、必要な場合にのみ実行する必要があります。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターでは、保留中で、どの方向にも流れることが予想されるメディア パケットがない通話に対して、RTCP パケットのトランク経由での送信を続行するかどうかを指定します。保留音が Lync Server クライアントまたはトランクで有効な場合、通話はアクティブと見なされ、このプロパティは無視されます。そのような状況では RTCPActiveCalls パラメーターを使用します。</p>
<p>Lync Server の要素のアクティブな通話に対する受信 RTCP メディアのチェックを無効にすることは、欠落したピアを検出するための重要なセーフガードをなくすことになるので、必要な場合にのみ実行する必要があります。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>PSTN ゲートウェイ、IP-PBX、サービス プロバイダーの SBC から受信した応答コードに適用する SIP 応答コード変換ルールの一覧。これらのルールにより、管理者はトランク経由で受信した 400 から 699 の間の値の SIP 応答コードを、Lync Server とより整合性のある新しい値にマップできます。</p>
<p>このコマンドレットで、この一覧およびそれに対応するルールを直接作成することもできます。ただし、SIP 応答コード変換ルールを作成するには、<strong>New-CsSipResponseCodeTranslationRule</strong> コマンドレットを呼び出すことをお勧めします。そのコマンドレットを実行すると、ルールが作成され、対応するスコープを持つトランク構成に対して割り当てられます。</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>省略可能</p></td>
<td><p>SRTPMode</p></td>
<td><p>このパラメーターの値には、仲介サーバーと、サービス プロバイダーの PSTN ゲートウェイ、IP-PBX、または SBC 間のメディア トラフィックを保護する SRTP のサポート レベルを指定します。メディア バイパスの場合、この値はメディア構成の EncryptionLevel 設定と互換性を持つ必要があります。メディア構成は、<strong>New-CsMediaConfiguration</strong> コマンドレットおよび <strong>Set-CsMediaConfiguration</strong> コマンドレットを使用して設定します。</p>
<p>有効な値は次のとおりです。</p>
<p>- Required:SRTP 暗号化を使用する必要があります。</p>
<p>- Optional:サービス プロバイダーがサポートしている場合、SRTP を使用します。</p>
<p>- NotSupported:SRTP 暗号化はサポートされていないため、使用されません。</p>
<p>注: SRTPMode はゲートウェイがトランスポート層セキュリティ (TLS) を使用するように構成されている場合にのみ使用されます。ゲートウェイがトランスポートとして伝送制御プロトコル (TCP) を使用して構成されている場合、SRTPMode は内部的に NotSupported に設定されます。</p>
<p>既定値は次のとおりです。必須</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration オブジェクト。トランク構成オブジェクトのパイプライン処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 型のオブジェクトが変更されます。

## 関連項目

#### その他のリソース

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)

