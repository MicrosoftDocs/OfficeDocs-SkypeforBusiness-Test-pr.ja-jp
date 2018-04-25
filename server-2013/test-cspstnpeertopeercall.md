---
title: Test-CsPstnPeerToPeerCall
TOCTitle: Test-CsPstnPeerToPeerCall
ms:assetid: 839cf83f-b667-4cbe-b1ab-28f54a8a9d0b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398662(v=OCS.15)
ms:contentKeyID: 48272694
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnPeerToPeerCall

 

_**トピックの最終更新日:** 2015-03-09_

公衆交換電話網 (PSTN) ゲートウェイ経由で、1 組のユーザーがピアツーピア通話を実行できるかどうかをテストします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsPstnPeerToPeerCall -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 例

## 例 1

例 1 では、1 組の構成済みのテスト ユーザーが atl-cs-001.litwareinc.com というプールにログオンできるかどうかを確認します。テスト ユーザーのログオン後に、**Test-CsPstnPeerToPeerCall** コマンドレットを実行して、この 2 人のユーザーが PSTN ゲートウェイ経由でピアツーピア通話を行うことができるかどうかを確認します。このコマンドが有効なのは、テスト ユーザーが atl-cs-001.litwareinc.com プール用に定義されている場合だけです。定義されている場合、コマンドを実行すると、最初のテスト ユーザーがシステムにログオンできるかどうかの判定と、このユーザーがプールで定義されている 2 番目のユーザーを呼び出せるかどうかの確認が行われます。

テスト ユーザーが定義されていない場合、テスト実行中に使用するユーザーを認識できないため、コマンドは失敗します。プールのテスト ユーザーが定義されていない場合、およびサーバー プラットフォーム モードで実行していない場合は、SenderSipAddress パラメーターと ReceiverSipAddress パラメーター、およびテスト アカウントとして機能するユーザーの対応する資格情報を追加する必要があります。こうして、**Test-CsPstnPeerToPeerCall** コマンドレットで、指定した 2 人のユーザーを使用したチェックを実行します。

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com 

## 例 2

例 2 のコマンドは、ユーザーのペア (litwareinc\\pilar と litwareinc\\kenmyer) が Lync Server にログオンして PSTN ゲートウェイ経由のピアツーピア通話を行うことができるかどうかをテストします。これを実行するには、最初のコマンドで **Get-Credential** コマンドレットを使用して、Pilar Ackerman というユーザーの名前とパスワードを含む、Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 litwareinc\\pilar はパラメーターとして含まれているため、管理者は、\[Windows PowerShell 資格情報の要求\] ダイアログ ボックスに Pilar Ackerman のアカウントのパスワードを入力するだけです)。作成された資格情報オブジェクトは、$cred1 という名前の変数に格納されます。2 番目のコマンドも同じことをしますが、このときは、Ken Myer というアカウントの資格情報オブジェクトを戻します。

3 番目のコマンドでは、2 人のユーザーが 2 つの資格情報オブジェクトを使用して Lync Server にログオンし、PSTN ゲートウェイ経由のピアツーピア通話を行うことができるかどうかを判定します。このタスクを実行するには、**Test-CsPstnPeerToPeerCall** コマンドレットを呼び出して次のパラメーターを指定します。TargetFqdn (レジストラー プールの FQDN)、SenderSipAddress (1 番目のテスト ユーザーの SIP アドレス)、SenderCredential (1 番目のテスト ユーザーの資格情報を保持している Windows PowerShell オブジェクト)、ReceiverSipAddress (もう一方のテスト ユーザーの SIP アドレス)、および ReceiverCredential (もう一方のテスト ユーザーの資格情報を保持している Windows PowerShell オブジェクト)。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## 例 3

例 3 は、Test-CsPstnPeerToPeerCall コマンドレットをサーバー プラットフォーム モードで使用する方法を示しています。このモードでは、テスト ユーザーの SIP アドレスを指定しますが、ユーザーの資格情報は含めません。この方法で実行すると、Lync Server は証明書を使用して 2 人のテスト ユーザーを認証します。

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" 

