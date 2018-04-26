---
title: Test-CsGroupIM
TOCTitle: Test-CsGroupIM
ms:assetid: 1e73fd7a-5727-4688-8d4c-a3107c3985e9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398273(v=OCS.15)
ms:contentKeyID: 48271459
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsGroupIM

 

_**トピックの最終更新日:** 2015-03-09_

2 人のユーザーがインスタント メッセージング (IM) 会議を開催できるかどうかをテストします。**Test-CsGroupIM** コマンドレットは "代理トランザクション" であり、状態とパフォーマンスを監視する目的で使用される、一般的な Lync Server アクティビティをシミュレーションするものです。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsGroupIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsGroupIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsGroupIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## 例

## 例 1

例 1 では、あらかじめ構成した 2 人のテスト ユーザーがプール atl-cs-001.litwareinc.com にログオンして、IM 会議に参加できるかどうかを確認します。このコマンドが有効なのは、テスト ユーザーが atl-cs-001.litwareinc.com プールに定義されている場合だけです。定義されている場合、コマンドを実行して、2 人のユーザーがシステムにログオンできるかどうかを確認し、次に、これらのユーザーがインスタント メッセージング会議に参加できるかどうかを確認します。

テスト ユーザーが定義されていない場合、テスト実行中に使用するユーザーを認識できないため、コマンドは失敗します。プールにテスト ユーザーを定義していない場合は、SenderSipAddress パラメーターと ReceiverSipAddress パラメーターを指定するとともに、インスタント メッセージング セッションに関係のあるユーザーの対応する資格情報を指定する必要があります。**Test-CsGroupIM** コマンドレットを実行し、指定した 2 人のユーザーを使用して確認を実行します。

    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com

## 例 2

例 2 のコマンドは、2 人のユーザー (litwareinc\\pilar と litwareinc\\kenmyer) が Lync Server にログオンして、インスタント メッセージング会議に参加できるかどうかをテストします。これを行うために、例の最初のコマンドで **Get-Credential** コマンドレットを使用して、Pilar Ackerman というユーザーの名前とパスワードを含む、Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 (litwareinc\\pilar) はパラメーターとして含まれているため、管理者は、表示された \[Windows PowerShell 資格情報の要求\] ダイアログ ボックスに Pilar Ackerman のアカウントのパスワードを入力するだけです)。作成された資格情報オブジェクトは、$cred1 という名前の変数に格納されます。2 番目のコマンドも同じことをしますが、このときは、Ken Myer というアカウントの資格情報オブジェクトを戻します。

手元にある 2 つの資格情報オブジェクトを使用して、例の 3 番目のコマンドを実行し、2 人のユーザーが Lync Server にログオンして、インスタント メッセージング会議に参加できるかどうかを確認します。このタスクを実行するには、**Test-CsGroupIM** コマンドレットを呼び出して次のパラメーターを指定します。TargetFqdn (レジストラー プールの FQDN )、SenderSipAddress (最初のユーザーの SIP アドレス)、SenderCredential (最初のユーザーのユーザー資格情報)、ReceiverSipAddress (2 番目のユーザーの SIP アドレス)、および ReceiverCredential (2 番目のユーザーのユーザー資格情報)。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## 解説

**Test-CsGroupIM** コマンドレットは、Lync Server の代理トランザクションの一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信などの一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) などのアプリケーションから自動で実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、**CsHealthMonitoringConfiguration** コマンドレットを使用して、テスト ユーザーを各レジストラー プールに設定します。これらのテスト ユーザーとは、代理トランザクションでの使用を目的としてあらかじめ構成されている 1 組のユーザーのことです (通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません)。プールに構成されたテスト ユーザーを使用すると、管理者がテスト用にユーザー アカウント ID を指定したり資格情報を入力したりしなくても、そのプールに対して簡単に代理トランザクションを実行できます。

管理者は、実際のユーザー アカウントを使用して代理トランザクションを実行することもできます。たとえば、2 人のユーザーがインスタント メッセージを交換できない場合、管理者は、問題のある 2 人のユーザー アカウント (2 つのテスト アカウントではなく) を使用して代理トランザクションを実行し、問題の診断と解決を試みることができます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーの資格情報を入力する必要があります。

