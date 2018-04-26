---
title: Test-CsAddressBookService
TOCTitle: Test-CsAddressBookService
ms:assetid: 8398c9ea-eaab-4a4d-9e09-473ea2b27e22
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398661(v=OCS.15)
ms:contentKeyID: 48272693
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookService

 

_**トピックの最終更新日:** 2015-03-09_

アドレス帳のダウンロード Web サービスをホストするサーバーへのユーザーのアクセス機能をテストします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsAddressBookService -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## 例

## 例 1

例 1 では、プール atl-cs-001.litwareinc.com のアドレス帳のダウンロード Web サービスをテストしています。このコマンドでは、プール atl-cs-001.litwareinc.com で構成済みのテスト ユーザーを使用してアドレス帳のダウンロード Web サービスをテストします。

    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com 

## 例 2

例 2 に示すコマンドは、アドレス帳のダウンロード Web サービスを実行するサーバーを使用できるかどうかもテストします。この場合、コマンドはユーザー Ken Myer (litwareinc\\kenmyer) の資格情報で実行します。これを実行するには、最初のコマンドで **Get-Credential** コマンドレットを使用して、Ken Myer というユーザーの名前とパスワードを含む、Windows PowerShell 資格情報オブジェクトを作成します (ログオン名 (litwareinc\\kenmyer) はパラメーターとして含まれているため、管理者は、\[Windows PowerShell 資格情報の要求\] ダイアログ ボックスに Ken Myer のアカウントのパスワードを入力するだけです)。作成された資格情報オブジェクトは、$cred1 という名前の変数に格納されます。

2 番目のコマンドで、**Test-CsAddressBookService** コマンドレットを使用して atl-cs-001.litwareinc.com というプールのアドレス帳のダウンロード Web サービスをテストします。このコマンドを Ken Myer のユーザー資格情報で実行するために、UserCredential パラメーターとパラメーター値 $cred1 を含めます。また、UserSipAddress パラメーターを使用して Ken の SIP アドレスを指定することも必要です。

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:kenmyer@litwareinc.com"

## 例 3

例 3 は、atl-cs-001.litwareinc.com のアドレス帳のダウンロード Web サービスをテストする方法を示しています。これを実行するため、次の 2 つのパラメーターと共に **Test-CsAddressBookService** コマンドレットを呼び出します。TargetUri はアドレス帳のダウンロード Web サービスの URI を指定し、UserSipAddress はテストで使用されるユーザー アカウントの Windows PowerShell SIP アドレスを含みます。

``` 


Test-CsAddressBookService -TargetUri https://atl-cs-001.litwareinc.com/abs/handler -UserSipAddress "sip:kenmyer@litwareinc.com"
```

## 解説

**Test-CsAddressBookService** コマンドレットは、"代理トランザクション" の一例です。代理トランザクションは Lync Server で使用され、システムへのログオン、インスタント メッセージの交換、公衆交換電話網 (PSTN) 上の電話への発信など、一般的なタスクをユーザーが正常に実行できることを検証するものです。これらのテストは、管理者が手動で実行することも、Microsoft System Center Operations Manager (以前の Microsoft Operations Manager) のようなアプリケーションから自動で実行することもできます。

代理トランザクションは、通常、2 つの異なる方法で実行されます。多くの管理者は、**CsHealthMonitoringConfiguration** コマンドレットを使用して、各レジストラー プールにテスト ユーザーを設定します。テスト ユーザーとは、代理トランザクションでの使用を目的として構成されている 1 組のユーザーのことです (通常、これらはテスト アカウントであり、実際のユーザーのアカウントではありません)。プールに構成されたテスト ユーザーを使用すると、管理者がテスト用にユーザー アカウント ID を指定したり資格情報を入力したりしなくても、そのプールに対して代理トランザクションを実行できます。

管理者は、実際のユーザー アカウントを使用して代理トランザクションを実行することもできます。たとえば、2 人のユーザーがインスタント メッセージを交換できない場合、管理者は、それら 2 人のユーザー アカウント (2 つのテスト アカウントではなく) を使用して代理トランザクションを実行し、それから問題の診断と解決を試みることができます。実際のユーザー アカウントを使用して代理トランザクションを実行する場合は、各ユーザーのログオン名とパスワードを入力する必要があります。

**Test-CsAddressBookService** コマンドレットを使用すると、ユーザーがアドレス帳のダウンロード Web サービスに接続可能であることを確認できます。**Test-CsAddressBookService** コマンドレットを実行すると、指定したプールのアドレス帳のダウンロード Web サービスに接続してアドレス帳ファイルの場所を要求します。この場所がアドレス帳のダウンロード Web サービスで表示される場合は、テストが成功とみなされます。要求が拒否された場合は、テストが失敗とみなされます。

アドレス帳のダウンロード Web サービスのテストには 2 種類の方法があります。サービス自体をテストするか、または関連付けられた Web サービスをテストします。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Test-CsAddressBookService** コマンドレットを実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAddressBookService"}

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
<td><p>アドレス帳のダウンロード Web サービスをテストするレジストラー プールの完全修飾ドメイン名 (FQDN) です。次に例を示します。-TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;。</p>
<p>TargetUri パラメーターと TargetFqdn パラメーターを同じコマンドで使用することはできません。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>必須</p></td>
<td><p>String</p></td>
<td><p>アドレス帳 Web クエリ サービスの URI (Uniform Resource Identifier) です。次に例を示します。-TargetUri &quot;https://atl-cs-001.litwareinc.com/abs/handler&quot;</p>
<p>TargetUri パラメーターと TargetFqdn パラメーターを同じコマンドで使用することはできません。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必須</p></td>
<td><p>PSCredential</p></td>
<td><p>テストで使用されるユーザー アカウントのユーザーの資格情報オブジェクトです。UserCredential に渡す値は、<strong>Get-Credential</strong> コマンドレットを使用して取得されるオブジェクト参照である必要があります。たとえば次のコードは、litwareinc\kenmyer というユーザーの資格情報オブジェクトを戻し、そのオブジェクトを $x という名前の変数に格納します。</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;。</p>
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
<td><p>外部ユーザーがアドレス帳のダウンロード Web サービスを使用できることを確認できます。</p></td>
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
<p>$TestOutput という名前のロガー変数の出力を保存するには、以下の構文を使用します。</p>
<p>-OutLoggerVariable TestOutput</p>
<p>注: 変数名を指定するときは、先頭に $ 文字を付けないでください。ロガー変数に格納された情報を HTML ファイルに保存するには、以下のようなコマンドを使用します。</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>ロガー変数に格納された情報を XML ファイルに保存するには、以下のようなコマンドを使用します。</p>
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
<td><p><em>UserSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テストで使用されるユーザーの SIP アドレスです。このパラメーターを指定しないと、<strong>Test-CsAddressBookService</strong> ではログインしているユーザーのアカウントを使用してチェックが実行されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSCredential</p></td>
<td><p>場所情報サービスにアクセスするユーザー資格情報を含んだオブジェクトです。このオブジェクトは <strong>Get-Credential</strong> コマンドレットを呼び出し、該当する資格情報を指定することで取得できます。</p>
<p>このパラメーターは、TargetUri パラメーターと UserSipAddress パラメーターが指定されており、このコマンドレットを実行するコンピューターにサーバー証明書が存在しない場合に必須です。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Test-CsAddressBookService** コマンドレットは、パイプライン処理された入力を受け入れません。

## 戻り値の種類

**Test-CsAddressBookService** コマンドレットを実行すると、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスが戻されます。

## 関連項目

#### その他のリソース

[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)  
[Update-CsAddressBook](update-csaddressbook.md)

