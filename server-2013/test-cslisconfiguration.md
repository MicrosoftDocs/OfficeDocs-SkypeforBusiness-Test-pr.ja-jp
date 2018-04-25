---
title: Test-CsLisConfiguration
TOCTitle: Test-CsLisConfiguration
ms:assetid: 6983d42e-6b93-4365-b0f1-81031d6e251b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398497(v=OCS.15)
ms:contentKeyID: 48272392
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLisConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

場所情報サーバー (LIS) 構成をテストします。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Test-CsLisConfiguration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BssId <String>] [-ChassisId <String>] [-Force <SwitchParameter>] [-Mac <String>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-PortId <String>] [-PortIdSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] [-Subnet <String>]

## 例

## 例 1

この例では、FQDN atl-cs-001.litwareinc.com で LIS 構成をテストします。現在のユーザー資格情報を使用して、その FQDN の LIS Web サービスに接続できれば、テストに成功します。サブネット IP アドレス 192.168.0.0 にマップする場所を検出可能な場合は、その場所のアドレスが戻されます。

このコマンドを正常に実行するには、代理トランザクション ユーザーを含んだ状態監視構成が存在する必要があります。状態監視構成が存在するかどうかを確認するには、**Get-CsHealthMonitoringConfiguration** コマンドレットを実行します。新しい状態監視構成を作成するには、**New-CsHealthMonitoringConfiguration** コマンドレットを実行します。

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0

## 例 2

この例は、UserSipAddress パラメーターが追加されている点を除いて、例 1 と同じです。このコマンドは、代理トランザクション ユーザーは設定されていないが、コマンドを実行するコンピューターにサーバー証明書が存在する場合に使用します。

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com

## 例 3

この例の最初の行では、Windows PowerShell コマンドレットである **Get-Credential** コマンドレットを呼び出して、ユーザーにユーザー ID とパスワードの入力を求めています。この情報は、変数 $cred 内に暗号化形式で格納されます。

2 行目は、UserSipAddress パラメーターが追加されている点を除いて、例 2 のコマンドと同じです。このコマンドは、代理トランザクション ユーザーが設定されておらず、コマンドを実行するコンピューターにサーバー証明書が存在しない場合に使用します。

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com -UserCredential $cred

## 例 4

この例の最初の行では、**Get-Credential** コマンドレットを呼び出して、ユーザーにユーザー ID とパスワードの入力を求めています。この情報は、変数 $cred 内に暗号化形式で格納されます。

2 行目では、リモート ユーザーの SIP アドレス (sip:kmyer@litwareinc.com) に基づいて Web サービス URI (https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc) に対して呼び出しを行い、行 1 で取得した資格情報を WebCredential パラメーターに渡して、LIS 構成をテストします。特定のユーザー資格情報を使用して、その URI の LIS Web サービスに接続できれば、テストに成功します。サブネット IP アドレス 192.168.0.0、MAC アドレス 0A-23-00-00-00-AA または Port ID 4500、および ChassisId 0A-23-00-00-00-AA にマップする場所を検出できた場合、その場所のアドレスが戻されます。

このコマンドは、コマンドを実行するコンピューターにサーバー証明書が存在しない場合に使用します。

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -WebCredential $cred -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## 例 5

この例は、コマンドで WebCredential パラメーターを使用しない点 (そのため、**Get-Credential** コマンドレットも呼び出しません) を除いて、例 4 と同じです。このコマンドは、コマンドを実行するコンピューターにサーバー証明書が存在する場合に使用します。

    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## 解説

