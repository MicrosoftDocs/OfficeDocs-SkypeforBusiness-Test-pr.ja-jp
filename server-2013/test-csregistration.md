---
title: Test-CsRegistration
TOCTitle: Test-CsRegistration
ms:assetid: 9e38cb36-c97a-43f2-97fe-64759f663be2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412737(v=OCS.15)
ms:contentKeyID: 48273042
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsRegistration

 

_**トピックの最終更新日:** 2015-03-09_

ユーザーが Lync Server にログオンできるかどうかをテストします。**Test-CsRegistration** コマンドレットは "代理トランザクション" です。一般的な Lync Server の処理をシミュレーションし、システムの状態やパフォーマンスを監視するために使用します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsRegistration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsRegistration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsRegistration [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 例

## 例 1

例 1 では、プール atl-cs-001.litwareinc.com のレジストラー サービスをテストしています。このコマンドは、プール atl-cs-001.litwareinc.com のテスト ユーザーが定義されている場合のみ機能します。テスト ユーザーが定義されている場合、最初のテスト ユーザーが Lync Server にログオンできるかどうかが判定されます。

テスト ユーザーが定義されていない場合、どのユーザーとしてログオンするかコマンドが認識できないため、エラーになります。テスト ユーザーをプールに定義していない場合は、UserSipAddress パラメーターを指定し、コマンドがログオンを試行する際に使用する、ユーザー資格情報を指定する必要があります。

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com 

## 例 2

例 2 に示すコマンドでは、特定のユーザー (litwareinc\\pilar) が Lync Server にログオンできるかどうかをテストしています。これを行うため、この例の最初のコマンドでは **Get-Credential** コマンドレットを使用して、ユーザー Pilar Ackerman の名前とパスワードを格納している Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 litwareinc\\pilar はパラメーターとして指定されているため、管理者は \[Windows PowerShell 資格情報の要求\] ダイアログ ボックスで、Pilar Ackerman アカウントのパスワードのみ入力する必要があります)。作成された資格情報オブジェクトは、$cred1 という名前の変数に格納されます。

次に、2 番目のコマンドでは、このユーザーがプール atl-cs-001.litwareinc.com にログオンできるかどうかをチェックします。このタスクを実行するため、**Test-CsRegistration** コマンドレットに 3 つのパラメーター TargetFqdn (レジストラー プールの FQDN)、UserCredential (Pilar Ackerman のユーザー資格情報を格納している Windows PowerShell オブジェクト)、UserSipAddress (指定したユーザー資格情報に対応する SIP アドレス) を指定して呼び出しています。

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:pilar@litwareinc.com"

## 解説

**Test-CsRegistration** コマンドレットは、Lync Server の "代理トランザクション" の一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信などの一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) などのアプリケーションから自動で実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、CsHealthMonitoringConfiguration コマンドレットを使用して、テスト ユーザーを各レジストラー プールに設定します。このテスト ユーザーは、代理トランザクションで使用するためにあらかじめ構成されている 1 組のユーザーです (通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません)。プールに構成されているテスト ユーザーを使って、管理者はテスト用にユーザー アカウントの ID を指定したり資格情報を入力したりしなくても、そのプールに対して代理トランザクションを簡単に実行することができます。

管理者は、実際のユーザー アカウントを使用して代理トランザクションを実行することもできます。たとえば、2 人のユーザーがインスタント メッセージを交換できない場合、2 つのテスト アカウントではなく、問題の 2 つのユーザー アカウントを使用して代理トランザクションを実行し、問題の診断と解決を試みることができます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーのログオン名とパスワードを入力する必要があります。

**Test-CsRegistration** コマンドレットでは、組織内のユーザーが Lync Server にログオンできるかどうかを検証できます。**Test-CsRegistration** コマンドレットでこのチェックを実行するには、テスト アカウントが 1 つ必要です。テストを実行するプールにテスト ユーザーを設定した場合、アカウントを指定する必要はありません。**Test-CsRegistration** コマンドレットは代わりに、そのプールに割り当てられている最初のテスト アカウントを自動的に使用します (詳細については、[New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md) コマンドレットのヘルプ トピックを参照してください)。または、プールに割り当てられていないアカウントを使用して、テストを実行することもできます。この場合は、テスト ユーザーを構成していなくてもテストを実行できます。また、この方法では、特定のユーザーが Lync Server へログオンできるかどうかをテストできます (この方法でテストする場合、テストするアカウントのユーザー名およびパスワードを指定する必要があります)。

**Test-CsRegistration** コマンドレットを実行すると、テスト ユーザーによる Lync Server へのサインオンが試行されます。成功した場合、テスト ユーザーはシステムから切断されます。これはすべてユーザーの介入なしに行われ、実際のユーザーに影響を及ぼすこともありません。たとえば、テスト アカウント sip:kenmyer@litwareinc.com と同一の実際の Lync Server アカウントを持つユーザーが実在するとします。その場合、テストは実ユーザーの Ken Myer を停止させることなく実行されます。テスト アカウントの Ken Myer がシステムからログオフしても、実ユーザーの Ken Myer はログオンしたままになります。

Verbose パラメーターを指定すると、**Test-CsRegistration** コマンドレットがテストを完了するために行うすべての処理の詳しい説明を取得できます。

このコマンドレットを実行できるユーザー: このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsRegistration"}

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
<td><p>String</p></td>
<td><p>テスト対象プールの完全修飾ドメイン名 (FQDN) です。</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>必須かどうか</p></td>
<td><p>PSCredential</p></td>
<td><p>テストするアカウントのユーザー資格情報オブジェクトです。UserCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使って取得した、オブジェクト参照である必要があります。たとえば、次のコードは litwareinc\kenmyer というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを</p>
<p>$x という名前の変数に格納します。$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。プールの状態監視構成設定でテストを実行している場合は、このパラメーターは必要ありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>省略可能</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>テストで使用される認証の種類。有効な値は次のとおりです。</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
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
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。たとえば、$TestOutput という名前の変数に出力を保存するには、次の構文を使用します。</p>
<p>-OutVerboseVariable TestOutput</p>
<p>変数名を指定するときは、先頭に $ 記号は使用しないでください。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>レジストラー サービスが使用する SIP ポートです。レジストラーが既定のポート 5061 を使用する場合、このパラメーターは必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テストするユーザー アカウントの SIP アドレスです。次に例を示します。-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。UserSipAddress パラメーターは、UserCredential と同じユーザー アカウントを参照している必要があります。プールの状態監視構成設定でテストを実行している場合は、このパラメーターは必要ありません。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsRegistration** コマンドレットは、パイプ処理による入力を受け入れません。

## 戻り値の種類

**Test-CsRegistration** コマンドレットは、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスを戻します。

