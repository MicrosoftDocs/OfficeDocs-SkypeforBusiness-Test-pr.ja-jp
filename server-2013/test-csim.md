---
title: Test-CsIM
TOCTitle: Test-CsIM
ms:assetid: 2fdab54c-5ec4-4db5-b29c-a3efaae68f66
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425802(v=OCS.15)
ms:contentKeyID: 48271637
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsIM

 

_**トピックの最終更新日:** 2015-03-09_

2 人のユーザーがインスタント メッセージを交換できるかどうかをテストします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-EmailHost <String>] [-Force <SwitchParameter>] [-IsSsl <$true | $false>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Password <String>] [-Port <UInt16>] [-TestLegalIntercept <SwitchParameter>] [-Username <String>] [-WaitSeconds <Int16>]

## 例

## 例 1

例 1 では、事前構成されたテスト ユーザーのペアが atl-cs-001.litwareinc.com プールにログオンしてインスタント メッセージを交換できるかどうかが確認されます。このコマンドが有効なのは、テスト ユーザーが atl-cs-001.litwareinc.com プール用に定義されている場合だけです。定義されている場合は、このコマンドにより、2 人のユーザーがシステムにログオンできるかどうか、ログオンできる場合はインスタント メッセージを交換できるかどうかを判断します。

テスト ユーザーが定義されていない場合、テスト実行中に使用するユーザーを認識できないため、コマンドは失敗します。プールにレジストラーを定義していない場合は、SenderSipAddress パラメーターと ReceiverSipAddress パラメーター、および IM セッションに関与しているユーザーに対応する資格情報を指定する必要があります。次に **Test-CsIM** コマンドレットは、2 人の指定されたユーザーを使用してチェックを実行します。

    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com

## 例 2

例 2 のコマンドでは、ユーザーのペア (litwareinc\\pilar および litwareinc\\kenmyer) が Lync Server にログオンしてインスタント メッセージを交換できるかどうかがテストされます。これを行うために、最初のコマンド例で **Get-Credential** コマンドレットを使用して、Pilar Ackerman というユーザーの名前とパスワードを含む、Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 (litwareinc\\pilar) はパラメーターとして指定されているため、管理者は、\[Windows PowerShell 資格情報の要求\] ダイアログ ボックスに Pilar Ackerman のアカウントのパスワードを入力するだけです)。作成された資格情報オブジェクトは、$cred1 という名前の変数に格納されます。2 番目のコマンドも同じことをしますが、このときは、Ken Myer というアカウントの資格情報オブジェクトを戻します。

取得した 2 つの資格情報オブジェクトを使用して、例の 3 番目のコマンドで、2 人のユーザーが Lync Server にログオンしてインスタント メッセージを交換できるかどうかを判断します。これを行うため、次のパラメーターを指定して **Test-CsIM** コマンドレットを呼び出します。TargetFqdn (レジストラー プールの FQDN)、SenderSipAddress (最初のテスト ユーザーの SIP アドレス)、SenderCredential (このユーザーの資格情報を含む Windows PowerShell オブジェクト)、-ReceiverSipAddress (他のテスト ユーザーの SIP アドレス)、および ReceiverCredential (他のユーザーの資格情報を含む Windows PowerShell オブジェクト)。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## 解説

**Test-CsIM** コマンドレットは、Lync Server "代理トランザクション" の一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信などの一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) などのアプリケーションから自動で実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、**CsHealthMonitoringConfiguration** コマンドレットを使用して、テスト ユーザーを各レジストラー プールに設定します。これらのテスト ユーザーとは、代理トランザクションでの使用を目的としてあらかじめ構成されている 1 組のユーザーのことです (通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません)。プールに構成されたテスト ユーザーを使用すると、管理者がテスト用にユーザー アカウント ID を指定したり資格情報を入力したりしなくても、そのプールに対して簡単に代理トランザクションを実行できます。

管理者は、実際のユーザー アカウントを使用して代理トランザクションを実行することもできます。たとえば、2 人のユーザーがインスタント メッセージを交換できない場合、管理者は (テスト アカウントのペアではなく) 問題の 2 人のユーザー アカウントを使用して代理トランザクションを実行し、問題を診断して解決しようと試みます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーの資格情報を入力する必要があります。

**Test-CsIM** コマンドレットは、まず、1 組のテスト ユーザーを Lync Server にログオンさせることから開始します。2 人のログオンが成功すると、コマンドレットは次に、2 人のテスト ユーザー間でインスタント メッセージング (IM) セッションを開始します (ユーザー 1 がユーザー 2 を IM セッションに招待し、ユーザー 2 がその招待を受け入れます)。2 人のユーザーの間でメッセージを交換できることが確認されると、**Test-CsIM** コマンドレットは IM セッションを終了し、両方のユーザーをシステムからログオフします。

このコマンドレットを実行できるユーザー: このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsIM"}

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
<td><p>必須</p></td>
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
<td><p><em>EmailHost</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>Legal Intercept テストで使用するユーザーの電子メール ホスト。次に例を示します。</p>
<p>-EmailHost &quot;litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>IsSsl</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>True に設定されている場合、Secure Socket Layer (SSL) プロトコルを使用してテストを実行することを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。この変数には、出力を HTML あるいは XML ファイルに保存する目的で使用する ToHTML と ToXML のペアのメソッドが含まれます。</p>
<p>$TestOutput という名前のロガー変数の出力を保存するには、以下の構文を使用します。</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注: 変数名を指定するときは、先頭に $ 文字を付けないでください。ロガー変数に格納された情報を HTML ファイルに保存するには、次のようなコマンドを使用します。</p>
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
<td><p><em>Password</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>Legal Intercept テストで使用するユーザーのパスワード。</p></td>
</tr>
<tr class="odd">
<td><p><em>Port</em></p></td>
<td><p>省略可能</p></td>
<td><p>UInt16</p></td>
<td><p>Legal Intercept サービスに使用するポート。</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、最初のユーザーの SIP アドレス。次に例を示します。-ReceiverSipAddress &quot;sip:jhaas@litwareinc.com&quot;。ReceiverSipAddress パラメーターが ReceiverCredential と同じユーザー アカウントを参照している必要があります。</p>
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
<td><p><em>TestLegalIntercept</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>指定されている場合、Test-CsIM は、指定したユーザーの Legal Intercept サービスをテストします。</p></td>
</tr>
<tr class="even">
<td><p><em>Username</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>Legal Intercept テストで使用するユーザーのユーザー名。</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitSeconds</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int16</p></td>
<td><p>Legal Intercept サービスの応答をシステムが待機する時間 (秒) を指定します。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsIM** コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

**Test-CsIM** コマンドレットは、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Test-CsGroupIM](test-csgroupim.md)

