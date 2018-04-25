---
title: Test-CsPstnOutboundCall
TOCTitle: Test-CsPstnOutboundCall
ms:assetid: 12d940c3-8526-4c8f-8dc1-3fe65a3211bc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398207(v=OCS.15)
ms:contentKeyID: 48271323
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnOutboundCall

 

_**トピックの最終更新日:** 2015-03-09_

ユーザーが公衆交換電話網 (PSTN) に配置されている電話番号に電話をかけることができるかどうかをテストします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsPstnOutboundCall -TargetPstnPhoneNumber <String> -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall -TargetFqdn <String> -TargetPstnPhoneNumber <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 例

## 例 1

例 1 では、あらかじめ構成したテスト ユーザーがプール atl-cs-001.litwareinc.com にログオンして、PSTN ゲートウェイを使用して電話をかけることができるかどうかを確認しています。このコマンドが有効なのは、テスト ユーザーが atl-cs-001.litwareinc.com プール用に定義されている場合だけです。定義されている場合、コマンドを実行して、1 番目のテスト ユーザーがシステムにログオンできるかどうか、ログオンできる場合は、PSTN ネットワークに配置されている電話に電話をかけることができるかどうかを確認します。

テスト ユーザーが定義されていない場合、テスト実行中に使用するユーザーを認識できないため、コマンドは失敗します。プールにテスト ユーザーを定義していない場合、UserSipAddress パラメーターおよびテストに使用しているユーザー アカウントに対応する資格情報を指定する必要があります。**Test-CsPstnOutboundCall** コマンドレットを実行し、指定したユーザーを使用して確認を実行します。

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" 

## 例 2

例 2 のコマンドは、テスト ユーザー (litwareinc\\kenmyer) が Lync Server にログオンして、PSTN ゲートウェイを使用して電話をかけることができるかどうかをテストします。これを実行するには、例の最初のコマンドで **Get-Credential** コマンドレットを使用して、Ken Myer というユーザーの名前とパスワードを含む、Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 litwareinc\\kenmyer はパラメーターとして指定されているため、\[Windows PowerShell 資格情報の要求\] ダイアログ ボックスで管理者が入力する必要がある情報は、Ken Myer アカウントのパスワードだけです)。作成された資格情報オブジェクトは、$cred1 という名前の変数に格納されます。

手元にある資格情報オブジェクトを使用して、例の 2 番目のコマンドを実行し、テスト ユーザーが Lync Server にログオンして、通話先の電話番号 (+15551234567) に電話をかけることができるかどうかを確認します。このタスクを実行するには、**Test-CsPstnOutboundCall** コマンドレットを呼び出して次のパラメーターを指定します。TargetFqdn (レジストラー プールの FQDN)、UserSipAddress (電話をかけるユーザーの SIP アドレス)、UserCredential (テスト ユーザーの資格情報を格納する Windows PowerShell オブジェクト)、および TargetPstnPhoneNumber (電話する電話番号)。

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1

## 例 3

例 3 は、**Test-CsPstnOutboundCall** コマンドレットをサーバー プラットフォーム モードで使用する方法を示しています。このモードでは、ユーザーの SIP アドレスが指定されますが、ユーザー資格情報は含まれません。このように実行する場合、Lync Server は資格情報を使用してテスト ユーザーを認証します。

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress sip:kenmyer@litwareinc.com -TargetPstnPhoneNumber "+15551234567"

## 解説

**Test-CsPstnOutboundCall** コマンドレットは、Lync Server "代理トランザクション" の一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信などの一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) などのアプリケーションから自動で実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、**CsHealthMonitoringConfiguration** コマンドレットを使用して、テスト ユーザーを各レジストラー プールに設定します。これらのテスト ユーザーとは、代理トランザクションでの使用を目的としてあらかじめ構成されている 1 組のユーザーのことです (通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません)。プールに構成されたテスト ユーザーを使用すると、管理者がテスト用にユーザー アカウント ID を指定したり資格情報を入力したりしなくても、そのプールに対して簡単に代理トランザクションを実行できます。

