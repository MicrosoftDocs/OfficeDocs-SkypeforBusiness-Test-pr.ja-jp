---
title: Test-CsAddressBookWebQuery
TOCTitle: Test-CsAddressBookWebQuery
ms:assetid: 9753dcba-83b3-437b-98f0-2806305a5bbb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398773(v=OCS.15)
ms:contentKeyID: 48272953
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookWebQuery

 

_**トピックの最終更新日:** 2015-03-09_

ユーザーがアドレス帳 Web クエリ サービスを使用して、アドレス帳の情報を検索および取得できるかどうかをテストします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsAddressBookWebQuery -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAddressBookWebQuery -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsAddressBookWebQuery -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TargetSipAddress <String>]

## 例

## 例 1

例 1 では、SIP アドレスが sip:kenmyer@litwareinc.com の連絡先を検索して、プール atl-cs-001.litwareinc.com でアドレス帳 Web クエリ サービスをテストします。このコマンドは、プール atl-cs-001.litwareinc.com のテスト ユーザーが定義されている場合のみ機能します。テスト ユーザーが定義されている場合、プールに定義されている最初のテスト ユーザーの資格情報を使ってコマンドが実行されます。

テスト ユーザーが定義されていない場合、コマンドは失敗します。プールのテスト ユーザーを定義していない場合は、UserSipAddress パラメーターと、コマンドの実行に使用するユーザーの資格情報を指定する必要があります。

    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.litwareinc.com  -TargetSipAddress "sip:kenmyer@litwareinc.com"

## 例 2

例 2 に示すコマンドも アドレス帳 Web クエリ サービス が使用可能かどうかをテストしますが、この例では、ユーザー Ken Myer (litwareinc\\kenmyer) の資格情報を使ってコマンドが実行されます。これを実行するため、最初のコマンドで **Get-Credential** コマンドレットを使用して、Ken Myer というユーザーの名前とパスワードを含む、Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 litwareinc\\kenmyer はパラメーターとして指定されているため、管理者は \[Windows PowerShell 資格情報の要求\] ダイアログ ボックスで、Ken Myer アカウントのパスワードのみ入力する必要があります)。作成された資格情報オブジェクトは、$cred1 という名前の変数に格納されます。

2 番目のコマンドでは、**Test-CsAddressBookWebQuery** コマンドレットを使用し、プール atl-cs-001.litwareinc.com で アドレス帳 Web クエリ サービス をテストします。Ken Myer のユーザー資格情報を使ってこのコマンドを実行するため、UserCredential パラメーターを指定し、パラメーター値を $cred1 に設定します。また、TargetSipAddress を使用し、コマンドレットがアドレス帳で SIP アドレスが sip:kenmyer@litwareinc.com の連絡先を検索するように指定します。

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:kenmyer@litwareinc.com" -TargetSipAddress "sip:kenmyer@litwareinc.com"

## 例 3

例 3 は、atl-cs-001.litwareinc.com で アドレス帳 Web クエリ サービス をテストする方法を示しています。これを行うため、**Test-CsAddressBookWebQuery** コマンドレットを呼び出し、次の 3 つのパラメーターを指定します。TargetUri で アドレス帳 Web クエリ サービス の URI を指定し、UserSipAddress でテスト対象のユーザー アカウントの Windows PowerShell SIP アドレスを指定し、TargetSipAddress で検索対象のユーザー アカウントの SIP アドレスを指定します。

    Test-CsAddressBookWebQuery -TargetUri https://atl-cs-001.litwareinc.com/groupexpansion -UserSipAddress "sip:packerman@litwareinc.com" -TargetSipAddress "sip:kenmyer@litwareinc.com"

## 解説

**Test-CsAddressBookWebQuery** コマンドレットは、"代理トランザクション" の一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信などの一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) などのアプリケーションから自動で実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、**CsHealthMonitoringConfiguration** コマンドレットを使用して、テスト ユーザーを各レジストラー プールに設定します。このテスト ユーザーは、代理トランザクションで使用するためにあらかじめ構成されている 1 組のユーザーです (通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません)。プールに構成されているテスト ユーザーを使って、管理者はテスト用にユーザー アカウントの ID を指定したり資格情報を入力したりしなくても、そのプールに対して代理トランザクションを実行することができます。

