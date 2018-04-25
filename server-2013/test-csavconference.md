---
title: Test-CsAVConference
TOCTitle: Test-CsAVConference
ms:assetid: a1492563-9a97-44ac-b19a-8d5972cdd062
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412749(v=OCS.15)
ms:contentKeyID: 48273087
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAVConference

 

_**トピックの最終更新日:** 2015-03-09_

1 組のユーザーが音声ビデオ (A/V) 会議に参加できるかどうかをテストします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsAVConference -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAVConference -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsAVConference [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## 例

## 例 1

例 1 では、1 組の構成済みテスト ユーザーがプール atl-cs-001.litwareinc.com にログオンし、A/V 会議に参加できるかどうかをチェックします。このコマンドは、プール atl-cs-001.litwareinc.com のテスト ユーザーが定義されている場合のみ機能します。テスト ユーザーが定義されている場合、2 人のユーザーがシステムにログオンできるかどうかを判定します。ログオンできる場合、最初のテスト ユーザーは A/V 会議を作成し、2 番目のユーザーが参加するように招待します。その後、コマンドレットによって、2 人のテスト ユーザーが正常に接続を確立できたかどうかが検証されます。

テスト ユーザーが定義されていない場合、テスト中に使用するユーザーが不明であるため、コマンドはエラーになります。テスト ユーザーをプールに定義していない場合は、SenderSipAddress パラメーターと ReceiverSipAddress パラメーターのほかに、インスタント メッセージの交換に使用するユーザーに対応する資格情報を指定する必要があります。**Test-CsAVConference** コマンドレットは、指定された 2 人のユーザーを使用してチェックを実施します。

    Test-CsAVConference -TargetFqdn atl-cs-001.litwareinc.com 

## 例 2

例 2 に示すコマンドは、1 組のユーザー (litwareinc\\pilar および litwareinc\\kenmyer) が、Lync Server にログオンして A/V 会議に参加できるかどうかをテストします。これを行うため、この例の最初のコマンドでは **Get-Credential** コマンドレットを使用して、ユーザー Pilar Ackerman の名前とパスワードを格納している Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 litwareinc\\pilar はパラメーターとして指定されているため、管理者は \[Windows PowerShell 資格情報の要求\] ダイアログ ボックスで、Pilar Ackerman アカウントのパスワードのみ入力する必要があります)。作成された資格情報オブジェクトは、$cred1 という名前の変数に格納されます。2 番目のコマンドも同じことをしますが、このときは、Ken Myer というアカウントの資格情報オブジェクトを戻します。

準備した 2 つの資格情報オブジェクトを使用して、この例の 3 番目のコマンドでは、2 人のユーザーが Lync Server にログオンして A/V 会議に参加できるかどうかを確認します。このタスクを実行するため、**Test-CsAVConference** コマンドレットに次のパラメーターを指定して呼び出します。TargetFqdn (レジストラー プールの FQDN)、SenderSipAddress (1 人目のテスト ユーザーの SIP アドレス)、SenderCredential (この同じユーザーの資格情報を格納している Windows PowerShell オブジェクト)、ReceiverSipAddress (もう 1 人のテスト ユーザーの SIP アドレス)、および ReceiverCredential (もう 1 人のユーザーの資格情報を格納している Windows PowerShell オブジェクト) です。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAVConference -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## 解説

**Test-CsAVConference** コマンドレットは、"代理トランザクション" の一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信などの一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) などのアプリケーションから自動で実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、**CsHealthMonitoringConfiguration** コマンドレットを使用して、テスト ユーザーを各レジストラー プールに設定します。このテスト ユーザーは、代理トランザクションで使用するためにあらかじめ構成されている 1 組のユーザーです (通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません)。プールに構成されているテスト ユーザーを使って、管理者はテスト用にユーザー アカウントの ID を指定したり資格情報を入力したりしなくても、そのプールに対して代理トランザクションを実行することができます。

また、管理者は実際のユーザー アカウントを使用して、代理トランザクションを実行することもできます。たとえば、ある 2 人のユーザーがインスタント メッセージの交換を行うことができない場合に、管理者は (テスト アカウントではなく) その 2 つのユーザー アカウントを使って代理トランザクションを実行し、問題の診断と解決を試みることができます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーのログオン名とパスワードを入力する必要があります。

**Test-CsAVConference** コマンドレットは、2 人のテスト ユーザーが A/V 会議に参加できるかどうかをチェックします。このコマンドを実行すると、2 人のユーザーはシステムにログオンします。正常にログオンした後、最初のユーザーは A/V 会議を作成し、その会議に 2 番目のユーザーが参加するのを待ちます。短時間にわたってデータを交換した後、会議は削除され、2 人のテスト ユーザーはログオフします。

**Test-CsAVConference** コマンドレットは、2 人のテスト ユーザー間の実際の A/V 会議を実施するのではなく、A/V 会議を実施するために必要な接続を 2 人のユーザーが確立できるかどうかの検証を行います。

このコマンドレットを実行できるユーザー: このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAVConference"}

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
<td><p>テスト対象の 2 ユーザー アカウントのうち、最初のユーザーの資格情報オブジェクト。ReceiverCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得したオブジェクト参照である必要があります。たとえば、次のコードではユーザー litwareinc\pilar の資格情報オブジェクトを戻し、そのオブジェクトを $y という名前の変数に格納します。</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合は、受信者の資格情報は必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>必須</p></td>
<td><p>PSCredential</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、2 番目のユーザーの資格情報オブジェクト。SenderCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得したオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\kenmyer というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $x という名前の変数に格納します。</p>
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
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
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
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。この変数には、出力を HTML あるいは XML ファイルに保存する目的で使用する ToHTML と ToXML のペアのメソッドが含まれます。</p>
<p>$TestOutput という名前のロガー変数に出力を保存するには、以下の構文を使用します。</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注: 変数名を指定するときは、先頭に $ 文字を付けないでください。ロガー変数に格納された情報を HTML ファイルに保存するには、以下のようなコマンドを使用します。</p>
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
<p>変数名を指定するときは、先頭に $ 記号を使用しないでください。</p></td>
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

なし。

## 戻り値の種類

**Test-CsAVConference** コマンドレットは、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[Test-CsDialInConferencing](test-csdialinconferencing.md)

