---
title: Test-CsPresence
TOCTitle: Test-CsPresence
ms:assetid: 09a5faf6-4e80-4a3b-ac84-aec9778ee9b5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398148(v=OCS.15)
ms:contentKeyID: 48271196
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPresence

 

_**トピックの最終更新日:** 2015-03-09_

ユーザーが Lync Server にログオンできるかどうか、ユーザーのプレゼンス情報を公開できるかどうか、およびもう 1 人のユーザーが公開しているプレゼンス情報にサブスクライブできるかどうかをテストします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsPresence -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-PublisherSipAddress <String>] [-RegistrarPort <Int32>] [-SubscriberSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPresence -PublisherCredential <PSCredential> -PublisherSipAddress <String> -SubscriberCredential <PSCredential> -SubscriberSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPresence [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-SubscriberSipAddress <String>]

## 例

## 例 1

例 1 では、あらかじめ構成されたテスト ユーザーのペアが atl-cs-001.litwareinc.com プールにログオンできるかどうかを確認しています。テスト ユーザーがログオンした後で、**Test-CsPresence** コマンドレットを実行して 2 人のユーザーがプレゼンス情報を交換できるかどうかを確認します。このコマンドが正常に機能するのは、テスト ユーザーが atl-cs-001.litwareinc.com プールに対して定義されている場合だけです。定義されていれば、このコマンドで、1 番目のテスト ユーザーがシステムにログオンできるかどうかを確認し、このユーザーがこのプールに対して定義されている 2 番目のテスト ユーザーとプレゼンス情報を交換できるかどうかを確認できます。

レジストラーが定義されていない場合、テスト実行中に使用するユーザーを認識できないので、コマンドは失敗します。プールに対してテスト ユーザーを定義していない場合、SubscriberSipAddress パラメーターと PublisherSipAddress パラメーター、およびプレゼンス サブスクライバーとプレゼンス発行者の役割を果たすユーザーに対応する資格情報を指定する必要があります。**Test-CsPresence** コマンドレットは、指定された 2 人のユーザーを使用して確認を行います。

    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com 

## 例 2

例 2 のコマンドでは、ユーザーのペア (litwareinc\\pilar と litwareinc\\kenmyer) が Lync Server にログオンしてからプレゼンス情報を交換できることを確認します。これを行うために、この例の最初のコマンドで **Get-Credential** コマンドレットを使用して、Pilar Ackerman というユーザーの名前とパスワードが含まれる Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 litwareinc\\pilar はパラメーターとして指定されているため、表示される \[Windows PowerShell 資格情報の要求\] ダイアログ ボックスで管理者が入力する必要がある情報は、Pilar Ackerman アカウントのパスワードだけです)。作成された資格情報オブジェクトは、$cred1 という名前の変数に格納されます。2 番目のコマンドも同じことをしますが、こちらは Ken Myer というアカウントの資格情報オブジェクトを戻します。

2 つの資格情報オブジェクトを取得した後、この例の 3 番目のコマンドで、この 2 人のユーザーが Lync Server にログオンしてからプレゼンス情報を交換できるかどうかを判別します。これを行うために、**Test-CsPresence** コマンドレットを呼び出しますが、このとき次のパラメーターを指定します。TargetFqdn (レジストラー プールの FQDN)、SubscriberSipAddress (最初のテスト ユーザー の SIP アドレス)、SubscriberCredential (最初のテスト ユーザーの資格情報が含まれる Windows PowerShell オブジェクト)、PublisherSipAddress (もう一方のテスト ユーザーの SIP アドレス)、および PublisherCredential (もう一方のテスト ユーザーの資格情報が含まれる Windows PowerShell オブジェクト)。

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com -SubscriberSipAddress "sip:pilar@litwareinc.com" -SubscriberCredential $cred1 -PublisherSipAddress "sip:kenmyer@litwareinc.com" -PublisherCredential $cred2

## 解説

**Test-CsPresence** コマンドレットは、Lync Server 代理トランザクションの一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信などの一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) などのアプリケーションから自動で実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、**CsHealthMonitoringConfiguration** コマンドレットを使用して、テスト ユーザーを各レジストラー プールに設定します。通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません。プールに構成されたユーザー アカウントを使用すると、管理者がテスト用にユーザー アカウント ID を指定したり資格情報を入力したりしなくても、そのプールに対して簡単に代理トランザクションを実行できます。

管理者は、実際のユーザー アカウントを使用して代理トランザクションを実行することもできます。たとえば、2 人のユーザーがインスタント メッセージを交換できない場合、管理者は、問題のある 2 人のユーザー アカウント (2 つのテスト アカウントではなく) を使用して代理トランザクションを実行し、問題の診断と解決を試みることができます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーのログオン名とパスワードを入力する必要があります。

**Test-CsPresence** コマンドレットを使用して、テスト ユーザーのペアが Lync Server にログオンして、プレゼンス情報を交換できるかどうかを確認します。これを行うために、コマンドレットを実行して、この 2 人のユーザーをシステムにログオンさせます。両方のログオンが正常に行われたら、1 番目のテスト ユーザーが、2 番目のテスト ユーザーからプレゼンス情報を受信するよう依頼します。2 番目のユーザーがこの情報を公開したら、**Test-CsPresence** コマンドレットを実行して、情報が 1 番目のユーザーに正常に転送されたことを確認します。プレゼンス情報を交換したら、2 人のテスト ユーザーは Lync Server からログオフします。

このコマンドレットを実行できるユーザー: このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPresence"}

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
<td><p><em>PublisherCredential</em></p></td>
<td><p>必須</p></td>
<td><p>PSCredential</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、最初のユーザーの資格情報オブジェクト。PublisherCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得されるオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\kenmyer というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $x という名前の変数に格納します。</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合は、発行者の資格情報は必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberCredential</em></p></td>
<td><p>必須</p></td>
<td><p>PSCredential</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、2 番目のユーザーの資格情報オブジェクト。SubscriberCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得されるオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\pilar というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $y という名前の変数に格納します。</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合は、サブスクライバーの資格情報は必要ありません。</p></td>
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
<p>出力を $TestOutput という名前のロガー変数に保存するには、以下の構文を使用します。</p>
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
<td><p><em>PublisherSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、最初のユーザーの SIP アドレス。次に例を示します。-PublisherSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。PublisherSipAddress パラメーターが PublisherCredential と同じユーザー アカウントを参照している必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合は、SIP アドレスは必要ありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>レジストラー サービスが使用する SIP ポート。レジストラーが既定のポート 5061 を使用する場合、このパラメーターは必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テスト対象の 2 ユーザー アカウントのうち、2 番目のユーザーの SIP アドレス。次に例を示します。-SubscriberSipAddress &quot;sip:pilar@litwareinc.com&quot;.SubscriberSipAddress パラメーターが SubscriberCredential と同じユーザー アカウントを参照している必要があります。</p>
<p>プールの状態監視構成設定でテストを実行している場合は、SIP アドレスは必要ありません。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsPresence** コマンドレットはパイプライン処理された入力を受け入れません。

## 戻り値の種類

**Test-CsPresence** コマンドレットを実行すると、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Test-CsRegistration](test-csregistration.md)