このコマンドレットは、指定されたパラメーターの情報に基づいて、場所情報サーバー (LIS) Web サービスにアクセスできるかどうかを判別します。Web サービスにアクセスでき、指定のパラメーターのいずれかに該当する場所が検出されると、テストはパスしたものとみなされ、場所が表示されます。場所が検出されない場合でも、Web サービスにアクセス可能であれば、テストにはパスしますが、場所情報は戻されません。また、いずれのオプション パラメーターも指定せずにこのコマンドレットを呼び出すと、Web サービスにアクセスできる限りテストにパスしますが、この場合も場所情報は戻されません。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Test-CsLisConfiguration** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsConfiguration"}

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
<td><p>テストを実行するサーバーの完全修飾ドメイン名 (FQDN) (server.litwareinc.com の形式) です。</p>
<p>このパラメーターは、TargetUri パラメーターを指定しない限り必須です。TargetUri パラメーターを指定する場合は、TargetFqdn を指定できません。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>必須</p></td>
<td><p>String</p></td>
<td><p>場所情報サービスの URI (Uniform Resource Identifier) です。場所情報サービスの URI は、コマンド Get-CsService –WebServer | Select-Object LIServiceInternalUri を実行することによって取得できます。</p>
<p>このパラメーターの値を指定する場合は、UserSipAddress パラメーターも必要になります。コマンドを実行するコンピューターにサーバー証明書が存在しない場合は、WebCredential パラメーターの値も指定する必要があります。</p>
<p>このパラメーターは、TargetFqdn パラメーターを指定しない限り必須です。</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>必須</p></td>
<td><p>PSCredential</p></td>
<td><p>場所情報サービスにアクセスするためのユーザー資格情報を含んだオブジェクトです。このオブジェクトは <strong>Get-Credential</strong> コマンドレットを呼び出し、該当する資格情報を指定することで取得できます。</p>
<p>TargetFqdn パラメーターと UserSipAddress パラメーターが指定されている場合、およびこのコマンドレットを実行するコンピューターにサーバー証明書が存在しない場合、このパラメーターは必須です。</p></td>
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
<td><p><em>BssId</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>ワイヤレス アクセス ポイントの基本サービス セット識別子 (BSSID) です。この値は、nn-nn-nn-nn-nn-nn の形式 (12-34-56-78-90-ab など) にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>ChassisId</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>ネットワーク スイッチのメディア アクセス制御 (MAC) アドレスです。この値は、nn-nn-nn-nn-nn-nn の形式 (12-34-56-78-90-ab など) または IP アドレスにする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>このパラメーターは、場所情報サーバーではサポートされていません。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Mac</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>ポート スイッチの MAC アドレス。この値は、nn-nn-nn-nn-nn-nn の形式 (12-34-56-78-90-ab など) にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>コマンドレットを実行した結果の詳細な出力が、指定された変数に保存されます。この変数には、出力を HTML あるいは XML ファイルに保存する目的で使用する ToHTML と ToXML のペアのメソッドが含まれます。</p>
<p>$TestOutput という名前のロガー変数に出力を保存するには、以下の構文を使用します。</p>
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
<td><p><em>PortId</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>テストする場所に関連付けられたポートの ID。MAC アドレスまたは IP アドレスを含めることもできます。</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIdSubType</em></p></td>
<td><p>省略可能</p></td>
<td><p>PortIDSubType</p></td>
<td><p>ポートのサブタイプです。この値は、数値または文字列で入力できますが、有効なサブタイプにする必要があります。有効なサブタイプは次のとおりです。</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>レジストラー サービスのポート番号。</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnet</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>サブネットの IP アドレスです。値は IPv4 アドレス (192.0.2.0 のようにピリオドによる桁区切り) として入力する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>リモート ユーザーの SIP アドレスです。</p>
<p>このパラメーターの値を指定する場合は、TargetFqdn または TargetUri パラメーターも必須です。</p>
<p>このパラメーターは、代理トランザクションのユーザーを設定していない場合に限り、TargetFqdn パラメーターを指定するときに必須です。代理トランザクションのユーザーが設定されているかどうかを確認するには、<strong>Get-CsHealthMonitoringConfiguration</strong> コマンドレットを実行します。</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSCredential</p></td>
<td><p>場所情報サービスにアクセスするためのユーザー資格情報を含んだオブジェクトです。このオブジェクトは <strong>Get-Credential</strong> コマンドレットを呼び出し、該当する資格情報を指定することで取得できます。</p>
<p>このパラメーターは、TargetUri パラメーターと UserSipAddress パラメーターが指定されており、このコマンドレットを実行するコンピューターにサーバー証明書が存在しない場合に必須です。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。

## 戻り値の種類

**Test-CsLisConfiguration** コマンドレットは、Microsoft.Rtc.SyntheticTransactions.TaskOutput オブジェクトのインスタンスを戻します。

## 関連項目

#### その他のリソース

[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)