## 解説

**Test-CsPstnPeerToPeerCall** コマンドレットは、Lync Server の "代理トランザクション" の一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信など、一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) のようなアプリケーションから自動で実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、**CsHealthMonitoringConfiguration** コマンドレットを使用して、各レジストラー プールにテスト ユーザーを設定します。テスト ユーザーとは、代理トランザクションでの使用を目的として構成されている 1 組のユーザーのことです (通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません)。プールに構成されたテスト ユーザーを使用すると、管理者がテスト用にユーザー アカウント ID を指定したり資格情報を入力したりしなくても、そのプールに対して簡単に代理トランザクションを実行できます。

管理者は、実際のユーザー アカウントを使用して代理トランザクションを実行することもできます。たとえば、2 人のユーザーがインスタント メッセージを交換できない場合、管理者は、問題のある 2 人のユーザー アカウント (2 つのテスト アカウントではなく) を使用して代理トランザクションを実行し、問題の診断と解決を試みることができます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーのログオン名とパスワードを入力する必要があります。

**Test-CsPstnPeerToPeerCall** コマンドレットは、サーバー プラットフォーム モードでも使用できます。その場合は、ユーザーの SIP アドレスのみ指定が必要になります。Lync Server は、証明書を使用してそれらのユーザーを認証します。

**Test-CsPstnPeerToPeerCall** コマンドレットを呼び出すと、まずテスト ユーザー 2 人の Lync Server へのログオンが試行されます。ログオンが成功すると、ユーザー 1 からユーザー 2 への PSTN ゲートウェイ経由の呼び出しが試行されます。**Test-CsPstnPeerToPeerCall** コマンドレットでは、テスト ユーザーに割り当てられているダイヤル プラン、音声ポリシー、およびその他のポリシーと構成設定を使用してこの呼び出しを行います。テストが予定どおり実行され、ユーザー 2 が呼び出しに応答できたことが確認されると、両方のテスト アカウントがシステムからログオフします。

**Test-CsPstnPeerToPeerCall** コマンドレットでは、実際に電話で発信します。これにより、接続を確立でき、ネットワーク全体でデュアルトーン多重周波数 (DTMF) コードを送信できることを検証し、接続を介してメディアを送信できるかどうかを判断します。ただし、その呼び出しにはコマンドレット自体が応答するため、手動で通話を終了する必要はありません (つまり、誰も発信された電話に応答して、切る必要はありません)。

このコマンドレットを実行できるユーザー: このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnPeerToPeerCall"}

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
<td><p>テスト対象の 2 ユーザー アカウントのうち、最初のユーザーの資格情報オブジェクト。ReceiverCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得されるオブジェクト参照である必要があります。たとえば以下のコードは、litwareinc\pilar というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $y という名前の変数に格納します。</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合、またはサーバー プラットフォーム モードで実行している場合は、受信者の資格情報は必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>必須</p></td>
<td><p>PSCredential</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、2 番目のユーザーの資格情報オブジェクト。SenderCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得されるオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\kenmyer というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $x という名前の変数に格納します。</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合、またはサーバー プラットフォーム モードで実行している場合は、送信者の資格情報は必要ありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>必須</p></td>
<td><p>String</p></td>
<td><p>テスト対象プールの完全修飾ドメイン名 (FQDN) です。</p></td>
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
<p>$TestOutput という名前のロガー変数の出力を保存するには、以下の構文を使用します。</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注: 変数名を指定するときは、先頭に $ 文字を付けないでください。ロガー変数に格納された情報を HTML ファイルに保存するには、以下のようなコマンドを使用します。</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>ロガー変数に格納された情報を XML ファイルに保存するには、以下のようなコマンドを使用します。</p>
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
</tbody>
</table>


## 入力の種類

なし。**Test-CsPstnPeerToPeerCall** コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

**Test-CsPstnPeerToPeerCall** コマンドレットを実行すると、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Test-CsPstnOutboundCall](test-cspstnoutboundcall.md)

