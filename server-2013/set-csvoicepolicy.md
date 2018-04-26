---
title: Set-CsVoicePolicy
TOCTitle: Set-CsVoicePolicy
ms:assetid: e6035b74-d760-4c48-aa0b-d09d129e0830
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399021(v=OCS.15)
ms:contentKeyID: 48273891
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicePolicy

 

_**トピックの最終更新日:** 2015-03-09_

既存の音声ポリシーを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsVoicePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、ユーザーごとのポリシー UserVoicePolicy2 の AllowSimulRing プロパティを False に設定しています。つまり、このポリシーを割り当てられたユーザーは、同時呼び出し (会社の電話への着信時に携帯電話などの 2 番目の電話を呼び出すかどうかを決定する機能) を使用できません。このコマンドはまた、このポリシーの PSTN 使用法の一覧から "Local" を削除します (Identity パラメーターが明示的に指定されていないことに注意してください。Identity パラメーターは位置パラメーターであるため、ID 値をパラメーター一覧の最初に設定しておけば、Identity であることを明示する必要はありません)。

    Set-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{remove="Local"}

## 例 2

この例では、サイト Redmond の音声ポリシーを変更して、組織で定義されたすべての PSTN 使用法がこのポリシーに適用されるようにしています。この例の最初の行で **Get-CsPstnUsage** コマンドレットを呼び出して、組織のグローバルな PSTN 使用法のセットを取得し、そのセットを変数 $a に保存します。2 行目では **Set-CsVoicePolicy** コマンドレットを呼び出し、サイト Redmond の音声ポリシーを変更します。値は PstnUsages パラメーターに渡され、ポリシーの現在の使用法の一覧を、グローバルな PSTN 使用法のセットに含まれた一覧に置き換えています。置換値の構文 $a.Usage。この構文を使用して、(PSTN 使用法の一覧が含まれた) PSTN 使用法の設定の Usage プロパティを参照しています。

    $a = Get-CsPstnUsage
    Set-CsVoicePolicy -Identity site:Redmond -PstnUsages @{replace=$a.Usage}

## 解説

