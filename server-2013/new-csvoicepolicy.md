---
title: New-CsVoicePolicy
TOCTitle: New-CsVoicePolicy
ms:assetid: 3852de89-a604-437a-9fdf-3597b88ce13d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425856(v=OCS.15)
ms:contentKeyID: 48271769
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoicePolicy

 

_**トピックの最終更新日:** 2015-03-09_

新しい音声ポリシーを作成します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsVoicePolicy -Identity <XdsIdentity> [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、Identity を UserVoicePolicy1 にして、ユーザーごとの新しい音声ポリシーを (既定の設定で) 作成します。

    New-CsVoicePolicy -Identity UserVoicePolicy1

## 例 2

この例では、Identity を UserVoicePolicy2 にしてユーザーごとの新しい音声ポリシーを作成し、AllowSimulRing プロパティを False に設定します。この設定により、このポリシーが割り当てられるすべてのユーザーで、同時呼び出し (会社の電話への着信時に毎回携帯電話などの 2 番目の電話を呼び出すかどうかを決定する機能) は有効にはなりません。このコマンドにより PSTN 使用法の一覧に "Local" も追加され、これによりこの音声ポリシーは Local PSTN 使用法も使用するボイス ルートと関連付けられます (Identity パラメーターが明示的に指定されていないことに注意してください。Identity パラメーターは位置パラメーターであるため、最初に ID 値をパラメーター一覧の最初に設定しておけば、それが ID であるということを明示する必要はありません)。

    New-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{add = "Local"}

## 例 3

この例では、Redmond サイトの新しい音声ポリシーを作成し、組織で定義されているすべての PSTN 使用法をこのポリシーに適用します。この例の 1 行目では、**Get-CsPstnUsage** コマンドレットを呼び出して組織の PSTN 使用法のグローバル セットを取得し、それを変数 $a に格納します。2 行目では、**New-CsVoicePolicy** コマンドレットを呼び出して Redmond サイトの新しい音声ポリシーを作成します。値が PstnUsages パラメーターに渡され、PSTN 使用法のグローバル セットに含まれている一覧がこのポリシーに追加されます。追加する値の構文は $a.Usage です。この構文を使用して、(PSTN 使用法の一覧が含まれた) PSTN 使用法の設定の Usage プロパティを参照しています。

    $a = Get-CsPstnUsage
    New-CsVoicePolicy site:Redmond -PstnUsages @{add = $a.Usage}

## 解説

このコマンドレットは、新しい音声ポリシーを作成します。音声ポリシーは、同時呼び出し (会社の電話への着信時に 2 番目の電話を呼び出す機能) や自動転送などの、エンタープライズ VoIP 関連機能の管理に使用されます。このコマンドレットで作成したポリシーによって、これらの機能の多くを有効にするか無効にするかが決定されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**New-CsVoicePolicy** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoicePolicy"}

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
<td><p>ポリシーのスコープまたは名前を指定する一意の識別子。このコマンドレットの有効な値は、site:&lt;サイト名&gt; (&lt;サイト名&gt; は、このポリシーが割り当てられる Lync Server サイトの名前 (site:Redmond など))、および RedmondVoicePolicy などのユーザーごとのポリシーを指定する文字列です。グローバル ポリシーは既定で存在します。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターが True に設定されていると、呼び出しを転送できます。このパラメーターが False に設定されていると、呼び出しを転送できません。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターが True に設定されていると、別のプールに所属する内部番号に呼び出しがあった際にそのプールまたは WAN を使用できない場合、公衆交換電話網 (PSTN) 経由でルーティングします。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>同時呼び出しは、1 つの番号がダイヤルされた際に複数の電話を呼び出せるようにする機能です。このパラメーターを True に設定すると、この機能が有効となります。このパラメーターが False に設定されていると、このポリシーが割り当てられているユーザーに同時呼び出しを構成することはできません。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>省略可能</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>管理者が着信の転送および同時呼び出しを管理する方法を提供します。有効な値は次のとおりです。</p>
<p>* VoicePolicyUsage - 既定の音声ポリシー使用法を使って、すべての通話に対する着信の転送および同時呼び出しを管理します。これは既定の値です。</p>
<p>* InternalOnly - 着信の転送および同時呼び出しは、1 人の Lync ユーザーから他の 1 人にかけた通話に限定されます。</p>
<p>* CustomUsage - カスタムの PSTN 使用法を使って、着信の転送および同時呼び出しを管理します。この使用法は、CustomCallForwardingSimulRingUsages パラメーターを使用して指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>着信の転送および同時呼び出しの管理に使用するカスタムの PSTN 使用法です。音声ポリシーにカスタムの使用法を追加するには、次のような構文を使用します。</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>カスタムの使用法を削除するには、次の構文を使用します。</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>CustomCallForwardingSimulRingUsages パラメーターで使用する前に、その使用法が存在している必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>音声ポリシーの説明。</p>
<p>最大長: 1040 文字</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>帯域幅の制限などのネットワーク構成を管理するために設定できるポリシー。このパラメーターを True に設定すると、これらのポリシーが優先されます。つまり、このパラメーターを True に設定すると帯域幅の確認は行われず、呼び出しは通話受付管理 (CAC) 設定に関係なく処理されます。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallPark</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>コール パーク アプリケーション を使用すると、一定範囲内の特定の番号で呼び出しを保留 (パーク) しておき、後で受けることができます。このパラメーターを True に設定すると、適用が有効になります。このパラメーターを False に設定すると、このポリシーに割り当てられているユーザーは、自分の電話番号への呼び出しを保留することができません。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>呼び出しを別の番号に転送できるかどうかを決定します。このパラメーターを True に設定すると呼び出しを転送することができ、False に設定すると転送することができません。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDelegation</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>代理呼び出しにより、ユーザーは別のユーザーの呼び出しに応答したり、他のユーザーに代わって呼び出しを行ったりすることができます。たとえば、代理呼び出しによって、マネージャーは、すべての着信が自分と管理者の両方の電話に着信するよう設定することができます。このパラメーターを True に設定すると、このポリシーの対象ユーザーは代理呼び出しを設定できます。このパラメーターを False に設定すると、代理呼び出しが無効となります。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>悪意のある呼び出しのトレースは、悪意があると指定された呼び出しをトレースするための標準機能です。このような呼び出しは発信者 ID がブロックされていてもトレースできます。トレースを使用できるのは適切な機関のみであり、ユーザーは使用できません。このプロパティを True に設定すると、悪意のある呼び出しのトレース設定が有効となります。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>チーム呼び出しを使用すると、あるユーザーの番号の呼び出し時に着信するユーザーのグループを指定できます。この機能は、顧客からの着信に対してチームの全員が応答できるようにする場合などに便利です。このパラメーターを True に設定すると、この機能が有効となります。</p>
<p>既定値は次のとおりです。True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、応答のないモバイル デバイスへの通話は、モバイル デバイス プロバイダーのボイスメールではなく、組織のボイスメールにルーティングされます。着信応答が &quot;あまりにも早い&quot; 場合 (すなわち、PSTNVoicemailEscapeTimer プロパティに設定された値が経過する前に応答した場合)、モバイル デバイスは応答不可であると判断し、通話は組織のボイスメールにルーティングされます。</p>
<p>既定値は False です。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>永続的な変更としてオブジェクトをコミットせずに、オブジェクト参照を作成します。このパラメーターを指定して呼び出したコマンドレットの出力を変数に割り当てる場合、オブジェクト参照のプロパティを変更し、コマンドレットに対応する Set- コマンドレットを呼び出してそれらの変更をコミットできます。</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このポリシーを説明する表示可能な名前。</p>
<p>既定値は次のとおりです。DefaultPolicy</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>PSTN 料は、一般に長距離通話料として知られています。支店間でネットワークを使用して通話ができるボイス オーバー IP (VoIP) ソリューションを導入し、この料金がかからないようにしている組織もあります。このパラメーターを True に設定すると、料金がかからないネットワーク経由でなく、有料の PSTN 経由で呼び出しが行われます。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>このポリシーで使用できる PSTN 使用法の一覧。PSTN 使用法によって音声ポリシーと電話ルートを関連付けます。</p>
<p>値が現在の PSTN 使用法のグローバル一覧に含まれている限り、任意の文字列値をこの一覧に含めることができます (重複する文字列は使用できません。すべての文字列は一意である必要があります)。PSTN 使用法の一覧は、<strong>Get-CsPstnUsage</strong> コマンドレットを呼び出すことによって取得できます。</p>
<p>既定では、この一覧は空です。このパラメーターの値を指定しないと、このポリシーが適用されるユーザーは発信の PSTN 通話を行うことができなくなることを示す警告メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int64</p></td>
<td><p>着信応答が &quot;あまりにも早い&quot; かどうかの判断に使われる時間 (ミリ秒)。この時間内に着信応答があると、Lync Server はモバイル デバイスが応答不可であると判断し、通話を自動的に組織のボイスメールに切り替えます。この時間が経過するまで着信応答がなければ、通話はそのまま処理されます。既定値は 1500 ミリ秒です。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>省略可能</p></td>
<td><p>Guid</p></td>
<td><p>新しい音声ポリシーが作成される Skype for Business Online テナント アカウントのグローバル一意識別子 (GUID)。次に例を示します。</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を戻すことができます。</p>
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

なし。

## 戻り値の種類

このコマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy オブジェクトの 1 つのインスタンスが作成されます。

## 関連項目

#### その他のリソース

[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