また、管理者は実際のユーザー アカウントを使用して、代理トランザクションを実行することもできます。たとえば、ある 2 人のユーザーがインスタント メッセージの交換を行うことができない場合に、管理者は (テスト アカウントではなく) その 2 つのユーザー アカウントを使って代理トランザクションを実行し、問題の診断と解決を試みることができます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーのログオン名とパスワードを入力する必要があります。

管理者は **Test-CsAddressBookWebQuery** コマンドレットを使って、ユーザーが アドレス帳 Web クエリ サービス を使用して特定の連絡先を検索できることを確認できます。**Test-CsAddressBookWebQuery** コマンドレットを実行すると、まず認証を行うため Web チケット サービスに接続します。認証に成功すると、今度は アドレス帳 Web クエリ サービス に接続して、指定された連絡先の検索を行います。連絡先が見つかると、その情報をローカル コンピューターへ戻そうとします。これらの手順がすべて完了できる場合にのみ、テストは成功としてマークされます。

このコマンドレットを実行できるユーザー: このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAddressBookWebQuery"}

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
<td><p>アドレス帳 Web クエリ サービス がテストされるレジストラー プールの完全修飾ドメイン名 (FQDN) です。次に例を示します。-TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p>TargetUri パラメーターと TargetFqdn パラメーターの両方を、同じコマンド内で使用することはできません。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>必須</p></td>
<td><p>String</p></td>
<td><p>アドレス帳 Web クエリ サービス の Uniform Resource Identifier (URI) です。次に例を示します。-TargetUri &quot;https://atl-cs-001.litwareinc.com/groupexpansion&quot;。</p>
<p>TargetUri パラメーターと TargetFqdn パラメーターの両方を、同じコマンド内で使用することはできません。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必須</p></td>
<td><p>PSCredential</p></td>
<td><p>テストで使用されるユーザー アカウントのユーザーの資格情報オブジェクトです。UserCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得したオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\kenmyer というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを</p>
<p>$x という名前の変数に格納します。$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>このコマンドを実行するときは、ユーザーのパスワードを入力する必要があります。</p></td>
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
<td><p><em>External</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>外部ユーザーが アドレス帳 Web クエリ サービス を使用できるかを確認できます。</p></td>
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
<p>変数名を指定するときは、先頭に $ 記号を使用しないでください。</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>レジストラー サービスが使用する SIP ポートです。レジストラーが既定のポート 5061 を使用する場合、このパラメーターは必要ありません。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>アドレス帳 Web クエリ サービス によって戻されると想定される連絡先の SIP アドレスです。次に例を示します。-TargetSipAddress &quot;sip:kenmyer@litwareinc.com&quot;。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テストで使用されるユーザーの SIP アドレスです。このパラメーターが指定されていない場合、<strong>Test-CsAddressBookWebQuery</strong> コマンドレットは、テスト対象のプールの状態監視の構成設定を使って確認を行います。</p></td>
</tr>
<tr class="even">
<td><p><em>WebCredential</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSCredential</p></td>
<td><p>場所情報サービスにアクセスするユーザー資格情報を含んだオブジェクトです。このオブジェクトは <strong>Get-Credential</strong> コマンドレットを呼び出し、該当する資格情報を指定することで取得できます。</p>
<p>このパラメーターは、TargetUri パラメーターと UserSipAddress パラメーターが指定されており、このコマンドレットを実行するコンピューターにサーバー証明書が存在しない場合に必須です。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsAddressBookWebQuery** コマンドレットは、パイプ処理による入力を受け入れません。

## 戻り値の種類

**Test-CsAddressBookWebQuery** コマンドレットは、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Update-CsAddressBook](update-csaddressbook.md)

