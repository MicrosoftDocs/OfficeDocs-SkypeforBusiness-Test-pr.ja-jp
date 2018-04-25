---
title: New-CsTrunkConfiguration
TOCTitle: New-CsTrunkConfiguration
ms:assetid: f3958f86-3313-4929-9f9d-f796a2669aea
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg413021(v=OCS.15)
ms:contentKeyID: 48273978
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrunkConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

サービス プロバイダーの公衆交換電話網 (PSTN) ゲートウェイ、IP-PBX (インターネット プロトコル - 構内交換機)、セッション境界コントローラー (SBC) など、トランク ピア エンティティに関する設定を示す新しいトランク構成を作成します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsTrunkConfiguration -Identity <XdsIdentity> [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-InMemory <SwitchParameter>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、site:Redmond の ID を持つ新しいトランク構成を作成します。この新しい構成の残りのプロパティには既定値が設定されます。

    New-CsTrunkConfiguration -Identity site:Redmond

## 例 2

この例では、site:Redmond の ID を持つ新しいトランク構成を作成し、メディアのバイパスを有効にします。メディアのパイパスを有効にするため、EnableBypass パラメーターに値 $True を割り当てます。この新しい構成の残りのプロパティには既定値が設定されます。

    New-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## 例 3

この例では、site:Redmond の Identity を持つ新しいトランク構成を作成し、次に新しい発信変換をこのトランクに割り当てます。この例の 1 行目では、**New-CsTrunkConfiguration** コマンドレットを呼び出して新しいトランク構成を既定の設定で作成します。次の行では **New-CsOutboundTranslationRule** コマンドレットを呼び出します。ここで、ID の値に site:Redmond/OTR1 が割り当てられていることに注意してください。ID の最初の部分 (site:Redmond) では、ルールが適用されるスコープを定義します。このスコープは新しいトランク構成の ID に一致しています。つまり、このルールはこの構成に自動的に適用されます。スコープの後にはスラッシュ記号 (/) と文字列が続いています。この文字列は、単にこのルールの一意の名前です (ルールは各スコープに複数設定できます)。その後、Pattern パラメーターおよび Translation パラメーターに値を渡して、このルールを定義します。

    New-CsTrunkConfiguration -Identity site:Redmond
    New-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Pattern '^\+(\d{8})$' -Translation '9$1'

## 解説

このコマンドレットを使用すると、PSTN ゲートウェイ エンティティに適用できる新しいトランク構成を作成できます。各構成は、サービス プロバイダーの PSTN ゲートウェイ、IP-PBX、SBC のようなトランク ピア エンティティに関する特定の設定を格納しています。これらの設定では、このトランクでメディア バイパスが有効か、特定の条件下で Real-time Transport Control Protocol (RTCP) パケットを送信するか、セキュア リアルタイム プロトコル (SRTP) 暗号化を要求するかなどを構成します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**New-CsTrunkConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrunkConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p>XdsIdentity</p></td>
<td><p>トランク構成のスコープが含まれる一意識別子。トランク構成はサイト スコープでも、PSTN ゲートウェイ サービスのサービス スコープでも作成できます (グローバル構成は既定で存在し、削除または再作成することはできません)。たとえば、site:Redmond (サイトの場合)、または PstnGateway:Redmond.litwareinc.com (サービスの場合) のように入力します。</p></td>
</tr>
<tr class="even">
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターの値には、既知のメディア終端ポイントがあるかどうかを指定します (既知のメディア終端ポイントの例として、メディア終端が信号終端と同じ IP を持つ PSTN ゲートウェイがあります)。トランクに既知のメディア終端ポイントがない場合は、この値を False に設定します。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>トランク構成の目的を記述する文字列です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>3PCC プロトコルを使用して、転送された通話がホストされたサイトをバイパスできるようにするかどうかを指定します。3PCC は、「三者間通話コントロール」とも呼ばれ、第三者を使用して二人の通話者を接続するとき (たとえば、オペレーターが人物 A から人物 B への通話を接続するとき) に使用します。REFER メソッドは、送信者が提供する情報を使用して、受信者が第三者に連絡する必要があることを示す標準の SIP メソッドです。既定値は False ($False) です。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBypass</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターの値には、メディアのバイパスがこのトランクで有効かどうかを指定します。この値を True に設定してバイパスを有効にします。メディアのバイパスを有効にするには、PSTN ゲートウェイ、SBC、および PBX で次のものを含む特定の機能がサポートされている必要があります。</p>
<p>- 招待に対する分岐された応答を受信する機能。</p>
<p>- Lync Server クライアントとメディア終端ポイントは、仲介サーバー を介さずに直接通信できる必要があります。</p>
<p>- ゲートウェイのサブネットはクライアントのサブネットと同じサイトに定義する必要があります。別のサイトに定義した場合、制限された帯域幅を使用している WAN リンクでその 2 つのサイトを分割する必要があります。</p>
<p>メディア バイパスを有効にできるのは、次の状況下のみです。</p>
<p>- ConcentratedTopology パラメーターが True に設定されている</p>
<p>- EnableReferSupport パラメーターが False に設定され RTCPActiveCalls と RTCPCallsOnHold が False に設定されている、または EnableReferSupport が True に設定されている</p>
<p>EnableBypass が True で EnableReferSupport が False の場合は、それ以降に転送されるバイパス通話は、バイパスではなくなることに注意してください。</p>
<p>メディアのバイパスを特定のトランクに対して有効にするには、そのメディアのパイパスと対象のトランクをグローバルに有効にする必要があります。<strong>New-CsNetworkMediaBypassConfiguration</strong> コマンドレットを使用すると、メディアのバイパスをグローバルに有効にすることができます。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>True に設定されていると、10 秒以内にゲートウェイによって応答されなかった発信通話は次の使用可能なトランクにルーティングされます。追加のトランクがない場合、その通話は自動的に削除されます。その結果、ネットワーク速度とゲートウェイ応答が遅い組織では、通話が不必要に削除される可能性があります。</p>
<p>既定値は True です。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>True に設定すると、指定された SIP トランク構成設定のコレクションによって管理される SIP トランクを通過する通話に対して、ロケーション ベースの音声ルーティングが有効になります。ロケーション ベースの音声ルーティングでは、通話をルーティングするときに、発信ユーザーと着信ユーザーの両方のロケーションが考慮されます。このプロパティを True に設定する場合は (既定値は False)、NetworkSiteId プロパティも設定する必要があります。</p>
<p>このパラメーターは、Lync Server 2013 の 2013 年 2 月のバージョンで導入されました。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>サービス プロバイダーが携帯電話会社であるかどうかを定義します。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>SIP トランクがオンライン音声をサポートするかどうかを指定します。オンライン音声を使用すると、ユーザーは社内の Lync Server アカウントを使用しますが、ボイスメールは Office 365 でホストされます。既定値は False ($False) です。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>Presence Information Data Format Location Object (PIDF-LO) を含む緊急通話を、定義済みのゲートウェイ経由でルーティングするかどうかを定義します。緊急通話を、認定された緊急サービス プロバイダーにルーティングする場合は、このパラメーターを True に設定します (通話時に場所が送信されます)。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このトランクが、仲介サーバー からの REFER 要求の受信をサポートするかどうかを定義します。</p>
<p>メディア バイパスを有効にできるのは、次の状況下のみです。</p>
<p>- ConcentratedTopology パラメーターが True に設定されている</p>
<p>- EnableReferSupport パラメーターが False に設定され RTCPActiveCalls と RTCPCallsOnHold が False に設定されている、または EnableReferSupport が True に設定されている</p>
<p>EnableBypass が True で EnableReferSupport が False の場合は、それ以降に転送されるバイパス通話は、バイパスではなくなることに注意してください。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>SIP トランクが RTP ラッチをサポートするかどうかを指定します。RTP ラッチは、NAT (ネットワーク アドレス変換) 装置またはファイアウォールを経由した RTP/RTCP 接続を可能にする技術です。既定値は False ($False) です。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>セッション タイマーを有効にするかどうかを指定します。セッション タイマーを使用すると、特定のセッションがまだアクティブかどうかを判断できます。</p>
<p>このパラメーターが False に設定されている場合でも、リモート接続でセッション タイマーが有効になっている状況では、セッション タイマーを適用できることに注意してください。そのような状況では、仲介サーバー はリモート エンティティからのセッション タイマー プローブに応答します。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定した場合、サービス プロバイダーの PSTN ゲートウェイ、IP-PBX、または SBC は、仲介サーバー または Lync Server クライアントに送信される音声ストリームの中で音声の量を増やします。このパラメーターを False に設定すると、仲介サーバー (バイパスではない通話の場合)、または Lync Server クライアント (バイパス通話の場合) で音声の量が増やされます。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>通話履歴の情報をトランク経由で転送するかどうかを指定します。既定値は False ($False) です。</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardPAI</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>P-Asserted-Identity (PAI) ヘッダーを通話とともに転送するかどうかを指定します。PAI ヘッダーがあれば、発信者 ID を確認できます。既定値は False ($False) です。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>永続的な変更としてオブジェクトをコミットせずに、オブジェクト参照を作成します。このパラメーターを指定して呼び出したコマンドレットの出力を変数に割り当てる場合、オブジェクト参照のプロパティを変更し、コマンドレットに対応する Set- コマンドレットを呼び出してそれらの変更をコミットできます。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>省略可能</p></td>
<td><p>UInt32</p></td>
<td><p>サービス プロバイダーの PSTN ゲートウェイ、IP-PBX、または SBC が、仲介サーバー に送信した INVITE に対して受信できる分岐応答の最大数です。</p>
<p>既定値は次のとおりです。20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>トランク構成設定の新しいコレクションと関連付けられているネットワーク サイトのサイト ID です。EnableLocationRestriction プロパティを True に設定すると、このトランクを通過する場所に基づく音声ルーティングは、指定されたサイトに対して構成されている設定を使用して管理されます。ネットワーク サイト ID は、次のコマンドを使用して取得できます。</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p>
<p>このパラメーターは、Lync Server 2013 の 2013 年 2 月のリリースで導入されました。</p></td>
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
<td><p>発信ルーティングによって処理される通話 (PBX または PSTN の宛先にルーティングされる通話) に適用される、電話番号変換ルールのコレクションです。</p>
<p>この一覧とルールはこのコマンドレットを使用して直接作成できますが、発信変換ルールを作成する際には、<strong>New-CsOutboundTranslationRule</strong> コマンドレットを使用してルールを作成し、それをスコープが一致するトランク構成に割り当てるという方法を取ることをお勧めします。</p></td>
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
<td><p>このパラメーターでは、サービス プロバイダーの PSTN ゲートウェイ、IP-PBX、または SBC から送信される RTCP パケットがアクティブな通話に関するものかどうかを指定します。この文脈でアクティブな通話とは、メディアが少なくとも一方向へのフローを許可されている通話のことです。RTCPActiveCalls が True に設定されている場合は、仲介サーバー または Lync Server クライアントは 30 秒を上回る期間にわたって RTCP パケットを受信しないときに通話を終了することができます。</p>
<p>Lync Server の要素の中で、RTCP メディアがアクティブな通話であるかどうかのチェックを無効にすると、削除済みのピアに対する重要な保護策が削除されることに注意してください。必要な場合のみ、無効にしてください。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターでは、保留中の通話に対して、RTCP パケットのトランク経由での送信を続行するかどうか、およびメディア パケットがどちらの方向にもフローしないと予期されるかどうかを指定します。Lync Server クライアントとトランクのどちらかで保留音が有効になっている場合は、通話はアクティブであると見なされ、このプロパティは無視されます。そのような状況では、RTCPActiveCalls パラメーターを使用してください。</p>
<p>Lync Server の要素の中で、RTCP メディアがアクティブな通話であるかどうかのチェックを無効にすると、削除済みのピアに対する重要な保護策が削除されることに注意してください。必要な場合のみ、無効にしてください。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>サービス プロバイダーの PSTN ゲートウェイ、IP-PBX、または SBC から受信した応答コードに対して適用される、SIP 応答コード変換ルールから成る一覧です。管理者はこれらのルールを使用して、トランク経由で受信し 400 ～ 699 の値を持つ SIP 応答コードを、Lync Server との整合性がより高い新しい値にマッピングできます。</p>
<p>このコマンドレットで、この一覧およびそれに対応するルールを直接作成することもできます。ただし、SIP 応答コード変換ルールを作成するには、<strong>New-CsSipResponseCodeTranslationRule</strong> コマンドレットを呼び出すことをお勧めします。そのコマンドレットを実行すると、ルールが作成され、対応するスコープを持つトランク構成に対して割り当てられます。</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>省略可能</p></td>
<td><p>SRTPMode</p></td>
<td><p>このパラメーターの値には、仲介サーバーと、サービス プロバイダーの PSTN ゲートウェイ、IP-PBX、または SBC 間のメディア トラフィックを保護する SRTP のサポート レベルを指定します。メディア バイパスの場合、この値はメディア構成の EncryptionLevel 設定と互換性を持つ必要があります。メディア構成は、<strong>New-CsMediaConfiguration</strong> コマンドレットおよび <strong>Set-CsMediaConfiguration</strong> コマンドレットを使用して設定します。</p>
<p>有効な値は次のとおりです。</p>
<p>- Required:SRTP 暗号化を使用する必要があります。</p>
<p>- Optional:ゲートウェイでサポートされている場合は、SRTP が使用されます。</p>
<p>- NotSupported:SRTP 暗号化がサポートされていないので、使用されません。</p>
<p>注: SRTPMode は、ゲートウェイがトランスポート層セキュリティ (TLS) プロトコルを使用するよう構成されている場合にのみ使用されます。ゲートウェイがトランスポートとして伝送制御プロトコル (TCP) を使用するように構成されている場合は、SRTPMode は内部で NotSupported に設定されます。</p>
<p>既定値は次のとおりです。Required</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration 型のオブジェクトを作成します。

## 関連項目

#### その他のリソース

[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)

