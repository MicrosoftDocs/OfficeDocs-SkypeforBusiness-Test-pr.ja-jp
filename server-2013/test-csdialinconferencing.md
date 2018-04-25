---
title: Test-CsDialInConferencing
TOCTitle: Test-CsDialInConferencing
ms:assetid: e4aedf4f-77ac-4c8b-9613-07f8ea12c041
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg399013(v=OCS.15)
ms:contentKeyID: 48273866
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialInConferencing

 

_**トピックの最終更新日:** 2015-03-09_

**Test-CsDialInConferencing** コマンドレットは、ユーザーがダイヤルイン会議のセッションに参加できるかどうかを確認します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsDialInConferencing -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetPstnPhoneNumber <String>] [-UserSipAddress <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetPstnPhoneNumber <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 例

## 例 1

例 1 では、あらかじめ構成されたテスト ユーザーがプール atl-cs-001.litwareinc.com 上のダイヤルイン会議に参加できることを確認しています。このコマンドは、テスト ユーザーがプール atl-cs-001.litwareinc.com 用に定義されている場合にのみ機能します。そうしたテスト ユーザーが定義されている場合、このコマンドは最初のテスト ユーザーが Lync Server にログオンできるかどうかを判断します。

テスト ユーザーが定義されていない場合、どのユーザーとしてログオンするかを認識できないため、コマンドは失敗します。テスト ユーザーをプール用に定義していない場合は、UserCredential パラメーターを使用し、コマンドがログオンを試行する際に使用するユーザーの資格情報を指定する必要があります。

    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com 

## 例 2

例 2 に示すコマンドは、特定のユーザー (litwareinc\\pilar) がプール atl-cs-001.litwareinc.com のダイヤルイン会議に参加できるかどうかをテストします。そのために、この例の最初のコマンドでは、**Get-Credential** コマンドレットを使用して、Pilar Ackerman というユーザーの名前とパスワードが含まれる Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 litwareinc\\pilar がパラメーターとして指定されているので、管理者は \[Windows PowerShell 資格情報の要求\] ダイアログ ボックスに Pilar Ackerman のアカウントのパスワードを入力するだけで済みます)。結果として得られた資格情報オブジェクトは、$cred1 という名前の変数に格納されます。

次に 2 つ目のコマンドでは、ユーザー Pilar Ackerman が atl-cs-001.litwareinc.com プールにログオンしてダイヤルイン会議に参加できるか確認しています。このタスクを実行するため、**Test-CsDialInConferencing** コマンドレットに 3 つのパラメーター TargetFqdn (レジストラー プールの FQDN)、UserCredential (Pilar Ackerman のユーザー資格情報が含まれる Windows PowerShell オブジェクト)、および UserSipAddress (指定したユーザー資格情報に対応する SIP アドレス) を付けて呼び出します。

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:pilar@litwareinc.com" -UserCredential $cred1

## 解説

**Test-CsDialInConferencing** コマンドレットは、Lync Server の "代理トランザクション" の一例です。代理トランザクションは、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信など、一般的なタスクをユーザーが正常に完了できることを検証するために、Lync Server で使用されます。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) のようなアプリケーションによって自動的に実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、**CsHealthMonitoringConfiguration** コマンドレットを使用して、自組織のレジストラー プールのそれぞれに対してテスト ユーザーを設定します。これらのテスト ユーザーとは、代理トランザクションでの使用を目的としてあらかじめ構成されている 1 組のユーザーのことです (通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません)。プールに対して構成されたテスト ユーザーを使用すると、管理者がテスト用にユーザー アカウント ID を指定したり資格情報を入力したりしなくても、そのプールに対して簡単に代理トランザクションを実行できます。

管理者は、実際のユーザー アカウントを使用して代理トランザクションを実行することもできます。たとえば、2 人のユーザーがインスタント メッセージを交換できない場合、管理者は、問題のある 2 人のユーザー アカウント (2 つのテスト アカウントではなく) を使用して代理トランザクションを実行し、問題の診断と解決を試みることができます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーのログオン名とパスワードを入力する必要があります。