このコマンドレットは、既存の音声ポリシーを変更します。音声ポリシーは、同時呼び出し (会社の電話への着信時に 2 番目の電話を呼び出す機能) や自動転送などの、エンタープライズ VoIP 関連機能の管理に使用されます。このコマンドレットを使用して、多くのエンタープライズ VoIP 関連機能を有効および無効にする設定を変更します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーは **Set-CsVoicePolicy** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicePolicy"}

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
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、このポリシーに割り当てられたユーザーが呼び出しを転送できます。このパラメーターが False に設定されていると、呼び出しを転送できません。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、別のプールに所属する内部番号に呼び出しがあった際にそのプールまたは WAN を使用できない場合、公衆交換電話網 (PSTN) を使ってルーティングします。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>同時呼び出しは、1 つの番号がダイヤルされた際に複数の電話を呼び出せるようにする機能です。このパラメーターを True に設定すると、同時呼び出しが有効となります。このパラメーターが False に設定されていると、このポリシーに割り当てられているユーザーで同時呼び出しを構成することはできません。</p></td>
</tr>
<tr class="even">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>省略可能</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>管理者が着信の転送および同時呼び出しを管理する方法を提供します。有効な値は次のとおりです。</p>
<p>* VoicePolicyUsage – 既定の音声ポリシー使用法を使って、すべての通話に対する着信の転送および同時呼び出しを管理します。これは既定の値です。</p>
<p>* InternalOnly – 着信の転送および同時呼び出しは、1 人の Lync ユーザーから他の 1 人にかけた通話に限定されます。</p>
<p>* CustomUsage – カスタムの PSTN 使用法を使って、着信の転送および同時呼び出しを管理します。この使用法は、CustomCallForwardingSimulRingUsages パラメーターを使用して指定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>着信の転送および同時呼び出しの管理に使用するカスタムの PSTN 使用法です。音声ポリシーにカスタムの使用法を追加するには、次のような構文を使用します。</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>カスタムの使用法を削除するには、次の構文を使用します。</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>CustomCallForwardingSimulRingUsages パラメーターで使用する前に、その使用法が存在している必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>音声ポリシーの説明です。</p>
<p>最大長: 1040 文字</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>帯域幅を制限するようにポリシーを設定できます。また、ネットワーク構成に関する他の各種プロパティを設定できます。このパラメーターを True に設定すると、これらのポリシーが優先されます。つまり、このパラメーターを True に設定すると帯域幅の確認は行われず、呼び出しは通話受付管理 (CAC) 設定に関係なく処理されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallPark</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>コール パーク アプリケーション を使用すると、さまざまな番号の中の特定の番号で呼び出しを保留 (パーク) しておき、後で受けることができます。このパラメーターを True に設定すると、このポリシーに割り当てられているユーザーに対してこのアプリケーションが有効になります。このパラメーターを False に設定すると、このポリシーに割り当てられているユーザーは、自分の電話番号への呼び出しを保留することができません。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>呼び出しを別の番号に転送できるかどうかを決定します。このパラメーターを True に設定すると呼び出しを転送することができ、False に設定すると転送することができません。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDelegation</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>ユーザーが代理呼び出しを使用して、他のユーザーの代わりに通話に応答したり、電話をかけたりできます。たとえば、代理呼び出しによって、マネージャーは、すべての着信が自分と秘書の両方の電話に着信するよう設定することができます。このパラメーターを True に設定すると、このポリシーの対象ユーザーは代理呼び出しを設定できます。このパラメーターを False に設定すると、代理呼び出しが無効となります。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>悪意のある呼び出しのトレースは、悪意があると指定した呼び出しをトレースするための標準機能です。このような呼び出しは発信者 ID がブロックされていてもトレースできます。トレースを使用できるのは適切な機関のみであり、ユーザーは使用できません。このプロパティを True に設定すると、悪意のある呼び出しのトレース設定が有効となります。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>チーム呼び出しを使用すると、あるユーザーの番号の呼び出し時に着信するユーザーのグループを指定できます。この機能は、顧客からの着信に対してチームの全員が応答できるようにする場合などに便利です。このパラメーターを True に設定すると、この機能が有効となります。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、応答のないモバイル デバイスへの通話は、モバイル デバイス プロバイダーのボイスメールではなく、組織のボイスメールにルーティングされます。着信応答が &quot;あまりにも早い&quot; 場合 (すなわち、PSTNVoicemailEscapeTimer プロパティに設定された値が経過する前に応答した場合)、モバイル デバイスは応答不可であると判断し、通話は組織のボイスメールにルーティングされます。</p>
<p>既定値は False です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsIdentity</p></td>
<td><p>ポリシーのスコープ (および場合によっては名前) を指定する一意の識別子です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>VoicePolicy</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。 このオブジェクトは VoicePolicy 型である必要があり、<strong>Get-CsVoicePolicy</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このポリシーを説明するフレンドリ名です。</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>PSTN 料は、一般に長距離通話料として知られています。ブランチ オフィス間でネットワーク経由の通話が可能なボイス オーバー IP (VoIP) を導入して、この料金がかからないようにしている組織もあります。このパラメーターを True に設定すると、無料のネットワーク経由でなく、有料の PSTN 経由で呼び出しが行われます。</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>このポリシーで使用できる PSTN 使用法の一覧です。PSTN 使用法によって音声ポリシーと電話ルートを関連付けます。</p>
<p>この一覧には任意の文字列値を指定できますが、その値が現在の PSTN 使用法のグローバル一覧に存在している必要があります (重複する文字列は許可されません。すべての文字列は一意である必要があります)。PSTN 使用法の一覧は、<strong>Get-CsPstnUsage</strong> コマンドレットを呼び出すことで取得できます。</p>
<p>このパラメーターを使用してすべての PSTN 使用法をポリシーから削除する場合は、このポリシーが付与されているユーザーが PSTN 通話を発信できなくなる点に留意してください。</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int64</p></td>
<td><p>ある通話への応答が &quot;すぐに&quot; 行われたかどうかを判断するために使用される時間 (ミリ秒) です。この時間内に応答を受け取った場合、Lync Server はモバイル デバイスが使用できない状態にあると見なし、組織のボイスメールへの通話に自動的に切り替えます。この時間に達するまでに応答が一切行われなかった場合は、通話を続行できます。</p>
<p>既定値は 1,500 ミリ秒です。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>省略可能</p></td>
<td><p>Guid</p></td>
<td><p>音声ポリシーが変更される Skype for Business Online テナント アカウントのグローバル一意識別子 (GUID) です。次に例を示します。</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を返すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceDeploymentMode</em></p></td>
<td><p>省略可能</p></td>
<td><p>VoiceDeploymentMode</p></td>
<td><p>有効な値は次のとおりです。</p>
<p>* OnPrem</p>
<p>* Online</p>
<p>* OnlineBasic</p>
<p>* OnPremOnlineHybrid</p>
<p>既定値は OnPrem です。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy オブジェクト。音声ポリシー オブジェクトのパイプ処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットは、値またはオブジェクトを戻しません。代わりに、Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy オブジェクトのインスタンスを構成します。

## 関連項目

#### その他のリソース

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