**Test-CsGroupIM** コマンドレットを使用すると、組織内のユーザーが会議を開催できるかどうかを確認できます。**Test-CsGroupIM** コマンドレットでテストを実行するには、2 つのユーザー アカウントが必要です。テストを実行するプールにテスト ユーザーを設定している場合、これらのアカウントを指定する必要はありません。代わりに、**Test-CsGroupIM** コマンドレットを実行すると、プールに割り当てられているテスト アカウントが自動的に使用されます (詳細については、[New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md) コマンドレットのヘルプ トピックを参照してください)。または、レジストラーに割り当てられているアカウント以外のアカウントを使用して、テストを実行することもできます。これにより、プールにテスト ユーザーを構成していなくてもテストを実行することができます。また、特定の 2 人のユーザーが会議を開催できるかどうかをテストすることもできますこの方法を使用する場合、両方のユーザーのユーザー名とパスワードを入力する必要があります。

**Test-CsGroupIM** コマンドレットを実行すると、コマンドレットは、両方のテスト ユーザーを Lync Server にサインオンさせるよう試みます。成功すると、**Test-CsGroupIM** コマンドレットは、最初のテスト ユーザーを使用して新しい会議を作成し、2 番目のユーザーを会議に招待します。メッセージの交換後、両方のユーザーはシステムから切断されます。ユーザーによる操作なしに、また実際のユーザーに影響を及ぼすことなく、これらすべてが行われます。たとえば、テスト アカウント sip:kenmyer@litwareinc.com が実際の Lync Server アカウントの実ユーザーに対応するとします。この場合、テストは、実際の Ken Myer の業務を中断することなく実行されます。たとえば、Ken Myer のテスト アカウントがシステムからログオフした場合でも、Ken Myer 本人はログオン状態が保持されます。同様に、実際の Ken Myer は会議への招待を受け取りません。その招待は、テスト アカウントに対して送信されて、テスト アカウントによって承諾されます。

Verbose パラメーターを追加すると、テストを完了するために **Test-CsGroupIM** コマンドレットで実行されるすべてのアクションの詳細なアカウントを取得できます。

このコマンドレットを実行できるメンバー。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsGroupIM"}

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
<td><p><em>ReceiverCredential</em></p></td>
<td><p>必須</p></td>
<td><p>PSCredential</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、最初のユーザーの資格情報オブジェクト。ReceiverCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得されるオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\pilar というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $y という名前の変数に格納します。</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合は、受信者の資格情報は必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>必須</p></td>
<td><p>PSCredential</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、2 番目のユーザーの資格情報オブジェクト。SenderCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得されるオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\kenmyer というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $x という名前の変数に格納します。</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合は、送信者の資格情報は必要ありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必須かどうか</p></td>
<td><p>String</p></td>
<td><p>テスト対象プールの完全修飾ドメイン名 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>省略可能</p></td>
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
<td><p>テストで使用される認証の種類。有効な値は次のとおりです。</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。この変数には、出力を HTML または XML ファイルに保存する目的で使用する ToHTML と ToXML のペアのメソッドが含まれます。</p>
<p>$TestOutput という名前のロガー変数の出力を保存するには、以下の構文を使用します。</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注: 変数名を指定するときは、先頭に $ 文字を付けないでください。ロガー変数に格納された情報を HTML ファイルに保存するには、次のような構文を使用します。</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>ロガー変数に保存された情報を XML ファイルに保存するには、以下のようなコマンドを使用します。</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。たとえば、$TestOutput という名前の変数に出力を保存するには、次の構文を使用します。</p>
<p>-OutVerboseVariable TestOutput</p>
<p>変数名を指定するときは、先頭に $ 記号は使用しないでください。</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、最初のユーザーの SIP アドレス。次に例を示します。-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;。ReceiverSipAddress パラメーターが ReceiverCredential と同じユーザー アカウントを参照している必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合は、SIP アドレスは必要ありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>レジストラー サービスが使用する SIP ポート。レジストラーが既定のポート 5061 を使用する場合、このパラメーターは必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、2 番目のユーザーの SIP アドレス。次に例を示します。-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。SenderSipAddress パラメーターが SenderCredential と同じユーザー アカウントを参照している必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合は、SIP アドレスは必要ありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>このパラメーターが存在する場合、Join Launcher で音声ビデオ会議に参加できるかをテストします。Join Launcher を使うと、モバイル デバイスのユーザー (および、結果的には Mobility Service のユーザー) が会議に参加できるようになります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsGroupIM** コマンドレットは、パイプ処理された入力を受け入れません。

## 戻り値の種類

**Test-CsGroupIM** コマンドレットを実行すると、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトの 1 つのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Test-CsIM](test-csim.md)