**Test-CsDialInConferencing** コマンドレットは、テスト ユーザーのシステム ログオンの試行によって機能します (テスト ユーザーを使用している場合、**Test-CsDialInConferencing** コマンドレットはそのプール用に構成された最初のテスト アカウントを使用します)。ログオンが成功すると、コマンドレットはそのユーザーの資格情報とアクセス許可を使用して、利用可能なダイヤルイン会議のアクセス番号を試行します。各ダイヤルインの試行の成否が記録された後、テスト ユーザーが Lync Server からログオフされます。

**Test-CsDialInConferencing** コマンドレットは適切に接続できることの確認のみを行います。コマンドレットによって実際に発信が行われることはありません。また、他のユーザーが参加可能なダイヤルイン会議が作成されることもありません。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーは **Test-CsDialInConferencing** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialInConferencing"}

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
<td><p><em>TargetFqdn</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>テスト対象プールの完全修飾ドメイン名 (FQDN) です。</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>必須</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>テストするユーザー アカウントのユーザー資格情報オブジェクトです。UserCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得されるオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\kenmyer というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $x という名前の変数に格納します。</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。状態監視構成設定を使用してテストを実行している場合は、このパラメーターは必要ありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.SyntheticTransactions.SipSyntheticTransaction+AuthenticationMechanism</p></td>
<td><p>テストで使用される認証の種類。有効な値は次のとおりです。</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。この変数には、出力を HTML あるいは XML ファイルに保存する目的で使用する ToHTML と ToXML のペアのメソッドが含まれます。</p>
<p>出力を $TestOutput という名前のロガー変数に格納するには、次の構文を使用します。</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注: 変数名の指定時には、先頭に $ 文字を付けないでください。ロガー変数に格納された情報を HTML ファイルに保存するには、次のようなコマンドを使用します。</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>ロガー変数に格納された情報を XML ファイルに保存するには、次のようなコマンドを使用します。</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。たとえば、$TestOutput という名前の変数に出力を保存するには、次の構文を使用します。</p>
<p>-OutVerboseVariable TestOutput</p>
<p>変数名を指定するときは、先頭に $ 記号を使用しないでください。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Int32</p></td>
<td><p>レジストラー サービスが使用する SIP ポートです。レジストラーが既定のポート 5061 を使用する場合、このパラメーターは必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>PSTN ユーザーがダイヤルイン会議に参加できることを確認するために使用される PSTN 電話の電話番号です。次に例を示します。</p>
<p>-TargetPstnPhoneNumber &quot;+12065551219&quot;</p>
<p>TargetPstnPhoneNumber は、VerifyConferenceJoinType パラメーターを使用するときにのみ指定する必要があることに注意してください。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>テストするユーザー アカウントの SIP アドレスです。次に例を示します。-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。UserSipAddress パラメーターは、UserCredential と同じユーザー アカウントを参照している必要があります。状態監視構成設定を使用してテストを実行している場合は、このパラメーターは必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>VerifyConferenceJoin</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Boolean</p></td>
<td><p>True に設定すると、PSTN 電話を使用してダイヤルイン会議に参加できることを確認します。このテストを実行するときは、必要に応じて TargetPstnPhoneNumber を含めることができます。含める場合、TargetPstnPhoneNumber では、会議に参加するときに使用する PSTN 電話を指定する必要があります。TargetPstnPhoneNumber を指定しないと、<strong>Test-CsDialInConferencing</strong> コマンドレットは、適切なダイヤルイン会議の地域に事前に割り当てられているダイヤルイン電話番号を使用します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsDialInConferencing** コマンドレットはパイプライン入力を受け入れません。

## 戻り値の種類

**Test-CsDialInConferencing** コマンドレットを実行すると、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Test-CsAVConference](test-csavconference.md)