管理者は、実際のユーザー アカウントを使用して代理トランザクションを実行することもできます。たとえば、2 人のユーザーがインスタント メッセージを交換できない場合、管理者は、問題のある 2 人のユーザー アカウント (2 つのテスト アカウントではなく) を使用して代理トランザクションを実行し、問題の診断と解決を試みることができます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーのログオン名とパスワードを入力する必要があります。

Test-CsPstnOutboundCall はまたサーバー プラットフォーム モードで使用することもできます。その場合、ユーザーの SIP アドレスを指定する必要があるだけで、Lync Server は証明書を使用してユーザーを認証します。

**Test-CsPstnOutboundCall** コマンドレットを実行すると、コマンドレットではまず、テスト ユーザーを Lync Server にログオンさせるよう試みます。ログオンが正常に行われると、次に、PSTN ゲートウェイを使用して電話をかけるよう試みます。この電話は、ダイヤル プラン、音声ポリシー、およびテスト アカウントに割り当てられているその他のポリシーと設定を使用してかけられます。通話への応答があると、コマンドレットはネットワーク上にデュアルトーン多重周波数 (DTMF) コードを送信し、メディア接続を検証します。

テストを行う際に、**Test-CsPstnOutboundCall** コマンドレットを実行すると、実際に電話をかけられます。通話先が呼び出され、テストが成功するためには、通話先が応答する必要があります。また、この通話は、管理者が手動で終了する必要があります。

このコマンドレットを実行できるユーザー: このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnOutboundCall"}

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
<td><p>テスト対象プールの完全修飾ドメイン名 (FQDN)。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>必須</p></td>
<td><p>String</p></td>
<td><p>テストを実行するときに呼び出す PSTN 電話番号。通話先電話番号は E.164 形式を使用して指定するのが最良で、つまりその番号は &quot;+14255551298&quot; のようになることを意味します。この番号には正符号 (+)、その後に国/地域コード (1)、市外局番 (425)、電話番号 (5551298) が含まれます。電話番号を指定する際に、ダッシュ、かっこ、およびその他の文字は使用しないでください。</p>
<p>E.164 形式を使用しない場合、テスト ユーザーのダイヤル プランが番号に追加されます。Lync Server はそのダイヤル プランを使用して番号を E.164 形式に正規化します。番号を正規化できないと、電話をかけることはできず、テストは失敗します。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必須かどうか</p></td>
<td><p>PSCredential</p></td>
<td><p>テスト対象のアカウントのユーザーの資格情報オブジェクト。UserCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得されるオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\kenmyer というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $x という名前の変数に格納します。</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。</p>
<p>このパラメーターは、このコマンドが CsHealthMonitoringConfiguration コマンドレットを使用して構成されたテスト ユーザーを使用している場合には必要ありません。また、テストがサーバー プラットフォーム モードで実行されている場合も、このパラメーターを指定する必要はありません。その場合、Lync Server は証明書を使用してユーザーを認証しようとします。</p></td>
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
<td><p>System.String</p></td>
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
<td><p><em>RegistrarPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>レジストラー サービスが使用する SIP ポート。レジストラーが既定のポート 5061 を使用する場合、このパラメーターは必要ありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テスト対象のユーザー アカウントの SIP アドレス。次に例を示します。-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。UserSipAddress パラメーターは、UserCredential と同じユーザー アカウントを参照している必要があります。</p>
<p>このパラメーターは、このコマンドが CsHealthMonitoringConfiguration コマンドレットを使用して構成されたテスト ユーザーを使用している場合には必要ありません。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsPstnOutboundCall** コマンドレットはパイプライン処理された入力を受け入れません。

## 戻り値の種類

**Test-CsPstnOutboundCall** コマンドレットを実行すると、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Test-CsPstnPeerToPeerCall](test-cspstnpeertopeercall.md)

